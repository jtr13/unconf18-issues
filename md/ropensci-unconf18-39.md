# [Review of literature for API mocking and testing](https://github.com/ropensci/unconf18/issues/39)

> state: **open** opened by: **noamross** on: **4/24/2018**

A pretty frequent topic of conversation in rOpenSci circle is approaches to [testing packages that call Web APIs](https://discuss.ropensci.org/t/best-practices-for-testing-api-packages/460).  I think this topic could use a &quot;review of literature&quot; - a systematic look at the different packages for this in the ecosystem, how their interfaces differ, the advantages and disadvantages of each, missing functionalities to be developed, and best practices/design patterns for testing packages.

Outputs for this might just be a blog post or vignette, or a series of issues and PRs across the package ecosystem.

Notably @sckott is nearing release of [**vcr**](https://github.com/ropensci/vcr), it could host the vignette and this review might be good for making sure it covers the use-cases that we explore.

### Comments

---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/39#issuecomment-384155929) on: **4/25/2018**

&amp; just started book https://github.com/ropensci/http-testing-book (not to be published, just a book form pile of words)
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/39#issuecomment-384158078) on: **4/25/2018**

&gt; not to be published

hey, who knows
---
> from: [**michaelquinn32**](https://github.com/ropensci/unconf18/issues/39#issuecomment-385848790) on: **5/1/2018**

This is for C++, but covers some of the broad issues.
https://github.com/google/googletest/blob/master/googlemock/docs/ForDummies.md
