# [&quot;Safety Profiler&quot; for User package libraries](https://github.com/ropensci/unconf18/issues/34)

> state: **open** opened by: **hrbrmstr** on: **4/24/2018**

We embark on unconf 2018 at an appro time: R 3.5.0 launches and lots of folks are feeling the x.y package upgrade/sidegrade process.

However, we could build a profiler/auditor — much like the emergent &#x60;node audit&#x60; — which would let folks know just how lagging they are and what potential safety issues they may be facing as a result.

This could take a bit of work and would also require delving into packages that include C[++] libraries with them.

### Comments

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/34#issuecomment-384122567) on: **4/24/2018**

One possibility is to build this as a wrapper/plugin for [**goodpractice**](https://github.com/MangoTheCat/goodpractice).  At last year&#x27;s unconference Gabor created a plug-in structure and Hannah Frick has been working on extending and [documenting](https://mangothecat.github.io/goodpractice/articles/goodpractice.html) it recently.  We&#x27;re likely going to have several plug-in checks specific for rOpenSci.  A set of security-specific would be a great addition to those.  
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/34#issuecomment-384124962) on: **4/24/2018**

I think it&#x27;s also good to just articulate what kinds of things this can focus on. For example what kinds of user inputs are being taken and are they being sanitized, when does that matter and when does that not matter.
Somewhere the deidentification issue should come in too.
