# [Incorporate word doc track changes back into R markdown](https://github.com/ropensci/unconf18/issues/76)

> state: **open** opened by: **goldingn** on: **5/18/2018**

I know a lot of folks who are put off using R markdown for reports and scientific papers because they know it&#x27;ll be hard to incorporate the inevitable Word doc tracked changes they&#x27;ll get back from their collaborators/supervisors. 

I *think* pandoc could be used to convert both the original and edited doc back to markdown, and that could then be diffed to find the changes in text part of the markdown (if it&#x27;s a word doc, only text will have changed). It may then be possible to detect how those bits of text correspond to the R markdown document, and apply the changes there. 

It would also be nice to automate rendering of the changes. That can be done for pdfs via latexdiff: http://timotheepoisot.fr/2014/07/10/markdown-track-changes/
HTML might be trickier.

### Comments

---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390351927) on: **5/18/2018**

This is a whim and not something I&#x27;ve thought much about. If someone says &quot;this has already been done&quot; or &quot;this is not possible&quot; then I&#x27;ll be very happy to have my choice of project narrowed :) 
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390352497) on: **5/18/2018**

Somewhat related to #73
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390354690) on: **5/18/2018**

OK, so this definitely duplicates part of #42. In fact it probably serves as a half-decent summary of another project idea from that thread: automating @mmulvahill&#x27;s workflow for dealing with track changes from word
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390361021) on: **5/18/2018**

&gt; It may then be possible to detect how those bits of text correspond to the R markdown document, and apply the changes there.

I&#x27;m thinking you could just &#x60;grep()&#x60; for text matching that which changed in the original document, grabbing some sentences on either side to disambiguate multiple matches.


---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390361397) on: **5/18/2018**

a stretch goal could be to incorporate word comments into the R markdown using [this handy little trick](https://github.com/ropensci/unconf18/issues/74#issuecomment-390337985)
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/76#issuecomment-390363001) on: **5/18/2018**

I talk to myself in GitHub issues quite a lot.
