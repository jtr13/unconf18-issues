# [Batch File Processing Workflow](https://github.com/ropensci/unconf18/issues/47)

> state: **open** opened by: **laderast** on: **4/30/2018**

Hi Everyone,

I&#x27;ve been kicking this idea around for a little bit. Our group does a lot of batch processing of input files when we run our pipeline for flow cytometry data. Sometimes the output of a step will fail, and we have to flag the files that fail so they aren&#x27;t passed through further steps in the pipeline.

When I do this currently, I basically build file manifests (location of files with relevant metadata) and run some sort of processing in R. I was thinking maybe by incorporating data assertions (like with assertr), we can have a workflow that shows when files pass a step, and flags those files that fail a processing step. In the end, we can display to users of the pipeline which files passed and which files didn&#x27;t, and which steps.

Maybe there&#x27;s a little germ of an idea here that might work for the unconf. I&#x27;m not sure, so I&#x27;m putting it out there.

### Comments

---
> from: [**karthik**](https://github.com/ropensci/unconf18/issues/47#issuecomment-385476331) on: **4/30/2018**

Drake can do a lot of what you are asking for (cc @wlandau-lilly). &#x60;vis_drake_graph&#x60; on your Drake plan should show you steps that failed (in red). Fixing those should only re-run those steps and not everything from scratch. You might take a look at https://github.com/ropensci/drake and see if it&#x27;s something that matches your needs.
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/47#issuecomment-385478773) on: **4/30/2018**

+1 to that! Suppose we&#x27;re working with [this data analysis workflow](https://ropensci.github.io/drake/articles/drake.html) and one of our functions does not work.

&#x60;&#x60;&#x60;r
create_plot &lt;- function(data) {
  ggplot(data, aes(x &#x3D; Petal.Width, fill &#x3D; Species)) +
    geom_histogram(binwidth &#x3D; 0.25) +
    theme_gray(20) +
    BAD_LAYER
}
&#x60;&#x60;&#x60;

We run our workflow and see.

&#x60;&#x60;&#x60;r
&gt; make(plan)
target raw_data
target data
target fit
target hist
fail hist
Error: Target &#x60;hist&#x60;&#x60; failed. Call &#x60;diagnose(hist)&#x60; for details. Error message:
  object &#x27;BAD_LAYER&#x27; not found
&#x60;&#x60;&#x60;

Diagnostics include warnings, errors, messages, and other context.

&#x60;&#x60;&#x60;r
&gt; diagnose(hist)
&gt; diagnose(hist)
$target
[1] &quot;hist&quot;

$messages
NULL

$error
&lt;simpleError in create_plot(data): object &#x27;BAD_LAYER&#x27; not found&gt;
&#x60;&#x60;&#x60;

You can list the failed targets programatically.

&#x60;&#x60;&#x60;r
&gt; failed()
[1] &quot;hist&quot;
&#x60;&#x60;&#x60;

As Karthik mentioned, these failures are shown in the dependency graph.

&#x60;&#x60;&#x60;r
config &lt;- drake_config(plan)
vis_drake_graph(config, targets_only &#x3D; TRUE, full_legend &#x3D; FALSE)
&#x60;&#x60;&#x60;

![capture](https://user-images.githubusercontent.com/1580860/39442170-60113bee-4c7e-11e8-808d-b863b9d81e2a.PNG)


---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/47#issuecomment-385486142) on: **4/30/2018**

Ah, very cool. I didn&#x27;t know about Drake!
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/47#issuecomment-388654847) on: **5/13/2018**

@laderast, would &#x60;purrr::safely()&#x60; and &#x60;purrr::possibly()&#x60; help you?
---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/47#issuecomment-389269216) on: **5/15/2018**

Thanks @maurolepore - &#x60;purrr::safely()&#x60; is a nice approach
