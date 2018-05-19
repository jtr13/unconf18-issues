# [Taking some pain out of finding/linking to unique IDs?](https://github.com/ropensci/unconf18/issues/52)

> state: **open** opened by: **magpiedin** on: **5/8/2018**

A wish/need/dread for data standards came up in [issue 41](https://github.com/ropensci/unconf18/issues/41), and brought a few ideas to mind:
- For cleaning Darwin Core/biodiversity data, there are some good tools (e.g., [Kurator](http://wiki.datakurator.org/wiki/Kurator), which looks like it&#x27;s getting [some translation to R](https://github.com/rstats-gsoc/gsoc2018/wiki/Darwinazing-biodiversity-data-in-R)). 
- For finding IDs for publications, people, specimens, taxa, etc, there are lots of great resources (&#x60;fulltext&#x60;, &#x60;rorcid&#x60;, &#x60;spocc&#x60;, &#x60;taxize&#x60;...)
- But for actually finding &amp; linking the pieces (specifically, the unique IDs for publications, specimens, people, etc), projects often run out of energy/time/awareness
 
Any thoughts on a helper/gentle-reminder app or lesson for suggesting linkable values contained within datasets or papers -- for instance, by indexing what types of fields/records exist in a given dataset, and suggesting relevant packages from CRAN or ropensci that could retrieve identifiers? 

I realize I&#x27;m glossing over some major obstacles to actually linking data (e.g., cleaning free text values &amp; resolving entities is enough of a mountain; plan-ahead is better than fix-it-in-post when possible), so I&#x27;m all ears if this could use more [or a different] focus. 
Or if something magical already exists along these lines.
...Or if there&#x27;s a good/sustainable alternative to developing tools/packages that rely on multiple API wrappers?...

### Comments

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/52#issuecomment-387385973) on: **5/8/2018**

This is a hard problem! I have an as-yet unfunded proposal to develop a system that tries to use text-recognition ML identify fields in a dataset and link them to appropriate ontologies - for instance, recognizing which columns are species, which are publications, and such.  I believe that @amoeba has worked something similar for DataONE. 

Ease of use is definitely one of the big challenges - I could see something like a function like &#x60;find_ids()&#x60; that you could run on a document and it would return items that might have IDs (author names, species names, publications) using a text-recognition model (or maybe some pre-trained services like **monkeylearn**.), perhaps with boilerplate code for searching them via those packages?  

Running on CSVs or similar datasets is would probably be a bit harder because the off-the-shelf tools aren&#x27;t as developed, DataONE has a set of curated, annotated [data sets for training models](https://github.com/DataONEorg/semantic-query/tree/master/lib), and was working on it, but I&#x27;m not sure the status of that.
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/52#issuecomment-387451992) on: **5/8/2018**

Great suggestion.  Advice and simple, performant tools just to find the identifiers would be really cool -- too often most tools assume the user already has a pretty good grasp of the landscape and knows what they want.  

An important piece of this puzzle I think are things that can deliver immediate value to the researcher implementing them; or at least a clear value proposition for why to use identifiers.  The lesson idea sounds like an interesting way to go; it could illustrate both how to do a task like adding taxa ids, and demonstrate how that makes your life easier (say, in merging two datasets with differing taxonomy)?
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/52#issuecomment-387454408) on: **5/8/2018**

(On darwin core, @sckott also has WIP https://github.com/ropenscilabs/taxadc)
---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/52#issuecomment-387459654) on: **5/8/2018**

thanks @cboettig - i was just reading this issue. 

wrt &#x60;taxadc&#x60;, that&#x27;s just for taxonomy, to try to make it easy for users to convert https://github.com/ropensci/taxa classes to DWC compliant, and then serialize those objects to XML/JSON/JSON-LD/etc. 

I agree some kind of tool that scans text for entities that might have unique IDs would be great. On the taxonomy front, there&#x27;s i think a global names project tool that goes through and can identify taxonomic names in text. But I don&#x27;t know of tools for other entities that may have identifiers. 

We have at least some tools for identifiers for taxonomy and publications. Are there any major missing things that have identifiers that we don&#x27;t yet have tools for?
---
> from: [**magpiedin**](https://github.com/ropensci/unconf18/issues/52#issuecomment-387508147) on: **5/8/2018**

Thanks for brains!  I will keep fingers crossed for ML proposals, and all for something along the lines of a &quot;how to add/merge taxon id&#x27;s&quot; lesson if it can help elucidate some steps in the meantime (+ compliment other things in the works here/locally/globally). 

@sckott -- two things with id&#x27;s but not tools of their own are (as far as I know?):
1 - Institutional identifiers - [GRBio/GRSciColl](http://grbio.org/content/data-download-grbio) has a registry of &#x27;Cool&#x27; HTTP URIs
2 - Multimedia identifiers - &quot;dcterms:identifier&quot; in a few different standards including Audubon Core

That said, both of those might be a little shaky to develop anything around currently:
- For Institutions, GRBio itself might be too in-flux currently &amp; without an API, but they do have daily-updated dataset-downloads [which are a little oddly-structured and seem to be suspiciously missing the cool-URIs themselves...?].  But they&#x27;re supposedly getting a makeover/takeover from GBIF in the near future...
- For Multimedia, the current GBIF API can return media type, but I don&#x27;t think it can return media identifiers [yet] -- either directly or in association with an occurrence record.
-- Outside of GBIF, MorphoSource.org is one place that&#x27;s starting to serve up Audubon Core datasets [here](https://www.morphosource.org/About/report) 
-- &amp; Outside of biodiversity data, [IIIF](http://iiif.io) might have some good directions to keep an eye on...

...I think I&#x27;m forgetting something, but I&#x27;ll stop there...!
---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/52#issuecomment-388486693) on: **5/11/2018**

related to institutional identifiers, is the Organizational Identifiers group relevant ? https://orcid.org/content/organization-identifier-working-group and https://www.crossref.org/blog/organization-identifier-working-group-update/

&gt; For Institutions, GRBio ... supposedly getting a makeover/takeover from GBIF in the near future...

interesting, would like to learn more about this

Right, i&#x27;ve heard about IIIF, seems great. 

&gt; the current GBIF API can return media type, but I don&#x27;t think it can return media identifiers 

here&#x27;s some GBIF media data, what would the media identifiers be?

&#x60;&#x60;&#x60;
➜  ~ curl &#x27;http://api.gbif.org/v1/occurrence/search?taxonKey&#x3D;1&#x27; | jq &#x27;.results[].media&#x27;
&#x60;&#x60;&#x60;

&#x60;&#x60;&#x60;
[
  {
    &quot;type&quot;: &quot;StillImage&quot;,
    &quot;format&quot;: &quot;image/jpeg&quot;,
    &quot;identifier&quot;: &quot;https://static.inaturalist.org/photos/12648072/original.jpg?1514760468&quot;,
    &quot;references&quot;: &quot;https://www.inaturalist.org/photos/12648072&quot;,
    &quot;created&quot;: &quot;2017-12-31T22:46:43.000+0000&quot;,
    &quot;creator&quot;: &quot;John Flower&quot;,
    &quot;publisher&quot;: &quot;iNaturalist&quot;,
    &quot;license&quot;: &quot;http://creativecommons.org/publicdomain/zero/1.0/&quot;,
    &quot;rightsHolder&quot;: &quot;John Flower&quot;
  },
  {
    &quot;type&quot;: &quot;StillImage&quot;,
    &quot;format&quot;: &quot;image/jpeg&quot;,
    &quot;identifier&quot;: &quot;https://static.inaturalist.org/photos/12648077/original.jpg?1514760475&quot;,
    &quot;references&quot;: &quot;https://www.inaturalist.org/photos/12648077&quot;,
    &quot;created&quot;: &quot;2017-12-31T22:46:43.000+0000&quot;,
    &quot;creator&quot;: &quot;John Flower&quot;,
    &quot;publisher&quot;: &quot;iNaturalist&quot;,
    &quot;license&quot;: &quot;http://creativecommons.org/publicdomain/zero/1.0/&quot;,
    &quot;rightsHolder&quot;: &quot;John Flower&quot;
  }
]
&#x60;&#x60;&#x60;
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/52#issuecomment-388504076) on: **5/11/2018**

Media identifier... i.e., a URI corresponding to the format (mime type?)  Maybe the wikidata identifier is a reasonable choice? https://www.wikidata.org/wiki/Q2195

Funder ids from FundRef are another obvious one.  e.g. https://github.com/ropensci/codemetar/blob/master/inst/extdata/funderNames.csv
---
> from: [**magpiedin**](https://github.com/ropensci/unconf18/issues/52#issuecomment-388627864) on: **5/13/2018**

Nice!  Looks like those are indeed multimedia identifiers in the GBIF data -- staring us in the face at the &quot;identifier&quot; key  :) 

&#x60;&#x60;&#x60;&quot;identifier&quot;: &quot;https://static.inaturalist.org/photos/12648077/original.jpg?1514760475&quot;,&#x60;&#x60;&#x60;

(And my understanding is those media identifiers are supposed to be unique/follow a URI structure, but aren&#x27;t always a resolvable URL -- at least on GBIF and generally in the Audubon Core &#x60;dcterms:identifier&#x60; field)

I hadn&#x27;t been thinking of media format type, but cheers to Wikidata as a reasonable choice, especially as a starting point for less common media formats or things without a main/direct repository to pull from.  (&quot;[JHOVE](http://jhove.openpreservation.org/)&quot; &amp; &quot;[PRONOM](http://www.nationalarchives.gov.uk/aboutapps/PRONOM/tools.htm)&quot; might relate here, but I&#x27;m out of my depth with those)

Good thinking on FundRef, too.  It sounds like ORCID Organization IDs might overlap with FundRef and GRBio/SciColl, but the record data that could be pulled from each might be useful in different situations?  (If that&#x27;s not inviting disambiguation-problems -- &amp; I don&#x27;t think it would?)
---
> from: [**amoeba**](https://github.com/ropensci/unconf18/issues/52#issuecomment-389758394) on: **5/17/2018**

&gt; I believe that @amoeba has worked something similar for DataONE.

More or less, yeah! I&#x27;ve been generally working in this area for a few years along with many other collaborators. I feel like there are two issues that come up a lot:

1. Scientists don&#x27;t know/want to make use of identifiers in their work
2. Scientists who (magically) do want to use identifiers might not be able to find an appropriate one / can&#x27;t easily expand the existing identifier space for their needs

I think (1) is a much larger attack surface at this point and I&#x27;d love to brainstorm ideas. This feels somewhat related to https://github.com/ropensci/unconf18/issues/64 in that part of the research compendia review process might involve annotating code and data with appropriate identifiers (Hey, you might want to put your ORCID over here / annotate this column of this data file with this identifier).
