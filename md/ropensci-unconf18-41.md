# [Lesson/Examples of how to clean &#x27;field&#x27; data](https://github.com/ropensci/unconf18/issues/41)

> state: **open** opened by: **aurielfournier** on: **4/25/2018**

This might be too field ecology specific, but I think it could be useful more broadly. 

This is a situation I ran into in my grad school work, and I know many others who are doing field work where they are collecting data hard copy, and then entering it every few days over several months of work run into. 

There are data entry errors, spellings, issues, etc, plus you also end up with dozens of files that have been entered, probably my different people, etc. 

I dealt with this in my own field work by creating a script I ran over all the files, checked them for the correct spelling of different things, and then printed out the things that were wrong. 

This code is not my finest, but it got me through my phd. 

Maybe something that does this better already exists, and I just need to learn what it is so I can point others with this issue towards it. 

But if it doesn&#x27;t, this would be something I&#x27;d love to work on building. 

I realize this functionality already exists in open refine, but I personally don&#x27;t care for open refine, so I did it this way. 



&#x60;&#x60;&#x60;file_names &lt;- list.files(pattern&#x3D;&quot;.csv&quot;)

# these are the vectors of values that I am ok with, with the correct spellings

# areas are my study areas
areas &lt;- c(&quot;nvca&quot;,&quot;scnwr&quot;,&quot;fgca&quot;,&quot;slnwr&quot;,&quot;tsca&quot;,&quot;bkca&quot;,&quot;ccnwr&quot;,&quot;dcca&quot;,&quot;osca&quot;,&quot;tmpca&quot;)

# impound is my wetland impoundments
impound &lt;- c(&quot;rail&quot;,&quot;sanctuary&quot;,&quot;ash&quot;,&quot;scmsu2&quot;,&quot;scmsu3&quot;,&quot;sgd&quot;,&quot;sgb&quot;,&quot;pool2&quot;,&quot;pool2w&quot;,&quot;pool3w&quot;,&quot;m11&quot;,&quot;m10&quot;,&quot;m13&quot;,&quot;ts2a&quot;,&quot;ts4a&quot;,&quot;ts6a&quot;,&quot;ts8a&quot;,&quot;kt9&quot;,&quot;kt2&quot;,&quot;kt5&quot;,&quot;kt6&quot;,&quot;ccmsu1&quot;,&quot;ccmsu2&quot;,&quot;ccmsu12&quot;,&quot;dc14&quot;,&quot;dc18&quot;,&quot;dc20&quot;,&quot;dc22&quot;,&quot;os21&quot;,&quot;os23&quot;,&quot;pooli&quot;,&quot;poole&quot;,&quot;poolc&quot;)

# regions are the four regions
regions &lt;- c(&quot;nw&quot;,&quot;nc&quot;,&quot;ne&quot;,&quot;se&quot;)

# plant spellings that are correct 
plant &lt;- c(&quot;reed canary grass&quot;,&quot;primrose&quot;,&quot;millet&quot;,&quot;bulrush&quot;,&quot;partridge pea&quot;,&quot;spikerush&quot;,&quot;a smartweed&quot;,&quot;p smartweed&quot;,&quot;willow&quot;,&quot;tree&quot;,&quot;buttonbush&quot;,&quot;arrowhead&quot;,&quot;river bulrush&quot;,&quot;biden&quot;,&quot;upland&quot;,&quot;cocklebur&quot;,&quot;lotus&quot;,&quot;grass&quot;,&quot;cattail&quot;,&quot;prairie cord grass&quot;,&quot;plantain&quot;,&quot;sedge&quot;,&quot;sesbania&quot;,&quot;typha&quot;,&quot;corn&quot;,&quot;sumpweed&quot;,&quot;toothcup&quot;,&quot;frogfruit&quot;,&quot;canola&quot;,&quot;sedge&quot;,&quot;crop&quot;,&quot;rush&quot;,&quot;goldenrod&quot;,NA)

