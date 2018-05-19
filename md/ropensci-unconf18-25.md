# [Tools for discovering new packages (again)](https://github.com/ropensci/unconf18/issues/25)

> state: **open** opened by: **mpadge** on: **4/15/2018**

Direct follow-on from last year&#x27;s [two](https://github.com/ropensci/unconf17/issues/78) related [issues](https://github.com/ropensci/unconf17/issues/49) issues thanks to @sfirke. The [&#x60;flipper&#x60; package](https://github.com/ropenscilabs/flipper) is kinda developed, kinda stalled, but I personally would love to get that a bit more developed. It currently does full heavyweight text analysis  of &#x60;DESCRIPTION&#x60; files of all CRAN packages and produces a document similarity matrix that is used to connect one package to another.

The original vision of @njtierney was a standard swipe interface which we re-branded &quot;flip&quot; to enable quick and easy package browsing. In current state, one can simply:
&#x60;&#x60;&#x60;
flipper::flip (&quot;package about a bunch of interesting stuff&quot;)
&#x60;&#x60;&#x60;
And it&#x27;ll find a starting point in the matrix and then traverse strongest connections. We think that alone is kinda nifty, so please try! Required/desired refinements include:

1. Refining methods of traversing the matrix, including incorporating user stats with all associated concerns raised in [previous issue](https://github.com/ropensci/unconf17/issues/49). Extension to an ML framework would be very straightforward, because the whole thing works on fixed-sized binary vectors (like/dislike next jump along vector).
2. As @jimhester pointed out in [original issue](https://github.com/ropensci/unconf17/issues/78), trawling &#x60;man&#x60; files is likely to be even more informative. The infrastructure for this is all there, but it might push the limits of text similarity matrix processing?
3. Extension to all non-CRAN packages on github (I know there&#x27;s a list somewhere, and @maelle has her excellent [&#x60;is_package&#x60; function](https://github.com/ropenscilabs/ghrecipes/blob/master/R/is_package.R) for repo enquiry.)
3. Slick flippable interface

That&#x27;s all it would take to have most of the infrastructure there for one to type some text and start flipping through R packages until one discovered something desirable, interesting, or at least unexpected.

### Comments

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/25#issuecomment-384149801) on: **4/24/2018**

What about incorporating something like https://github.com/ropenscilabs/packagemetrics to the information returned, so that when searching for a package you get not only a description, but indicators of popularity and quality?
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/25#issuecomment-384178480) on: **4/25/2018**

That&#x27;s actually a great example. Incorporating new data means either a new network weighting matrix (for edges, or relationships between packages), or a new vector of nodal properties. I&#x27;ve been mostly concentrating on the former, but &#x60;packagemetrics&#x60; is a great example of the latter. These are computationally much cheaper, and equally important. Nodal vectors then need to be translated into edge matrices to guide traversal algorithms, and I also haven&#x27;t explored that translation yet at all. &#x60;packagemetrics&#x60; would provide a fine opportunity to develop that too.
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/25#issuecomment-384220571) on: **4/25/2018**

Possibly a project of its own, but one of the ways in which I discover packages is through use cases, often in the form of blog posts. I have yet to come up with an idea that wouldn&#x27;t be &quot;hackable&quot; in some capacity (i.e. there&#x27;d be nothing to stop someone to load a bunch of packages just for the pings, or whatever), but I&#x27;d be curious to think about a way of somehow highlighting package (or even function) usage in a way that ties back to the package itself- package usage in the wild, if you will. 
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/25#issuecomment-384221675) on: **4/25/2018**

Ah I love this @batpigandme! I&#x27;ve thought about adding this to the guidelines for rOpenSci packages https://github.com/ropensci/onboarding-meta/issues/39 , in practice it&#x27;d be a list inside README which is maybe not optimal since the README is often .Rbuildignored. But the README lives in the pkgdown website.
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/25#issuecomment-384221928) on: **4/25/2018**

obviously I&#x27;m open to suggestions of better ways to save this information in the package docs!
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/25#issuecomment-385951054) on: **5/2/2018**

It occurs to me that some of this work would be applicable to the editorial need of finding _authors_.  For instance, given a package submission, could we identify packages with similar uses, dependencies, or even code patterns? If so, that package&#x27;s author might make a good reviewer for the submission, and the same analysis could also alert us to overlap between the submission and another package.

That said, I&#x27;m painfully aware that journals have such systems for finding potential reviewers for manuscripts and the results are rarely really helpful.  Not sure if they are just based on keyword matching or something like that, though.
