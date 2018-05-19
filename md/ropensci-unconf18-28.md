# [Promote data-packages to facilitate project-oriented workflows](https://github.com/ropensci/unconf18/issues/28)

> state: **open** opened by: **maurolepore** on: **4/17/2018**

Can we facilitate project-oriented workflows by promoting data-packages?

Although researchers would benefit from using self-contained projects, they rarely do. This workflow seems more common:
* Store the data locally in one directory.
* Import the data from multple R sessions and run analyses.

This approach is problematic becaue each R session is not self-contained.

A neat solution is to build a data-package. While its source may live in a single local directory, the data can be accessed by loading the data from any project, keeping it self-contained. 

But many reasearchers don&#x27;t know this approach or believe that building a package is too difficult. Indeed, building a basic data-package requires relatively few tools. The process can largely be handeled with the __usethis__ package (by Hadley Wickham, @jennybc and RStudio). Can we describe the steps required to build a data-package via a series of __usethis__ functions?

(As a starting point here is a [checklist](https://fgeo.netlify.com/2018/04/04/2018-04-04-building-infrastructure-for-a-data-package/) I use to build data-packages.)

### Comments

---
> from: [**ldecicco-USGS**](https://github.com/ropensci/unconf18/issues/28#issuecomment-382503485) on: **4/18/2018**

I&#x27;ve had good luck with using a data-package for some projects. It became rougher though to rely on a package as my data got bigger and I got more collaborators (both with updating the data package and version controlling the data on github). My group has put a pretty good deal of effort into creating a robust internal repository that allows us to do this, but it&#x27;s not trivial with bigger data. We could use Git Large File Storage (LFS)...but we had some issues getting all our collaborators to use that. Certainly data quickly becomes to big for CRAN, their package size requirements are pretty limiting.

Another option we can consider is focus on easy data caching...where we can use google drive, aws, other data storage options....(theme of the day....see #29 #30 )
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/28#issuecomment-382511170) on: **4/18/2018**

Interesting ideas!  

I think another thing we want to think carefully about here is how to keep in mind data archiving and publishing best practices as part of this workflow.  For instance, while I love the whole &#x60;data-raw&#x60; thing with storing scripts that go from raw data to tidy data, I get nervous about encouraging R packages as an ideal way to document, distribute and manage data.  

It is probably better to store data in a plain-text format, along with some basic metadata, that is agnostic to software details.  

I think this highlights the relatively large divide between how we go about preparing data for archiving / publishing vs how we use data day-to-day.  I think it would be a big win to to narrow that gap a little with tools that make it easier to do both.  For instance, several data repositories (figshare, DataONE) allow for data to be archived &#x27;privately&#x27; with access granted to only explicit collaborators.  This means users can benefit from having a secure, redundant, versioned copy of data sets that can be accessed by remote collaborators and scripted into their workflows.  Then publishing becomes just a matter of flipping a switch from private to public and not one of uploading data to the repo from scratch....
---
> from: [**karthik**](https://github.com/ropensci/unconf18/issues/28#issuecomment-382545804) on: **4/18/2018**

&gt;  I get nervous about encouraging R packages as an ideal way to document, distribute and manage data.

Exactly! This is something that @njtierney and I have been talking about a lot lately as we are documenting all of this. We are developing a set of best practices around sharing different types of data (more on that in a bit) but the general recommendation is not to share data inside R packages unless it&#x27;s explicitly for teaching/training or for supporting small examples. CRAN limits packages to 5mb, so that also imposes additional challenges (binary data is even less accessible outside the package ecosystem). 

You might also have also seen this paper: [Hosting Data Packages via drat: A Case Study with Hurricane Exposure Data ](https://journal.r-project.org/archive/2017/RJ-2017-026/index.html). This is also somewhat fragile and does not address the divide that Carl talks about above.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/28#issuecomment-383290210) on: **4/21/2018**

&gt; It became rougher though to rely on a package as my data got bigger ... Certainly data quickly becomes to big for CRAN

-- @ldecicco-USGS 
 
Thanks for noting this. That&#x27;s great point I hadn&#x27;t considered. I was thinking of packages not stored on CRAN but on GitHub or even locally. My suggestion for datapackages as a way to facilitate a project oriented workflow targets a problem that I find most commonly. 

It seems the researchers you have in mind are fluent in R enough to build and publish packages to CRAN. In contrast, most of the researchers I work with (ForestGEO, a network of 65 research groups around the world) don&#x27;t build packages nor use project oriented workflows. These are amazingly brilliant researchers doing amazing science. And I&#x27;m trying to help them become even more productive by providing them with tools and sytems that reduce the friction in taking more reproducible workflows.

Considering your point, I would love to brainstorm how else (other than via data-packages) the workflow I described above -- which I find most commonly  -- could be made project-oriented. It seems that hosting the data on a remote, versionable, repository is realatively easier and safer. (More on that in the next comment).
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/28#issuecomment-383291259) on: **4/21/2018**

&gt; [There is a] large divide between how we go about preparing data for archiving / publishing vs how we use data day-to-day. I think it would be a big win to to narrow that gap a little with tools that make it easier to do both. 

-- @cboettig 

I agree. I have experimented with [GitHub and Zenodo](https://guides.github.com/activities/citable-code/) and I liked it. You may already know this but let me summarize here what the win is:

After a not-too-hard setup, every GitHub release of a repo -- which can be created by adding a new tag with Git and pushing it to GitHub -- is automatically published to Zenodo. Zenodo is a data repository similar to Figshare -- it generates a DOI for each version of a project. 

In my opinion the workflow is already acceptably simple: From a local repo, pushing a new tag to GitHub generates both a new GitHub release and a new DOI. If the repo is a data-package, you&#x27;d be both releasing a new version of the package and publishing it to a service citable via a DOI.

What ideas do you have to improve even further the build-publish integration?








---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/28#issuecomment-383291936) on: **4/21/2018**

&gt; We are developing a set of best practices around sharing different types of data (more on that in a bit) 

-- @karthik 

Great! I&#x27;ll love to learn what you produce.

And thanks for pointing to that paper.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/28#issuecomment-384050562) on: **4/24/2018**

I gave a talk on this subject at NYR last week, slides here: https://github.com/noamross/2018-04-18-rstats-nyc/blob/master/Noam_Ross_ModernDataPkg_rstatsnyc_2018-04-20.pdf .  They&#x27;re not that self-explanatory, but my point was largely about how there&#x27;s a real trade-off between scientific best archival practices and the conveniences available from wrapping data in a package, but they can be minimized with some design approaches.

I think a good solution here is in-reach, but we need to devote some time and resources to it.  A good path is having a fully functional API packages for Zenodo and other repositories, and having these as back-ends to @richfitz&#x27;s **datastorr** package which does such great data versioning, distribution and caching (and getting **datastorr** to CRAN). Maybe we could make a push on these things at the unconf.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/28#issuecomment-390372283) on: **5/18/2018**

Summary: A lot of thought has already been invested in this. For example, @karthik and @njtierney are documenting best practices; and @noamross has slides and ideas to implement a solution involving @richfitz&#x27;s __datastorr__ package. Relates to #29, #30.