for(i in 1:length(file_names)){
  int &lt;-  read.csv(file_names[i])
# so this prints out instances where three are things that are not part of the lists above and includes the file name so I can go and find the issue.   
  print(paste0(int[(int$region %in% regions&#x3D;&#x3D;FALSE),]$region,&quot; &quot;,file_names[i],&quot; region&quot;))
  print(paste0(int[(int$area %in% areas&#x3D;&#x3D;FALSE),]$area,&quot; &quot;,file_names[i],&quot; area&quot;))
  print(paste0(int[(int$impound %in% impound&#x3D;&#x3D;FALSE),]$impound,&quot; &quot;,file_names[i],&quot; impound&quot;))
  print(paste0(int[(int$plant1 %in% plant&#x3D;&#x3D;FALSE),]$plant1,&quot; &quot;,file_names[i],&quot; plant1&quot;))
  print(paste0(int[(int$plant2 %in% plant&#x3D;&#x3D;FALSE),]$plant2,&quot; &quot;,file_names[i],&quot; plant2&quot;))
  print(paste0(int[(int$plant3 %in% plant&#x3D;&#x3D;FALSE),]$plant3,&quot; &quot;,file_names[i],&quot; plant3&quot;))
}

## once I resolve all of the issues identified from above I then read in all the files, put them in a list and I can stitch them together into one master file. 

vegsheets &lt;- list()

for(i in 1:length(file_names)){
  vegsheets[[i]] &lt;- read.csv(file_names[i])
}

## this takes the list and combines it all together into one data frame
masterdat &lt;- do.call(rbind, vegsheets)

# write it out into a master file
write.csv(masterdat, &quot;~/Github/data/2015_veg_master.csv&quot;, row.names&#x3D;FALSE)&#x60;&#x60;&#x60;

### Comments

---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/41#issuecomment-384394506) on: **4/25/2018**

I have many of these, and they all require something a little different, but the tool I use most is [**assertr**](https://github.com/ropensci/assertr)
---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/41#issuecomment-384423607) on: **4/25/2018**

I think this is actually a pretty broad problem, at least in epidemiology. For example, if you&#x27;re using data from a hospital-based reporting system, the fields in the raw data may change over time, or based on the person doing the query for you,and there are ample opportunities for this to wreak havoc.

Not sure if existing tools are adequate to cover these issues or not, although I think a broader problem is getting people responsible for these kinds of data to 1) pay attention to these issues and 2) take the time to use the tools!
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/41#issuecomment-384511340) on: **4/26/2018**

I like the idea of structuring &quot;Lessons&quot; @aurielfournier  

Reg. &#x60;assertr&#x60; is there a way to automatically write the commands based on a table with allowed values? Or based on say EML metadata?

The list of tips could also feature https://github.com/ChrisMuir/refinr 
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/41#issuecomment-384535859) on: **4/26/2018**

I concur with @jzelner on the broadness of the issue. It confronts me constantly via the [&#x60;bikedata&#x60; package](https://github.com/ropensci/bikedata), where different cities generally use their own data formats, and often inconsistently. I&#x27;ve recently adapted the whole thing to a dictionary-style lookup table of possible column names, but this is just at a first-cut stage. It is nevertheless pure C/C++, so I&#x27;d be keen to converse, listen, input on nice ways of interfacing R and C++ in this regard.
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/41#issuecomment-384749573) on: **4/26/2018**

I think this is great topic, and a tricky one.  I think the current situation involves both shortcomings of tooling and shortcomings of outreach, and I agree that one-size-fits-all solutions like OpenRefine only go so far -- like many tools in this space, it can feel both overbearing and not smart enough at the same time.

I definitely believe that &quot;Standards&quot; are a key part of finding happiness here, but they can also be a part of the problem.  Dates are a good trivial example: sure, python and ruby have libraries that can reliably parse &quot;Tuesday after Christmas 2012&quot; into a date, but I think we can all agree that dates are suddenly much easier to work with if [we all just use ISO-8601](https://xkcd.com/1179/).  

In ecology/evolution, we have similar solution for the whole problem of working with species name issues, (spelling, formatting, different higher taxonomy definitions, etc) by using taxonomic identifiers, but afik these have had very little penetration among anyone who actually sees their critters in the field, and very much suffers from [problem #927](https://xkcd.com/927/). 

Ideally, good tooling would pay us immediate dividends for using standards.  e.g. I think that&#x27;s the case with dates, there&#x27;s an immediate benefit in being able to date-time math etc this way (instead of, say, having separate columns for day, month, and year; which is still too common).  but for others like taxon ids, there&#x27;s no obvious benefit.  Spatial descriptions are somewhat in-between -- if you already do spatial analysis you already use spatial standards, but for the rest of us it&#x27;s easy to feel like you need a master&#x27;s in GIS before that would be useful, so we just name our regions and sites with convenient labels and get on with it.  Tooling that made it easier rather than harder to describe our somewhat standard data in a standard way could, IMHO, make a big difference.  But I think we still have too few examples of these tools that are easy enough and modular enough to quickly integrate into field-data-collection workflow.  Would love to join a brainstorm on this and bounce some of my no doubt hopelessly idealistic ideas off others!

 
---
> from: [**magpiedin**](https://github.com/ropensci/unconf18/issues/41#issuecomment-386900227) on: **5/6/2018**

Keen to hear more on this, too!  Ditto the need for more examples of tools &amp; standards &quot;outreach&quot; -- at the overall dataset-structure/schema-level, too.

Maelle, were you picturing something like being able to point &#x60;assertr&#x60; at an EML schema &amp;/or other standards/vocabs, e.g.:
- [EML 2.1.1](https://github.com/ropensci/EML/tree/master/inst/xsd/eml-2.1.1) (...in the handy [ropensci/EML](https://github.com/ropensci/EML) package)
- [Darwin Core](https://github.com/tdwg/dwc/blob/master/standard/documents/xml/tdwg_dwcterms.xsd)

[RDA&#x27;s list](http://rd-alliance.github.io/metadata-directory/standards/) of data standards defined in XML/RDF could be another resource to include if it helps generalize this example to other fields/domains that have their own formally-defined/under-used data standards--if that&#x27;s not wandering out of scope here.  (&amp; either way, ra for hopeless idealism! :)



---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/41#issuecomment-387299151) on: **5/8/2018**

@magpiedin yes I was imagining a wrapper that&#x27;d take your raw-ish data and an EML as arguments and output the discrepancies. I don&#x27;t know other metadata standards well enough 😉 Btw for EML creation there&#x27;s also the WIP https://github.com/cboettig/eml2 by @cboettig 
---
> from: [**magpiedin**](https://github.com/ropensci/unconf18/issues/41#issuecomment-387502800) on: **5/8/2018**

There&#x27;s a version 2 in the works, you say?  This makes my day :)

I threw in Darwin Core here on the off-chance that the field scenario @aurielfournier has in mind includes any species observation/occurrence data (e.g., inventorying wildlife in a particular area?).  If it&#x27;s a more experimental/other scenario, though, all ears, too.
---
> from: [**aurielfournier**](https://github.com/ropensci/unconf18/issues/41#issuecomment-387548153) on: **5/8/2018**

Sorry for dropping out for a bit. Just finally had time to look over the resources everyone tagged in here. 

&#x60;assertr&#x60; is fantastic, thank you for pointing thatout @noamross 

I am not super familiar with EML, but I need to get up to speed on it for some work related things, and from what i know of EML, having some kind of wrapper like @maelle described that takes raw data and EML and tells you what doesn&#x27;t match could be really exciting, especially since it could help more people actually keep meta data (a big issue in ecology). My &#x27;concern&#x27; there would be that EML might not be the best one to choose if we thought the problem was broader then &#x27;just&#x27; ecology. 

@magpiedin for the example I gave originally, I was talking about species occurrence data, in my dissertation, though I think in ecology the issue is certainly present beyond species occurrence data and would also apply to experimental and other data types. 

I&#x27;d be really interested in pursuing this as either an idea about developing lessons around an already exisiting tool, like &#x60;assertr&#x60;, or building something new on top that would bring in meta data. Both would be hugely helpful for the problem I had in grad school, and I think to many folks more broadly 


---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/41#issuecomment-387617069) on: **5/9/2018**

@aurielfournier I&#x27;ve used (and learnt about) EML for an epidemiology research project, and could document everything that had to be documented, no term was missing in EML standard. But I guess other fields that have other metadata standards (epidemiology doesn&#x27;t), could be more problematic? But a minimal tool EML+ &#x60;EML&#x60;/&#x60;eml2&#x60;+&#x60;assertr&#x60; could be useful as a starting point (and could be developed further for other metadata standards)?
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/41#issuecomment-387655768) on: **5/9/2018**

Maybe useful for testing such an EML+&#x60;assertr&#x60; tool
https://github.com/DeclareDesign/fabricatr
https://github.com/ropensci/charlatan
