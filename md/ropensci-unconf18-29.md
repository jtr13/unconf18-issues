# [ROpenSci storage for package caching](https://github.com/ropensci/unconf18/issues/29)

> state: **open** opened by: **mpadge** on: **4/18/2018**

Lots of packages need caching. When things get complicated enough, packages may need to access their own eternal data to do their internal stuff. This means caching somewhere, somehow, in a form that is reliable and available. This costs money.
&gt; Oh, I don&#x27;t have any of that; okay, I can&#x27;t do that package.

And there it ends. How about considering applications to ROpenSci to (financially) support caching via some suitable provider? The [&#x60;flipper&#x60; package](https://github.com/ropenscilabs/flipper) is a case in point. This works at the moment because it only trawls the &#x60;CRAN_package_db&#x60;. We would like to extend this to all [&#x60;man/&#x60; directories](https://github.com/ropensci/unconf18/issues/26#issuecomment-382140279), all non-CRAN packages on github, and [many potential other places](https://github.com/ropenscilabs/flipper/issues/6). This is impossible without some sorta cloudy caching scheme.

Any chance of ROpenSci having an application scheme whereby those with existing ROpenSci packages apply for access to a wee chunk of server space?

### Comments

---
> from: [**ldecicco-USGS**](https://github.com/ropensci/unconf18/issues/29#issuecomment-382478445) on: **4/18/2018**

I was literally just crafting a proposal for a caching process for &#x60;drake&#x60;! I think it&#x27;s a slightly different use-case than what you are proposing here, but maybe we can combine forces and think of all the caching use-cases and needs.  (See #30 )
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/29#issuecomment-382584002) on: **4/18/2018**

When it comes to caching, I am a huge fan of @richfitz&#x27;s [&#x60;storr&#x60;](https://github.com/richfitz/storr) package. It&#x27;s a general key-value storr with an expanding variety of backends (&quot;drivers&quot;), including &#x60;storr_rds()&#x60; and &#x60;storr_dbi()&#x60;. Maybe a remote &#x60;storr&#x60; driver would help here? Related: http://richfitz.github.io/storr/articles/external.html.
