# [Toward a general-purpose API response data tidier](https://github.com/ropensci/unconf18/issues/24)

> state: **open** opened by: **aedobbyn** on: **4/14/2018**

I think the goal for the unconf would be to lay the foundation for an eventual package that is meant to sit in a user’s pipeline directly after a &#x60;jsonlite::fromJSON()&#x60; call, in place of initial bespoke munging of the nested list. The package would:

- Tidy the nested list output into a tibble with one nested row per input
    - Will be a best guess at how the user wants data formatted; at worst it should be easier to work with than the raw output
- Allow for recursively filling &#x60;.empty&#x60; values at each level of the list (i.e., convert empty elements and &#x60;NULL&#x60;s to &#x60;NA&#x60;s or a user-defined value) so the tibble can be easily unnested
- Include special handling for the most commonly used APIs so we know we’re getting these right (?)

The first step here (which is the goal for the unconf -- many thanks to @jennybc for working through the initial idea with me) seems to me to be defining patters in 1) API requests and their resulting responses and 2) in the most common/successful strategies people use in their tidying process. I think it would be useful to query a few more-or-less representative RESTful APIs and note the commonalities in the solutions for tidying them. The idea would be to extract the intersection of these solutions into general-purpose verbs and also to identify where these approaches fail.

I could see this package being useful not just for one-off data grabbing and tidying jobs but also for developing packages that interface with an arbitrary API. Could of course be used on any nested list, but I think it makes sense to keep the scope of the package focused to API data.

For a name, I’m thinking **&#x60;roomba&#x60;**[^1] but definitely not married to it. 

[^1]: Provided that’s cool with the relevant trademark attorneys :satisfied:

### Comments

