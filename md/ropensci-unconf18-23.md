# [parallel progress bars](https://github.com/ropensci/unconf18/issues/23)

> state: **open** opened by: **goldingn** on: **4/13/2018**

Getting progress bars and other information in the console for big jobs running in parallel is something I&#x27;ve wanted for a *looong* time. It is possible to get [GUI progress bars on windows](http://blog.revolutionanalytics.com/2015/03/creating-progress-bar-with-foreach-parallel-processing.html) (using TK), but this method apparently doesn&#x27;t work on mac/linux, and doesn&#x27;t print to the console.

It would be awesome if this functionality could be integrated with the [future](https://github.com/HenrikBengtsson/future) package, so that it can be used on any parallel backed the future API supports. It would be super awesome if we could enable export of the widely used progress bars in [&#x60;utils&#x60;](https://rdrr.io/r/utils/txtProgressBar.html), and the swanky progress bars in [&#x60;progress&#x60;](https://github.com/r-lib/progress).

There are technical hurdles around with communication between processes and differences between operating systems, but it&#x27;s definitely achievable. I&#x27;ve put together a gist&lt;sup&gt;1&lt;/sup&gt; with a prototype that does this the dumb (but generalisable) way; writing progress information to tempfiles which are read by the main process:
&#x60;&#x60;&#x60;r
library (future)
source(&quot;https://gist.githubusercontent.com/goldingn/d5a3aebfbc63eaadd92f0ff5ca811a5d/raw/12b552722020626e3f7014e1d9314266287acee0/parallel_progress.R&quot;)

foo &lt;- function (n) {
  for (i in seq_len(n)) {
    update_parallel_progress(i, n)
    Sys.sleep(runif(1))
  }
  &quot;success!&quot;
}

plan(multiprocess)
future_replicate(4, foo(30))
&#x60;&#x60;&#x60;
![parallel_progress](https://user-images.githubusercontent.com/4450731/38763057-68d44cf2-3fd7-11e8-8f2e-a30d22e06669.gif)

There are various ways this could be improved:

 - Printing progress bars rather than just a percentage process (preferably just embedding bars from the utils and progress packages).
 - Sending progress information from processes running on another file system (e.g. remote servers&lt;sup&gt;2&lt;/sup&gt;)
 - Handling more processes than threads
 - Handling sequential execution
 - Proper integration with the future package

Related discussions:

[Re. progress information in &#x60;future&#x60;](https://github.com/HenrikBengtsson/future/issues/141) in which @HenrikBengtsson says he&#x27;d rather it were a separate package, and suggests using [&#x60;processx&#x60;](https://github.com/r-lib/processx).

[Re. multiple progress bars in progress](https://github.com/r-lib/progress/issues/26) - having progress bars on separate lines isn&#x27;t trivial since not all consoles allow overwriting of more than one line of output.

Heads up to @HenrikBengtsson and @gaborcsardi, in case they know of progress on this topic that I&#x27;m not aware of!

---

&lt;sup&gt;1&lt;/sup&gt; https://gist.github.com/goldingn/d5a3aebfbc63eaadd92f0ff5ca811a5d 
&lt;sup&gt;2&lt;/sup&gt; my main motivation for this is getting live console progress bars for [greta](https://greta-dev.github.io/greta) jobs running on Google CloudML

### Comments

---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/23#issuecomment-381399060) on: **4/15/2018**

See also the &#x60;future&#x60; progress bar in &#x60;furrr&#x60; https://twitter.com/dvaughan32/status/985471691852742656
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/23#issuecomment-381415938) on: **4/15/2018**

This is a really important issue for me as well, and I&#x27;ve implemented the basis of the &#x60;RcppParallel&#x60; necessities too. This is also by &quot;dumb&quot; file dump, after spending  several days poring through loads of TBB code and finding no better idea. A merge of both R and C++ approaches would likely be really helpful. An **R** function for C++ code injection should also be possible because it&#x27;s just appended to the end of an &#x60;RcppParallel::worker::operator&#x60; call.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/23#issuecomment-381419743) on: **4/15/2018**

Awesome! Yeah, it would be great if we could handle both R &amp; C++ in the same package.


---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/23#issuecomment-390362317) on: **5/18/2018**

The &#x60;greta.live&#x60; reference above relates to producing live-streaming plots of an ongoing analysis (MCMC in this case, but it could be anything). That would require very similar functionality, in having a master process providing information to the users, from log files written by the subprocesses.

Writing this parallel progress bar code in a general way would make similar problems like that easily achievable.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/23#issuecomment-390365117) on: **5/18/2018**

Also, we could think about supporting progress bars for jobs running on remote machines (e.g. using &#x60;future&#x60;&#x27;s &#x60;plan(remote)&#x60;) with the awesome looking rOpenSci [&#x60;ssh&#x60; package](https://github.com/ropensci/ssh)
