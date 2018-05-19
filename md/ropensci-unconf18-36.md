# [Compiling R logic to the browser](https://github.com/ropensci/unconf18/issues/36)

> state: **open** opened by: **noamross** on: **4/24/2018**

_(A rambling post that might converge into an actual unconf project)_

I&#x27;ve become intrigued lately with the applications of WebAssembly, the latest approach to running compiled code in the browser.  I wrote up a [proof-of-concept](https://noamross.github.io/wassa/inst/doc/adventures-in-webassembly.html) of how one could run the same C++ code via Rcpp or in an htmlwidget.  I think some exploration of use cases and design patterns of shared R/browser implementations of algorithms in this way could make a good unconf project. 

It&#x27;s a huge project to try to port R runtime to the browser this way, but there are a number of R packages that generate C(++) code for fast model execution that could then be compiled to WebAssembly in the browser:

-  [NIMBLE](https://r-nimble.org/) compiles a sub-set of R code into C++ code that uses the Eigen library.
-  [odin](https://github.com/mrc-ide/odin) by @richfitz generates C++ code from ODE systems defined in R
-  [Stan](http://mc-stan.org/) models are compiled to C++ before being compiled to binary. 
-  [pomp](https://kingaa.github.io/pomp/) models use C templates with snippets provided by the model-builder.

For any of these, one could imagine fitting and optimizing models in R, then porting them to the browser to power pages/apps built on simulation or prediction from those models.  For instance, I could use **odin** to fit a set of ODEs to data, and then port the fit odin model to an htmlwidget that lets the user simulate and visualize those ODE systems, with the option of changing some parameters or initial conditions.  Getting a Stan model to run in the browser in an htmlwidget seems super interesting, too - it would be like **shinystan** without Shiny.  (One of the Stan devs has said they would be interested in helping with this.)

Alternatively, keeping the concept of _compiling to the browser_ but in a very different way, we could compile **dplyr** code to the browser by using **dbplyr** to create SQL from R expressions, then sending this SQL to be executed by the browser via a JavaScript SQL implementation such as [alasql](http://alasql.org/).  One could create &quot;live&quot; htmlwidgets this way: they could query a remote data source, transform the data, and then feed it to an output like a plot.ly graph or a DataTable, all in the browser with no server back-end. 

Finally, a totally different idea suggested to me recently was using this for distributed computing.  Could one create htmlwidgets that run some code in the user&#x27;s browser and send results back home? (For instance, running one MCMC chain of a Stan model?)

Thoughts?

### Comments

---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/36#issuecomment-384133562) on: **4/24/2018**

Just wanted to add that greta can compile a large subset of R code (even if it doesn&#x27;t have stochastic elements) to a tensorflow graph, which could be run in-browser with [tensorflow.js](https://js.tensorflow.org/) (or [remotely/on GPUs](https://github.com/rstudio/cloudml) or [on a smartphone/tablet](https://www.tensorflow.org/mobile/tflite/))

I&#x27;ve also considered breaking that functionality out into a separate package that doesn&#x27;t do statistical modelling, and/or providing other backends than tensorflow (even C++?) 
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/36#issuecomment-384135116) on: **4/24/2018**

Indeed, I sort of left out tensorflow (and keras) because there&#x27;s already so much going on with them in this paradigm via tensorflow.js (and keras.js).  But a neat idea might be something like a **greta**-specific widget that executes via tensorflow.js, sort of like **shinystan**.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/36#issuecomment-384136354) on: **4/24/2018**

Yeah, that would be ace! If we go down that route, it might be worth checking in with JJ, in case he&#x27;s planning tensorflow js integration as part of the RStudio tensorflow suite.

@michaelquinn32 might be interested in something tensorflowy like this? 
---
> from: [**michaelquinn32**](https://github.com/ropensci/unconf18/issues/36#issuecomment-384376677) on: **4/25/2018**

Add it to the list!

Sorry, but I don&#x27;t have a sense of priority yet, and I REALLY need to read the greta internals to see where additions will be reasonable.

From the apps side, there&#x27;s also all of the tensorflow serving work to think about. @javierluraschi has been doing a bunch of awesome work on that too.
https://github.com/rstudio/tfdeploy

I&#x27;m not sure about evaluating the tradeoff between doing all of it in app vs treating the app as a client. 
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/36#issuecomment-385133246) on: **4/27/2018**

This list might be handy: https://github.com/terrytangyuan/ctv-model-deployment
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/36#issuecomment-385284871) on: **4/29/2018**

Despite the potential of tensorflow.js, I&#x27;m still pretty interested in the other pipelines I describe above, (WebAssembly and alasql), especially from the perspective of leveraging C/SQL infrastructure already developed for R so as to make it available browser-side.  I suggest we discuss ideas for both here, and we might split these out into different options during the issue-consolidation phase closer to the unconf.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/36#issuecomment-385287101) on: **4/29/2018**

Yep, good idea! 
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/36#issuecomment-387897225) on: **5/9/2018**

Not a lot of other conversations here, but I basically see three current projects described:

-  **An htmlwidget that does fetching ETL and display from remote data sources using dplyr SQL translation and &#x60;alasql&#x60;**:  This seems very doable and quite practical.
-  **Compiling a Stan model to WebAssembly**:  Seems like a good proof-of-concept that could be done if someone knows their way around Stan C++, but potentially a bear otherwise.
- **Deploying a greta model via tensorflow.js**:  Obviously we have the people for it :), if this is what Nick and Mike end up interested in.

I&#x27;m still sort of interested in other out-of-the-box WebAssembly ideas.
