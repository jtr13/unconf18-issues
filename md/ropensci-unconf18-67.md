# [packrat: ease the use of external libraries](https://github.com/ropensci/unconf18/issues/67)

> state: **open** opened by: **czeildi** on: **5/16/2018**

First case: a team collaborates on a project w &#x60;packrat&#x60; and one of the team members would like to use a package not closely related to the project like &#x60;colorout&#x60;. Afaik you can add this package as external package but then it would be required as external package for all project members. You can work around this by manipulating .Rprofile files but it is quite cumbersome.

Second case: There are some &quot;meta&quot; packages which do not necessarily have place as project dependencies like &#x60;usethis&#x60;, &#x60;lintr&#x60;, &#x60;goodpractice&#x60;, &#x60;covr&#x60;, &#x60;pkgdown&#x60; etc. I take advantage of these packages in almost all of my project but I do not necessarily want to add them as dependencies. I can use &#x60;packrat::with_extlib&#x60; but I run into the issue that it is not enough to specify the main package like &#x60;pkgdown&#x60; but also all their dependencies not present in my project which varies and makes it somewhat cumbersome to use. I think we could automate this.

&#x60;&#x60;&#x60;r
packrat::with_extlib(c(&quot;pkgdown&quot;, &quot;rstudioapi&quot;, &quot;highlight&quot;, &quot;debugme&quot;, &quot;callr&quot;, &quot;rematch&quot;), build_site())
&#x60;&#x60;&#x60;

tagging @kevinushey as the developer of &#x60;packrat&#x60; - what do you think? Is there already solution I missed? 

### Comments

---
> from: [**kevinushey**](https://github.com/ropensci/unconf18/issues/67#issuecomment-389597774) on: **5/16/2018**

I&#x27;d be open to discussing a better solution here. I think &#x60;packrat::with_extlib()&#x60; is not really the best solution here; there is likely something a little more ergonomic we could do.

I wonder if the simplest solution might be the right solution -- just provide some simple mechanism for putting the user library on the library search path, so that &#x60;library(pkgdown)&#x60; can find &#x60;pkgdown&#x60; in the user library even if not installed in the Packrat private library.

There&#x27;s also &#x60;packrat::opts$external.packages()&#x60;, which is a &#x27;smarter&#x27; version of the above where we attempt to symlink user packages into &#x60;packrat/lib-ext&#x60;, which we do always put on the library search path.
