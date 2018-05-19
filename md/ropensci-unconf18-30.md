# [Caching for drake](https://github.com/ropensci/unconf18/issues/30)

> state: **open** opened by: **ldecicco-USGS** on: **4/18/2018**

Data scientists are expert at mining large volumes of data to produce insights, predict outcomes, and/or create visuals quickly and methodically.  &#x60;drake&#x60; (https://github.com/ropensci/drake) has solved a lot of problems in the data-science-pipeline, but one thing we still struggle with is how to effectively collaborate on a large-scale project, without each contributor needing to run all of the workflow, or separating the workflows into many dis-jointed smaller workflows. In some large-scale projects, this is just not feasible.

It would be awesome if a wide community of R developers could come together and try to create a way for &#x60;drake&#x60; to have a collaborative caching feature. 

My group had set up a wrapper package for &#x60;remake&#x60; (&#x60;drake&#x60;&#x27;s predecessor) that allows tiny indicator files to be pushed up to github. These indicator files let the user know that the target was complete and the data was pushed up to some common caching location.  The next user would do an upstream pull request from Github, pull down the indicator file. The new user would not need to re-run a target that some other collaborator had already run, but instead pull the data down (if it&#x27;s needed) rather create it from the workflow. It got a bit awkward because we needed 2-3 remake targets to accomplish this, and that tripped up our &quot;non-power-user&quot; collaborators.

I&#x27;d propose the first step would be to develop caching workflow to Google Drive (using the &#x60;googledrive&#x60; package). Once the process was flushed out with using Google Drive, it could be more easily expanded to other data storage options (AWS using the &#x60;aws.s3&#x60; package for example). 

My gut says this might need to be a wrapper or companion package to &#x60;drake&#x60; (to keep the dependent packages minimized), but not sure. @wlandau and other &#x60;drake&#x60; experts: I would looove to hear any feedback you have on this idea. If in fact this issues is not-an-issue (ie...&#x60;drake&#x60; can already handle caching and I just missed it...totally possible...), then we could morph this issues into a group that helps create more content for a &#x60;drake&#x60; blogdown/bookdown book! 

The wrapper package for &#x60;remake&#x60; is here:
https://github.com/USGS-R/scipiper

#12 is another &#x60;drake&#x60;-based project. 












### Comments

---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/30#issuecomment-382582939) on: **4/18/2018**

I would be really stoked to have help on this! Remote/collaborative storage has been a major sticking point (see https://github.com/ropensci/drake/issues/198,  https://github.com/richfitz/storr/issues/55, and especially https://github.com/richfitz/storr/issues/61). I looked at [&#x60;scipiper&#x60;](https://github.com/USGS-R/scipiper), and I think a package like that could work for &#x60;drake&#x60;. I also think we might consider options that do not require changing the workflow plan. Ideally, we should be able to collaborate on Google Drive without adding targets or changing their commands.

A bit of background: &#x60;drake&#x60; uses @richfitz&#x27;s [&#x60;storr&#x60;](https://github.com/richfitz/storr) package for caching, usually in the local file system. By default, &#x60;make()&#x60; creates a [&#x60;storr_rds()&#x60;](http://richfitz.github.io/storr/reference/storr_rds.html) cache in a hidden &#x60;.drake/&#x60; directory to store the targets. You can use other &#x60;storr&#x60; caches such as &#x60;storr_environment()&#x60; and &#x60;storr_dbi()&#x60;, but these are not thread safe (e.g. for &#x60;make(jobs &#x3D; 8)&#x60;), and the &#x60;DBI&#x60; option requires a database connection that does not carry over to remote jobs (e.g. &#x60;make(parallelism &#x3D; &quot;future&quot;)&#x60; on HPC clusters). The [guide to customized storage](https://ropensci.github.io/drake/articles/storage.html) has more details.

As I understand it, the current practice for sharing results is to upload everything and hope that files in the &#x60;.drake/&#x60; cache does not get corrupted along the way. Services like Dropbox create disruptive backup files like the ones @kendonB [mentioned here](https://github.com/ropensci/drake/issues/198#issuecomment-362185998). For &#x60;drake&#x60;&#x27;s default cache (&#x60;storr_rds(mangle_key &#x3D; TRUE)&#x60;), it should be straightforward to clear out those extra files (https://github.com/richfitz/storr/issues/55#issuecomment-374230112). I just have not gotten around to building this into [&#x60;rescue_cache()&#x60;](https://ropensci.github.io/drake/reference/rescue_cache.html). @richfitz mentioned that &#x60;storr&#x60; might take care of some of the cleaning too (https://github.com/richfitz/storr/issues/55#issuecomment-367837646).

At this point, I think I should touch on some similar ideas / features that might help.

## drake hooks

The &#x60;make()&#x60; function has a &#x60;hook&#x60; argument, and you can use it to wrap things around the code that actually processes the target.

&#x60;&#x60;&#x60;r
custom_hook &lt;- function(code){
  force(code) # Build and store the target.
  sync_with_google_drive()
}
make(your_plan, hook &#x3D; custom_hook)
&#x60;&#x60;&#x60;

But I have not actually used this feature very much. To be honest, I designed it as a way to silence/redirect output, so we would need to do some internal refactoring on &#x60;drake&#x60; itself.

## A googledrive driver for storr?

I think it would be fantastic if &#x60;storr&#x60; supported an [RDS-like](http://richfitz.github.io/storr/reference/storr_rds.html) driver powered by &#x60;googledrive&#x60;.

&#x60;&#x60;&#x60;r
library(drake)
library(storr)
plan &lt;- drake_plan(...)
cache &lt;- storr_googledrive(&quot;https://drive.google.com/drive/my-drive/stuff/.drake&quot;)
make(plan, cache &#x3D; cache)
&#x60;&#x60;&#x60;

But from https://github.com/richfitz/storr/issues/61, that may be asking too much.

## Target logs: fingerprinting your pipeline

As for communication, @noamross had the bright idea of writing a log file to fingerprint the cache. If you commit it to GitHub, the changelog will show the targets that changed on each commit.

&#x60;&#x60;&#x60;r
library(drake)
load_basic_example()
make(my_plan, cache_log_file &#x3D; &quot;log.txt&quot;, verbose &#x3D; FALSE)
head(read.table(&quot;log.txt&quot;, header &#x3D; TRUE))
#&gt;               hash   type                   name
#&gt; 1 de0922cd962af6e2 target coef_regression1_large
#&gt; 2 331afc4b2b42b57f target coef_regression1_small
#&gt; 3 def5102800992696 target coef_regression2_large
#&gt; 4 2e52655d4d9ddb47 target coef_regression2_small
#&gt; 5 478684feec29a859 import             data.frame
#&gt; 6 e3bf796806094874 import                   knit
&#x60;&#x60;&#x60;

---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/30#issuecomment-382864213) on: **4/19/2018**

Update: if non-custom &#x60;drake&#x60; caches get corrupted when you upload them to Google Drive or Dropbox or the like, you can try to fix the problem with &#x60;drake_gc()&#x60; (development &#x60;drake&#x60; only). Related:

- [The issue explained](https://github.com/ropensci/drake/blob/master/vignettes/caution.Rmd#projects-hosted-on-dropbox-and-similar-platforms)
- https://github.com/ropensci/drake/issues/198
- https://github.com/ropensci/drake/issues/322
- https://github.com/richfitz/storr/issues/55