---
> from: [**jimhester**](https://github.com/ropensci/unconf18/issues/24#issuecomment-385214632) on: **4/28/2018**

The [GitNub graphQL API](https://developer.github.com/v4) is one common source of these wonderfully nested lists, likely any graphQL based API would produce similar nested outputs. 

I have found the data pretty cumbersome to work with as nested lists, so definitely think this is an area where additional tooling or a different data representation like you describe would help.
---
> from: [**aedobbyn**](https://github.com/ropensci/unconf18/issues/24#issuecomment-385219721) on: **4/28/2018**

Awesome thanks for pointing to that @jimhester!
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/24#issuecomment-385226265) on: **4/29/2018**

This sounds fantastic, I&#x27;m definitely interested in strategies for working with these deeply nested lists.  @sckott , @maelle and I have recently been playing with &#x60;jq&#x60; in this context; e.g. https://ropensci.org/blog/2018/04/26/rectangling-onboarding/.  &#x60;jq&#x60; is cool and all but I think it would be great to have a more native R interface for doing these kind of queries (analogous to &#x60;dplyr&#x60; instead of SQL).  

I&#x27;m also curious about other query strategies for deeply nested JSON (i.e. other than jq).  I&#x27;ve found some cool thinks can be done using the functions from @jeroen&#x27;s &#x60;jsonld&#x60; package, and have also played around using SPARQL to do graph queries on JSON files (eg https://ropensci.github.io/rdflib/articles/rdf_intro.html).  Again both of these approaches help do things that can be cumbersome with &#x60;purrr&#x60; alone but could use some nicer interfaces I think.  SPARQL queries can be tricky to write (at least for me, I struggle with pure SQL queries too), but the nice thing is the return type is essentially always a &#x60;data.frame&#x60;, so no additional rectangling needed once you know how to ask for what you want.

I&#x27;ve also been meaning to dive more into @hrbrmstr&#x27;s excellent little book, https://github.com/hrbrmstr/drill-sergeant-rstats,  on using Apache Drill from R to query large numbers of deeply nested JSON files.  

Both the SPARQL and Drill approaches can optionally communicate over ODBC protocols, which should make some interesting potential for integration with &#x60;dplyr&#x60; / &#x60;dbplyr&#x60; and the great work folks at RStudio have been doing with database connections.  Not really sure what is possible in that regard but would love to explore more.  
---
> from: [**jimhester**](https://github.com/ropensci/unconf18/issues/24#issuecomment-385377461) on: **4/30/2018**

Agreed, it would be great to have something you wouldn&#x27;t need to learn a new DSL for, particularly because there doesn&#x27;t seem to be one consensus standard DSL used to query JSON like there is for XML (XQuery).
---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/24#issuecomment-388490138) on: **5/11/2018**

Its possible we could build something on top of &#x60;jqr&#x60; - since it is very fast, and jeroen is working on streaming, so it could be used for those large data problems as well.  I think we could build in operations like replacing empty/NULL values with NA, and similar nasty problems with nested data. 
---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/24#issuecomment-388496706) on: **5/11/2018**

I like the &#x60;jqr&#x60; suggestion (Drill, et. al. is a pretty heavyweight dep), esp if we build filters / filter helpers (I&#x27;m not really a fan of the syntax b/c it messes with my own mental model of how it ought to work but that&#x27;s not really a big issue and it&#x27;s a great tool).
---
> from: [**aedobbyn**](https://github.com/ropensci/unconf18/issues/24#issuecomment-388525499) on: **5/11/2018**

Building something on top of &#x60;jqr&#x60; sounds useful, rather than doing all of the munging in an R object. Even if we only get so far as sniffing out and &#x60;NA&#x60;ifying &#x60;NULL&#x60;s and making it easier to flatten nested data in a way that usually makes sense, I think that&#x27;s a win.

+1 for abstracting away potentially multiple DSLs for querying JSON.

@hrbrmstr I don&#x27;t know anything about Drill but fwiw the Preface of your book is fantastic.
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/24#issuecomment-388570068) on: **5/12/2018**

Agree with all of the above!  @sckott and @aedobbyn both identify the nuisance of &#x60;empty&#x60;, and I agree with @hrbrmstr &#x27;s observation that the syntax isn&#x27;t super intuitive.  Would be nice to have a more &#x60;dplyr&#x60;-esque DSL, e.g. something more like


&#x60;&#x60;&#x60;r
jsonblob %&gt;% filter(repo.owner.name &#x3D;&#x3D; &quot;hrbrmstr&quot;)
&#x60;&#x60;&#x60;

Maybe it&#x27;s already obvious, but just wanted to note that I think this would provide a nice way to query R lists in general (since there&#x27;s a pretty tight JSON&lt;-&gt;list mapping); such an interface isn&#x27;t specific to just data already in JSON or just REST APIs.  

---
> from: [**aedobbyn**](https://github.com/ropensci/unconf18/issues/24#issuecomment-388587503) on: **5/12/2018**

Exactly!
  
Originally I&#x27;d been thinking of this at the level of something that&#x27;s already an R object but riddled with empty vectors etc. so workflow would look like 

&#x60;&#x60;&#x60;
jsonblob %&gt;% 
  jsonlite::fromJSON() %&gt;% 
  roomba::clean()
&#x60;&#x60;&#x60;

or something to that effect. But if doing the &#x60;clean&#x60;ing or the &#x60;filter&#x60;ing or whtever it may be on the &#x60;jsonblob&#x60; itself makes more sense then I&#x27;m all for that.

I still think a useful first step will be in identifying common patterns and stumbling blocks in nested structures like API response objects and constructing techniques for cleaning them in ways that are safe make sense in the majority of cases.

And totally agreed @cboettig I think we can tackle a lot of nasty nested list cases for free by addressing the API data specifically. (Maybe it&#x27;s also worth identifying other common list annoyances that don&#x27;t manifest in API response data, though.)
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390306993) on: **5/18/2018**

Just spitballing a bit further on this.  Not sure how common this case is for others, but often there&#x27;s a JSON object/blob with some pattern I understand and want to extract without having to make explicit references to just how deep it is buried.  For instance, something like the example below:

&#x60;&#x60;&#x60;
{
&quot;stuff&quot;: [{
               &quot;buried&quot;: [
                               &quot;deep&quot;: [
                                             {
                                              &quot;goodstuff&quot;: &quot;here&quot;,
                                              &quot;name&quot;: &quot;Bob Rudis&quot;,
                                              &quot;secret_power&quot;: ..., 
                                             },
                                             {
                                              &quot;goodstuff&quot;: &quot;here&quot;,
                                              &quot;name&quot;: &quot;Amanda Dobbyn&quot;,
                                              &quot;secret_power&quot;: ..., 
                                              &quot;more_nested_stuff&quot;: { ... }
                                             },
   
                                             ]
                                ]
              },
              {
               ...
              }
              ]

}
&#x60;&#x60;&#x60;

Maybe I just want the value of the &#x60;name&#x60;s of anything found in JSON objects that also contain the key-value pair &#x60;&quot;goodstuff&quot;: &quot;here&quot;&#x60;.  More generally, I&#x27;d like to just jump to that point in the &quot;graph&quot; and navigate from there, e.g. maybe I want to go up to the parent object and get some additional property, etc.  

Maybe this can be done in &#x60;JQ&#x60; already, but it&#x27;s not intuitive to me how to express it.  (particularly if I want to start &quot;walking the graph&quot; from that point without specifying just how I descended down to that node... My ideal interface would let me have some notion of variables, and let me return all matches to the requested variables in columns  of a &#x60;data.frame&#x60;.


(Not sure if the above is at all helpful as illustration, but will bring some real examples of highly nested json blobs I struggle with for fodder for an API design)

---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390332059) on: **5/18/2018**

that made me think of something fairly obscure: &quot;GraphGrep&quot; (https://cs.nyu.edu/shasha/papers/graphgrep/icpr2002.pdf) and a thing that kinda built on it &quot;Closure Trees&quot; (https://www.cs.ucsb.edu/~dbl/papers/he_icde_2006.pdf). It does require building a graph and index but for sufficiently large structures it might be worth it. For smaller ones that index build time might be small enough. @yonicd has been layering in some recursion on tidyverse bits but we cld also likely scaffold a query language on to &#x60;rapply()&#x60; if &#x60;jq&#x60; cannot do it.
---
> from: [**sckott**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390336292) on: **5/18/2018**

just having a play @cboettig with your eg above cleaned up:

&#x60;&#x60;&#x60;r
x &lt;- &#x27;{
&quot;stuff&quot;: {
   &quot;buried&quot;: {
      &quot;deep&quot;: [
       {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Bob Rudis&quot;,
        &quot;secret_power&quot;: 5
       },
       {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Amanda Dobbyn&quot;,
        &quot;secret_power&quot;: 4, 
        &quot;more_nested_stuff&quot;: 4
        }
      ],
      &quot;alsodeep&quot;: 2342423234,
      &quot;deeper&quot;: {
        &quot;foo&quot;: [
          {
            &quot;goodstuff&quot;: 5,
            &quot;name&quot;: &quot;barb&quot;
          }
        ]
      }
    }
}}&#x27;
&#x60;&#x60;&#x60;

&#x60;&#x60;&#x60;r
jqr::jq(x, &#x27;recurse(.[]?) | objects | select(has(&quot;goodstuff&quot;))&#x27;)
[
    {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Bob Rudis&quot;,
        &quot;secret_power&quot;: 5
    },
    {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Amanda Dobbyn&quot;,
        &quot;secret_power&quot;: 4,
        &quot;more_nested_stuff&quot;: 4
    },
    {
        &quot;goodstuff&quot;: 5,
        &quot;name&quot;: &quot;barb&quot;
    }
]
&#x60;&#x60;&#x60;

the jq command &#x60;&#x27;recurse(.[]?) | objects | select(has(&quot;goodstuff&quot;))&#x27;&#x60; is clearly not something we&#x27;d want a end user to have to deal with, but could be hidden under some nicer syntax 😼 
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390353046) on: **5/18/2018**

Thanks @sckott , that&#x27;s awesome ✨ .  And thanks for getting us to a reproducible example.  

Minor question first: that matches all blobs with the property &#x60;goodstuff&#x60;, it would be nice to match conditionally, so we only get the blob if &#x60;&quot;goodstuff&quot;: &quot;here&quot;&#x60;, (i.e. &#x60;barb&#x60; should not be included).

One thing that I struggle with in JQ is that it&#x27;s not clear how to walk up and down the graph though -- imagine I want the number from the &#x60;alsodeep&#x60; field as an &#x60;id&#x60; for everything in that blob?  And maybe I also want to descend deeper from the &#x60;goodstuff&#x60; and pull out some other element, like &#x60;more_nested_stuff.b&#x60; (if &#x60;more_nested_stuff&#x60; actually had more nesting in it, as in  my [modified toy example](https://gist.github.com/cboettig/e8a0947ced5224cd468af941dda002c6#file-ex-json).  

The syntax is super awkward, but it&#x27;s possible to do this kind conditional filter and walking with SPARQL variables.  The query: 

&#x60;&#x60;&#x60;r
q &lt;- &#x27;
PREFIX x: &lt;x:&gt;
SELECT ?name, ?power ?b ?id
WHERE { 
  ?object x:goodstuff &quot;here&quot; .
  ?object x:name ?name .
  OPTIONAL { ?object x:secret_power      ?power } .
  OPTIONAL { ?object x:more_nested_stuff ?y .
             ?y      x:b                 ?b} .
  OPTIONAL {
             ?parent x:deep ?object .
             ?parent x:alsodeep ?id
  }
}&#x27;
rdf_query(blob, q)
&#x60;&#x60;&#x60;

Returns a nice compact &#x60;tibble&#x60; containing only the columns named in &#x60;SELECT&#x60;.   (note that anything proceeded by a &#x60;?&#x60; is a variable, and we can call it wahtever we want.  Note that variables can be used to indicate the object (&#x60;?object&#x60;, &#x60;?parent&#x60;, the key (not shown), or the value &#x60;?power&#x60;, &#x60;?id&#x60;, &#x60;?y&#x60;)

&#x60;&#x60;&#x60;
# A tibble: 3 x 4
  name          power     b          id
  &lt;chr&gt;         &lt;int&gt; &lt;int&gt;       &lt;dbl&gt;
1 scott            NA    NA         NA 
2 Amanda Dobbyn     4     2 2342423234.
3 Bob Rudis         5    NA 2342423234.
&#x60;&#x60;&#x60;

Note that &#x60;barb&#x60; is absent (because she doesn&#x27;t have &#x60;&quot;goodstuff&quot;: &quot;here&quot;&#x60;, and &#x60;scott&#x60; is included.  Dropping the &#x60;OPTIONAL&#x60; bits would cause rows missing those elements to be omitted.  

I know the SPARQL syntax is basically 💩 (particularly with the ugly prefix stuff), but it is perhaps amenable to being broken down into a &#x60;dplyr&#x60; like syntax in much the way &#x60;dplyr&#x60; already does for SQL?  I&#x27;m not sure that we really want to use &#x60;rdflib&#x60;, but I am intrigued by the ability to walk the graph with variables and select and filter with SQL like statements...


---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390354034) on: **5/18/2018**

(p.s. meant to include reproducible code link as [gist](https://gist.github.com/cboettig/e8a0947ced5224cd468af941dda002c6))
---
> from: [**jimhester**](https://github.com/ropensci/unconf18/issues/24#issuecomment-390406859) on: **5/19/2018**

Alternatively we could just use R to walk the list, in [tidyversedashboard](https://github.com/jimhester/tidyversedashboard/blob/5e22668d80d7ab15efe237a2dfd961472ec06141/R/issue_progress.R#L10-L27) I wrote a simple function to do a depth first search of a nested list returning the index of the first location that matched a predicate function. Extending this to return indexes of all the matches rather than only the first would solve this problem, here is the example with the current implementation which returns only the first match.

&#x60;&#x60;&#x60; r
dfs_idx &lt;- function(x, f) {
  res &lt;- integer()
  walk &lt;- function(x, depth) {
    for (i in seq_along(x)) {
      if (isTRUE(tryCatch(f(x[[i]]), error &#x3D; function(e) FALSE))) {
        res[[depth]] &lt;&lt;- i
        return(TRUE)
      } else {
        if (is.list(x[[i]]) &amp;&amp; isTRUE(walk(x[[i]], depth + 1))) {
          res[[depth]] &lt;&lt;- i
          return(TRUE)
        }
      }
    }
  }
  walk(x, 1)
  res
}

x &lt;- jsonlite::fromJSON(&#x27;{
&quot;stuff&quot;: {
   &quot;buried&quot;: {
      &quot;deep&quot;: [
       {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Bob Rudis&quot;,
        &quot;secret_power&quot;: 5
       },
       {
        &quot;goodstuff&quot;: &quot;here&quot;,
        &quot;name&quot;: &quot;Amanda Dobbyn&quot;,
        &quot;secret_power&quot;: 4, 
        &quot;more_nested_stuff&quot;: 4
        }
      ],
      &quot;alsodeep&quot;: 2342423234,
      &quot;deeper&quot;: {
        &quot;foo&quot;: [
          {
            &quot;goodstuff&quot;: 5,
            &quot;name&quot;: &quot;barb&quot;
          }
        ]
      }
    }
  }
}&#x27;, simplifyVector &#x3D; FALSE)

x[[dfs_idx(x, function(x) { x$goodstuff &#x3D;&#x3D; &quot;here&quot; })]]$name
#&gt; [1] &quot;Bob Rudis&quot;
&#x60;&#x60;&#x60;

Created on 2018-05-19 by the [reprex package](http://reprex.tidyverse.org) (v0.2.0).


