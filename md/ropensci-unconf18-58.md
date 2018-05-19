# [A single interface to navigate the documentation of multiple packages](https://github.com/ropensci/unconf18/issues/58)

> state: **open** opened by: **maurolepore** on: **5/14/2018**

(Relates to #48, #25.)

How can you search all funcions, datasets and help files across multiple packages within a GitHub organization (e.g. tidyverse, rOpenSci)?

You may use https://www.rdocumentation.org/ or the search field of a GitHub organization; but I think those tools are too general. I propose to build a small package to create a searchable and clickable table of all functions or datasets by package -- including any number of packages within a GitHub organization. A good place to host such a table is on the website of the relevant GitHub organization. 

[Here is an example](https://forestgeo.github.io/fgeo/articles/fgeo.html#functions), which I built to solve my problem at the time. We could make the code more general and package it up.

### Comments

---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/58#issuecomment-390099876) on: **5/18/2018**

Summary: Build a small package to create a searchable and clickable table of all functions or datasets by package -- including any number of packages within a GitHub organization.
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/58#issuecomment-390110388) on: **5/18/2018**

Cross link to #25, which is a call for effectively the same thing. The [&#x60;flipper&#x60; package](https://github.com/ropenscilabs/flipper) has a lot of the necessary infrastructure for this.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/58#issuecomment-390371440) on: **5/18/2018**

Summary: This issue seems to be largely nested in #25. @mpadge, maybe we should discuss the overlap in person? Feel free to close.
