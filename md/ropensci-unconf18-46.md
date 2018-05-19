# [Help researchers track results in manuscript back to source code.](https://github.com/ropensci/unconf18/issues/46)

> state: **open** opened by: **maurolepore** on: **4/29/2018**

How do you link a result in your manuscript back to its source code? This is fundamental to reproducible research. It seems basic and straight forward but, in the wild world I live, it is not. Research gets messy quickly: After a few weeks out of touch with a project, wish me luck finding my own stuff; and forget about finding code in a project managed by someone else. 

My inelegant solution is this:

* I tag each analysis with a random label and a description.

&#x60;&#x60;&#x60;R
ab12 &lt;- &quot;Code which result proves that Earth is not flat.&quot;
result &lt;- code
&#x60;&#x60;&#x60;

* I keep the tag associated with that analysis throughout the lifecycle of the manuscript.

![image](https://user-images.githubusercontent.com/5856545/39407455-559397a6-4b94-11e8-84f1-e442606b59e9.png)

* Whenever I need to go back to the source code, I use RStudio&#x27;s _Go to File/Function_.

![image](https://user-images.githubusercontent.com/5856545/39407535-637b8e68-4b95-11e8-878a-2a7906db1164.png)

Is there a tool or better approach? What general recommendations do you have for researchers across a range of willingness to use version control and RStudio projects?

### Comments

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/46#issuecomment-385285090) on: **4/29/2018**

This is a great approach.  It is of course related to #42, but potentially applies very different workflows.   For projects where I&#x27;m not compiling the final output I like to have an &#x60;outputs&#x60; folder which has not only images and tables but an Rmd or text file output with all the essential quantitative values that make their way into the manuscript.  Usually things can be traced back from the filenames there.
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/46#issuecomment-385285276) on: **4/29/2018**

[&#x60;drake&#x60;](https://github.com/ropensci/drake) + literate programming may help a bit. [&#x60;Drake&#x60;&#x27;s main example](https://ropensci.github.io/drake/articles/drake.html)&#x27;s has a data analysis workflow with [this R Markdown report](https://github.com/ropensci/drake/blob/master/inst/examples/main/report.Rmd) at the very end. The active code chunk has calls to &#x60;loadd(fit)&#x60; and &#x60;readd(hist)&#x60;, which serve to 

1. Fetch targets from the cache when the report compiles, and
2. Tell [&#x60;drake&#x60;](https://github.com/ropensci/drake) to treat &#x60;fit&#x60; and &#x60;hist&#x60; as formal dependencies (so &#x60;drake::make()&#x60; rebuilds the &#x60;report.html&#x60; if there is a change to &#x60;fit&#x60; or &#x60;hist&#x60;.) Even if you don&#x27;t care about Make-like build management, you can still see where these data objects fit into the pipeline.

![screenshot_20180429_175059](https://user-images.githubusercontent.com/1580860/39411322-e80d42ee-4bd5-11e8-8f3a-a56caa5b5203.png)

In that sense, using and annotating an artifact are one in the same.

I am curious to know the views of @gmbecker and @duncantl on the original issue. As I understand it, provenance is a major focus of [&#x60;trackr&#x60;](https://github.com/gmbecker/trackr), [&#x60;RCacheSuite&#x60;](https://github.com/gmbecker/RCacheSuite), and [&#x60;CodeDepends&#x60;](https://github.com/duncantl/CodeDepends).

---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/46#issuecomment-385285604) on: **4/29/2018**

Edit: as for linking data objects back to the source code, the dependency graph shows the functions that generated &#x60;fit&#x60; and &#x60;hist&#x60;. That&#x27;s an important point I forgot to add. The previous graph excluded functions. See below for the full graph.

![screenshot_20180429_180514](https://user-images.githubusercontent.com/1580860/39411437-ebbe9080-4bd7-11e8-9843-d1870798f37f.png)

---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/46#issuecomment-385291374) on: **4/29/2018**

Awesome! I&#x27;m learning so much and the unconference hasn&#x27;t even started! Thank you!
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/46#issuecomment-385295746) on: **4/29/2018**

It&#x27;s such a fantastic crowd! I wish I could be at unconf to soak up more knowledge in person.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/46#issuecomment-390371674) on: **5/18/2018**

Summary: 
* Relates to #58, __drake__ (@wlandau),  __trackr__, __RCacheSuite__, and __CodeDepends__ (linked above; @gmbecker and @duncantl). 
* __drake__ comes up very often. Should we discuss to become more familiar with it?
