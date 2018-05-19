# [Tools and guidance on basic dataset metadata standards, files and formats.](https://github.com/ropensci/unconf18/issues/72)

> state: **open** opened by: **annakrystalli** on: **5/18/2018**

As a results of teaching Research Data Management to first year primarily biology and ecology PhD students using R for the passed 4 yrs, I’ve been thinking a lot about metadata. In particular what the most basic level we teach students should be and what sort of files and formats to use. 

I tried to teach them to create Ecological Metadata Language objects ([EML](http://www.dcc.ac.uk/resources/metadata-standards/eml-ecological-metadata-language)) using pkg [&#x60;eml2&#x60;](https://github.com/cboettig/eml2) last year but I wouldn’t consider my attempt successful. It seemed too much for them at this point in their studies and not critical enough to spend more of the limited time we had together on it.

But what I’ve tried to do since and feel I wanted them to ultimately get out of the session was to learn to prepare metadata files that are:
- Easy to produce and understand right from the start
- Useful in analyses
- Have good API to more complex metadata storage frameworks (ie through [&#x60;csvy&#x60;](https://github.com/leeper/csvy), &#x60;eml2&#x60; etc) that they can get to grips with further down the line, as and when it’s required.

So I’ve been thinking about R functionality that could help with both the task of creating said basic files and establishing best metadata management practice. Some of the features I’ve envisaged would help guide or semi-/automate some of the requirements identified in [rOpenSci Analysis Best Practice Guidelines](https://docs.google.com/document/d/1OYcWJUk-MiM2C1TIHB1Rn6rXoF5fHwRX-7_C12Blx8g/edit#heading&#x3D;h.dyoxrtoo15mm) as still being human powered, eg.  
- Know your data (list of variables described, visualise your data, data dictionary, data format)
- Description of root dataset (s) 
- Informative titles/labels 

I made a start putting some useful functionality together in nascent package [&#x60;metadatar&#x60;](https://github.com/annakrystalli/metadatar) (see draft README for quick demo of some of the functions) that I used successfully for teaching.  The main function creates a metadata table for a given dataset, with a row for each column of the original dataset.  The basic metadata fields are based on the EML attribute table and the function tries to automatically populate some of the fields but the rest need to be entered manually still. However, it would be great if this stage could be integrated with the excellent suggestions in issue #52 and perhaps through #68? (I need to get my head round CEDAR a bit more to understand how this might fit in).

To show students how keeping good metadata about variables can be useful in analyses, there’s also a function to extract more informative variable descriptions and units for plotting and presenting results in tables from the metadata table.

Would love to hear other people’s thoughts on this and their own current and ideal approaches to these issues and perhaps even work on developing some more tools for this during the unconf. It feels like a topic that could perhaps be integrated with issue #52?

## Summary of proposal

- Discuss and define what the minimum metadata standard should be and the objects/file formats they should be compiled and stored in.
- Consider what the best way to make such information available during analyses (ie as attributes of a data.frame/tibble?).
- Further develop functionality to help researchers/analysts produce such files.
- Link to tools that can help with ontologies (eg #52)
- Define a context that could be used to link the basic fields in the metadata table to  basic fields in different standards? 


### Comments

---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/72#issuecomment-390262795) on: **5/18/2018**

This sounds great!  Might also have tie-ins to #41 ?

To throw a bit more into the mix, I think Google&#x27;s [Dataset](https://developers.google.com/search/docs/data-types/dataset) description would be worth some exploring too, both because &#x27;hey, if Google supports it, that could definitely help with discovery&#x27; and also because I think it&#x27;s a pretty light-weight / user-friendly approach (says my sample size of &#x60;n&#x3D;1&#x60;).  

@sckott and I have tossed around the idea of using this to get a better picture of exactly what datasets rOpenSci packages can access, e.g. [movebank example](https://search.google.com/structured-data/testing-tool/u/0/#url&#x3D;https%3A%2F%2Fgithub.com%2Fcboettig%2Fmovebank%2Fraw%2Fmaster%2Finst%2Fextdata%2Fdatasauce.json), [GBIF](https://search.google.com/structured-data/testing-tool/u/0/#url&#x3D;https%3A%2F%2Fraw.githubusercontent.com%2Fropensci%2Frgbif%2Fmaster%2Finst%2Fextdata%2Fdata.json).  

I think it would be nice to think of a prototype package that could help generate the basic bits (i.e. bibliographic info, spatial &amp; temporal coverage of the data, data type), and also help you quickly and easily *do something* cool with that metadata (i.e. search interface, indicate the region on a map, period in time, etc).  I think getting immediate value to the researcher back out is an important missing piece of metadata descriptions; adding metadata often feels both way too painful and too altruistic.  

A nice feature of Google&#x27;s Dataset description is that it&#x27;s JSON, so basically equivalent to an R list object already, but since it&#x27;s all in the https://schema.org context, we get links to ontologies &quot;for free&quot; (such as the W3C&#x27;s [DCAT](https://www.w3.org/TR/vocab-dcat/)) because these maps are already built in OWL in the schema.org definitions.  Other cases one would have to map more &#x27;manually&#x27; but that might be easier anyway!  We have some very sketchy outlines for working with Schema.org in https://github.com/ropenscilabs/datasauce
