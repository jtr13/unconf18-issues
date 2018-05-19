# [Running minimal code with changed inputs](https://github.com/ropensci/unconf18/issues/53)

> state: **open** opened by: **OmaymaS** on: **5/8/2018**

I am not sure if this topic was tackled from all sides but thought about sharing.

**Problem**
When one runs a script, there could be a computationally heavy parts, but not all these parts require re-running. The inputs to these parts could be the same, the imported data might not have changed since the last time, etc.

In Rmarkdown, one can use caching in chunks to save some data importing. And in scripts one could write some conditions to control running some code.

**It would be more efficient if there&#x27;s a simple way to detect changes and decide which parts to be re-run automatically**

So if there are available solutions for this, let me know. If not we might think about certain functions or settings to help with this.


### Comments

---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387330966) on: **5/8/2018**

I think https://github.com/ropensci/drake could help with this?
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387368835) on: **5/8/2018**

Yes, I designed [&#x60;drake&#x60;](https://github.com/ropensci/drake) explicitly for this purpose. See &#x60;drake&#x60;&#x27;s [main example](https://ropensci.github.io/drake/articles/drake.html) for a proof of both concept and implementation.

It is so gratifying to see people independently discover the need for such a tool.
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387370309) on: **5/8/2018**

In lieu of the unconf, we&#x27;ll be having a two-day drake intensive! 😂
Seriously though, @wlandau, you should just post a list of all the things people have suggested for which drake provides a solution!
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387377365) on: **5/8/2018**

Thanks! It&#x27;s exciting how many of them are in this issue tracker alone.

I cannot physically be in Seattle on May 21-22, but I will do my absolute best to be present online.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387377399) on: **5/8/2018**

As much as I like **drake**, I see a space for a solution here is a little more lightweight.  Almost all R build systems force users to refactor their code away from scripts to functions.  There are good reasons for this but it adds a lot of overhead for people who are working with scripts. 

I think there could be a useful solution here wherein one does cacheing on an R script with a function like &#x60;source_cached()&#x60;.  In this solution, one would treat every line of code in the script like a **knitr** chunk.  Then one could either

 - Hash and save the script&#x27;s environment after every line (high storage), or
 - Hash every and save every object in the environment after every line (more overhead, less storage)

One could probably use &#x60;storr::driver_envionment()&#x60; for fast in-session storage, or a regular on-disk storr.

This wouldn&#x27;t be the most efficient solution but it would probably work very well for the case of a script that has gotten a bit unwieldy which someone is developing through interactive use.

Since this is meant to be a convenience tool, one would probably throw in an RStudio add-in, so one could run &#x60;source_cached()&#x60; on the current script with a hotkey.
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387378063) on: **5/8/2018**

@noamross I think &#x60;source_cached()&#x60; is absolutely possible, maybe even straightforward, with [&#x60;memoise&#x60;](https://github.com/r-lib/memoise) + [&#x60;CodeDepends&#x60;](https://github.com/duncantl/codedepends). And I agree, its bare simplicity would fill a niche.
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/53#issuecomment-387378542) on: **5/8/2018**

At one point, I thought maybe there could be an automatic way to turn an arbitrary R script into a &#x60;drake_plan()&#x60;, but this turns out to be extremely difficult to even think about.
