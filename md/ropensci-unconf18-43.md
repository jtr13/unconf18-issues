# [Implementation of non-linear dimensionality reduction algorithm (UMAP)](https://github.com/ropensci/unconf18/issues/43)

> state: **open** opened by: **seaaan** on: **4/26/2018**

I recently read about a new non-linear dimensionality reduction algorithm called UMAP ([github](https://github.com/lmcinnes/umap), [arxiv](https://arxiv.org/abs/1802.03426)), which is much faster than t-SNE, while producing two-dimensional visualizations that share many characteristics with t-SNE. I initially found out about it in the context of use on high-dimensional single-cell data in this [paper](https://www.biorxiv.org/content/biorxiv/early/2018/04/10/298430.full.pdf). 

The reference implementation is in Python (see github link above). It can be run in R through rPython as shown [here](https://gist.github.com/schochastics/2f83532f04729321b06822fbaa98f3ab). There is an R [package](https://github.com/jlmelville/smallvis) designed for comparing dimensionality reduction techniques that contains an implementation of UMAP, but this package is &quot;not suitable for large scale visualization&quot; and I&#x27;m not completely sure based on the README whether it is an accurate or approximate implementation. 

My thought is that the ideal would be a package focused on UMAP specifically, implemented in R or Rcpp. Unfortunately I am not at all an expert in this topic or familiar with the mathematics involved, so the best I would be able to do is try to translate the Python implementation into R. 


### Comments

---
> from: [**malisas**](https://github.com/ropensci/unconf18/issues/43#issuecomment-388906818) on: **5/14/2018**

Hi @seaaan , I use t-SNE at work all the time to analyze flow data and would potentially be interested in something like UMAP (especially when I have more than 100,000 data points and the t-SNE runtime starts to slow me down). I have zero experience in C++ or the mathematics involved but would like to learn both topics, and at any rate would like to express my interest in your proposal.

I&#x27;m quite ignorant about this entire topic, but what is the benefit of re-implementing the algorithm in R/Rcpp as opposed to relying on the bindings? (Though even if the user experience is the same, I can see how this could still be a really cool educational project.)
---
> from: [**seaaan**](https://github.com/ropensci/unconf18/issues/43#issuecomment-389045558) on: **5/15/2018**

I am also not an expert in this topic, but from what I can tell, the
advantage of an R or Rcpp version as compared to Python would mainly be
convenience. Running UMAP through rPython requires you to install Python
and UMAP first and then install rPython (which works from CRAN for Linux
and Mac but requires some additional effort for Windows). So you can get it
to work but it&#x27;s not as seamless as just installing a single package from
R.

I could be wrong about some of the steps as I haven&#x27;t had a chance to
actually test the rPython version yet, so maybe it&#x27;s not as complicated as
it sounds.

On May 14, 2018 10:56 AM, &quot;Malisa&quot; &lt;notifications@github.com&gt; wrote:

Hi @seaaan &lt;https://github.com/seaaan&gt; , I use t-SNE at work all the time
to analyze flow data and would potentially be interested in something like
UMAP (especially when I have more than 100,000 data points and the t-SNE
runtime starts to slow me down). I have zero experience in C++ or the
mathematics involved but would like to learn both topics, and at any rate
would like to express my interest in your proposal.

I&#x27;m quite ignorant about this entire topic, but what is the benefit of
re-implementing the algorithm in R/Rcpp as opposed to relying on the
bindings? (Though even if the user experience is the same, I can see how
this could still be a really cool educational project.)

—
You are receiving this because you were mentioned.
Reply to this email directly, view it on GitHub
&lt;https://github.com/ropensci/unconf18/issues/43#issuecomment-388906818&gt;,
or mute
the thread
&lt;https://github.com/notifications/unsubscribe-auth/AKDNdeMEDuPc3cWkMKAMTDS1Y2jZLJ-Zks5tycVdgaJpZM4TkgTE&gt;
.

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/43#issuecomment-389118289) on: **5/15/2018**

If the Python version is performance, it might be worthwhile to try to wrap
it with the **reticulate** package rather than port it. With **reticulate**
you can share in-memory objects with R so data transfer is more efficient,
and I think is cross-platform.

&gt;

---
> from: [**seaaan**](https://github.com/ropensci/unconf18/issues/43#issuecomment-389322654) on: **5/15/2018**

Thanks! So here are the options as I see them: 

* Access UMAP through rPython as described [here](https://gist.github.com/schochastics/2f83532f04729321b06822fbaa98f3ab). Somewhat complicated installation process? 
* Wrap UMAP using [reticulate](https://github.com/rstudio/reticulate). Also requires installing Python stuff but might be easier? 
* Rewrite UMAP in R or Rcpp. Easy installation but more work for us. 
---
> from: [**seaaan**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390212340) on: **5/18/2018**

Summary: UMAP is a new non-linear dimensionality reduction algorithm that&#x27;s like t-SNE but faster. It can be used for all kinds of data but I&#x27;m interested in it for flow cytometry and single cell RNA sequencing. We could either wrap the Python implementation or implement it ourselves in R/Rcpp.
---
> from: [**PeteHaitch**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390288247) on: **5/18/2018**

There are definitely people in the Bioconductor community interested in this (although I don&#x27;t know if any are going to be at the unconf). We discussed a reticulate wrapper around the Python implementation when a few of us were together at the [collaborative computational tools for the human cell atlas](https://meetings.czi.technology/human-cell-atlas/comp-tools/). @drisso may remember who showed the most interest in doing this or of any efforts underway.

---
> from: [**stefaniebutland**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390292077) on: **5/18/2018**

&gt; There are definitely people in the Bioconductor community interested in this (although I don&#x27;t know if any are going to be at the unconf)

I think @lcolladotor said he attends annual Bioconductor meetings. Lori Shepherd @lshep from Bioconductor Core team participated in unconf17
---
> from: [**drisso**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390293113) on: **5/18/2018**

Not surprisingly @LTLA was part of the conversation. It was in the more general context of how to create an interface between Bioconductor and scanpy. I won&#x27;t be at the unconf, but I&#x27;m happy to help remotely, if needed!

I think a reticulate wrapper could be the easier solution, unless a C++ implementation is much faster than the original python. 

---
> from: [**LTLA**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390321304) on: **5/18/2018**

I won&#x27;t go into it too much to avoid derailing this thread, but my idea would be to make it as easy (and standard, and reliable) to call Python code in an R package as it is to call C/C++/Fortran code. The difficulty lies in how we are able to (or, currently, not!) control the versions of Python and its packages, in order to guarantee consistent behaviour and ensure easy installability across systems. 

A reticulate wrapper around UMAP would indeed be easier in terms of the amount of initial work. However, without a standard framework for controlling Python packages and versions from within R, it shifts the burden onto the end-user (and ultimately back to developers in terms of support requests).
---
> from: [**lcolladotor**](https://github.com/ropensci/unconf18/issues/43#issuecomment-390370646) on: **5/18/2018**

Hi. I don&#x27;t really use Python and was not part of the work Peter, David and Aaron Lun did. So I can&#x27;t really comment on this thread.

Best,
Leo
