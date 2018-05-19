# [low-friction private data share &amp; data publication](https://github.com/ropensci/unconf18/issues/51)

> state: **open** opened by: **cboettig** on: **5/7/2018**

I&#x27;d love to have a robust and simple way to deal with data associated with a project.  

For individual data files &lt; 50 Mb, I have bliss.  I can commit these files to a private GitHub repo with ease; they are automatically available to Travis for any checks (no encoding private credentials); I can [flip a switch](https://guides.github.com/activities/citable-code/) and get a DOI for every new release once I make my data public.  

Or as another concrete example: my students are all asking me how to get there ~ 200MB spatial data files onto the private Travis builds we use in class.  

For larger data files, life is not so sweet.  The alternatives and their pitfalls, as I see them:

- Amazon S3.  Setup is far less trivial. Can be expensive if lots of people download my large files (maybe not an issue if it&#x27;s only for private data).  Working on travis requires encrypting keys.  No convenient button to press to make this public with DOI when ready. (though could manually upload to Zenodo).  Ability to directly access individual files (by URL).

- [datastorrr](https://github.com/ropenscilabs/datastorr).  Nearly perfect for data &lt; 2 GB; (adds data as &quot;attachments&quot; to GitHub releases, which aren&#x27;t version controlled.  Would love to see the branch that supports private authentication merged and a preliminary CRAN release.  Maybe good fodder for Unconf?

- Git LFS: Closest to my workflow for small data, but GitHub&#x27;s pricing model basically renders this unworkable.  (also no idea if Zenodo import captures LFS files).  @jimhester posted a brilliant work-around for this at https://github.com/jimhester/test-glfs using GitLab for the LFS side to store the large data files of a repo on GitHub (up to 10 GB), but I could never get this working myself. (Would love to get unstuck).

Other scientific repositories with less ideal solutions:

- &#x60;zenodo&#x60;.  Zenodo supports direct uploads with up to 50 GB of data, making it a great option for easy public data sharing.  No private option, no ability to download directly from DOI address.  

- &#x60;figshare&#x60; allows for private sharing and public sharing, DOIs for public data. Not sure file limits.  &#x60;rfigshare&#x60; package not actively maintained... No ability to download directly from DOI address

- &#x60;DataONE&#x60; Allows private and public sharing, supports ORCID auth, rich metadata model (burdensome to enter at first but could be useful with better tooling).  Requires re-authenticating with time-expiring token.  provides DOIs and other identifiers. No ability to download directly from DOI address, but does support ability to access individual files without downloading entire archive...


- ... more / other related strategies? 


Things that might be strategies but somehow never work well for me in this context:

- Box / Dropbox
- Google Drive



### Comments

---
> from: [**amoeba**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387234732) on: **5/7/2018**

Great idea! What about encrypted Dat?

This would mean that CI systems would download data from peers rather than fast CDNs like with S3/GitHub/etc which would mean slow builds for some proportion of users.
---
> from: [**Pakillo**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387235190) on: **5/7/2018**

Apart from [Dat](https://blog.datproject.org/2018/04/24/data-sharing-at-institutions-and-beyond-with-dat/), another option could be OSF: http://journals.sagepub.com/doi/full/10.1177/2515245918757689
---
> from: [**khondula**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387736742) on: **5/9/2018**

Another option to be aware of - I think that [Dataverse](https://dataverse.org/) repositories can accept individual files up to 2.5 GB and datasets up to 10 GB (according to [Nature](https://www.nature.com/sdata/policies/repositories#general) but also the [docs](http://guides.dataverse.org/en/4.6/user/dataset-management.html) say &quot;file upload limit size varies by installation&quot;). Anyone can submit to the flagship [Harvard Dataverse](https://dataverse.harvard.edu/) or [institutions](https://dataverse.org/institutions) can set up their own repositories. There is some discussion of setting dataset and file level permissions [here](http://guides.dataverse.org/en/4.6/user/dataset-management.html).
---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387882527) on: **5/9/2018**

I like the idea of dat, though It&#x27;s not clear what the status is of the project (seems all the main people have left?). Are there any similar projects?

I&#x27;d think we should steer away from figshare as they haven&#x27;t really been supporting their API

One thing that came to mind was http://academictorrents.com/ - though seems very tenuous, and login doesn&#x27;t have https, scary. There was also biotorrents, but even the domain name is gone now. Anyway, in general, perhaps a torrent solution could help in this space. Though I imagine many universities would by default block any torrent use from IP addresses coming from their members
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387889838) on: **5/9/2018**

It seems to me that the way to go with these is as common a front-facing API as possible with back-ends across multiple repositories which would handle DOI--&gt;file navigation.  Back-end repositories have their pros and cons in terms of private/public, file size, whether they have institutional archival arrangements, need for local software installation, DOI availability and reservation, etc.  It would be a good start to tabulate these so that people can know about them, and then prioritize those to focus back-end development on.  I think OSF checks most of the boxes, but people will differ.  This could work for even some more stringent/specialized archives like KNB/DataONE.

The front-end might be **datastorr** like in functionality and maybe API, but not be tied to GitHub.  You stash your API key or even your preferred back-end as environment variables, and then &#x60;data_release()&#x60;, &#x60;data_update()&#x60;, &#x60;dataset(ID,...), &#x60;set_public()&#x60;, &#x60;set_private()&#x60;, etc.

I&#x27;m not sure why the fact that they&#x27;re enterprise-focused is a reason to avoid figshare.  If lots of institutions use them that&#x27;s good.  Amazon is sure enterprise focused! If I recall development for rfigshare halted a bit because their API was unstable at one point, but they cover a lot of the bases.

Re: Dataverse, which also seems good, I note that Thomas Leeper is looking for a new maintainer for the [dataverse R package](https://github.com/IQSS/dataverse-client-r)
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/51#issuecomment-387892720) on: **5/9/2018**

Another good thing to assess for all the back-ends usage of common metadata standards - both for ease of development and long-term sustainability and compatibility across services.
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/51#issuecomment-388729608) on: **5/14/2018**

So I&#x27;ve been talking to some sociologist friends about this, and they share a major concern that is not unique:

1. Data sets are (often, and for them, almost always) very expensive to collect.
2. Many funding agencies and/or journals now require data sets to be openly published.
3. This mean that they in effect get one go and a good paper from their data before it&#x27;s released for general plundering and pillage, ultimately negatively impacting their research

A solution we discussed is a means of tracking and thereby always reliably ascribing data provenance, in effect ensuring that people otherwise suffering such effects would automatically be listed as authors of any papers using their data. And so...

### A solution

A [tangle](https://iota.org) (see whitepaper [here](https://www.iota.org/research/academic-papers)) potentially offers a perfect system for tracking data provenance.

### An unconf proposal

Software to constuct/modify tangle technology specifically for the sharing of data to ensure maintenance and attribution of provenance. Sharing/accessing a data set simply becomes a tangle transaction. Advantages:

1. Obviates any need for most of the above discussions because data access is P2P
2. Meta-data on provenance always maintained
3. Generators of data can always inquire about copies of their data, and/or standards can readily be set through ensuring citation refers to a tangle transaction.
4. The whole system is a graph, so (not too far down the track), the whole tangle of data meta-data will be able to be searched with &#x60;graphql&#x60;, offering a big boost to #26.
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/51#issuecomment-390275329) on: **5/18/2018**

All great ideas here.  I really like the approach @noamross outlines of identifying some core functionality that could be expressed in a generic front-end package, that could allow the user to swap in there preferred &#x27;back-end&#x27; storage choice, whether it&#x27;s a DOI-providing registry like Zenodo, a paid service like S3, or Blockchains-take-over-the-world thing.  





