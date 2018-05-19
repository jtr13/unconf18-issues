# [Color coded errors/warnings/messages/printed text](https://github.com/ropensci/unconf18/issues/61)

> state: **open** opened by: **czeildi** on: **5/15/2018**

By default errors, warnings and messages are all printed red in R which can be confusing as red usually means something wrong but a message can be just informative. I think it would be nice to provide an easy way to create colored messages, like by default red for error, yellow for warning, blue for friendly information etc. With the **crayon** package this should not be too difficult.

I am thinking about a way that maybe the end-user should be able to control this, or the creator of the package. We could distinguish style further based on the class of the condition.

### Comments

---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/61#issuecomment-389230677) on: **5/15/2018**

Fun idea.

Packages like &#x60;usethis&#x60; have implemented this for many of their printed outputs:

https://github.com/r-lib/usethis/blob/bb191e95ef1b0e3aa304e7267d1d968975414450/R/style.R#L11-L13

Off the top of my head I can&#x27;t quite think of a way that you could modify errors, warnings and message other than &#x60;tryCatch&#x60; which seems a little awkward. Probably a better way though.

I do really love coloured output though and I do think it is worth the effort. 


---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/61#issuecomment-389287848) on: **5/15/2018**

It&#x27;s all just standard ANSI colour codes. Even &#x60;crayon&#x60; is nothing other than simple pre- and post-pending the appropriate codes:
&#x60;&#x60;&#x60;
&gt; col_green &lt;- &quot;\033[32m\033[47m&quot; # 32m &#x3D; yellow; 47m &#x3D; white background
&gt; col_blue &lt;- &quot;\033[34m\033[1m\033[43m&quot; # 34m &#x3D; blue; 1m &#x3D; bold; 43m &#x3D; Yellow BG
&gt; col0 &lt;- &quot;\033[22m\033[39m\033[49m&quot; # 22m &#x3D; normal weight; 49m &#x3D; normal BG
&gt; message (col_green, &quot;blah&quot;, col0)
&gt; warning (col_blue, &quot;blah&quot;, col0)
&#x60;&#x60;&#x60;
Probably best not to mess with &#x60;message&#x60; and &#x60;warning&#x60;, but &#x60;col_message(&quot;my message&quot;, &quot;blue&quot;)&#x60; would do it.
---
> from: [**czeildi**](https://github.com/ropensci/unconf18/issues/61#issuecomment-389498131) on: **5/16/2018**

@boshek thanks for the usethis reference. I can imagine a bright future for a package focusing solely on formatting messages and maybe use that in &#x60;usethis&#x60; as well. @jennybc what do you think? Especially since the style guide for error messages in the [tidyverse style guide].(http://style.tidyverse.org/error-messages.html)

@mpadge yes, maybe this would be a tiny package but I see value in tiny single purpose packages. And I can imagine that even if you have one core function like &#x60;col_message&#x60; we could create shortcuts for errors, warnings etc to encourage a unified formatting

From a development perspective I can see a way to do the formatting when creating the error/warning etc. But if possible I would welcome an option for maybe globally setting style on the user side like &#x60;option(warning_color &#x3D; &quot;yellow&quot;)&#x60; that could effect even errors thrown by base R code. Again, I do not know whether this is technically possible.
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/61#issuecomment-389546638) on: **5/16/2018**

&gt; @jennybc what do you think? Especially since the style guide for error messages in the [tidyverse style guide](http://style.tidyverse.org/error-messages.html)

Yes we do have a &quot;todo&quot; to extract the whole [style.R](https://github.com/r-lib/usethis/blob/master/R/style.R) file from usethis and, probably, put it in a package to facilitate making consistent user interfaces that meet the style guide. There have been multiple requests to export those functions from usethis, but we&#x27;ve declined, because we don&#x27;t want packages to depend on usethis for that functionality.

Something I&#x27;ve been meaning to write down but have not is a map between, say, a function in [style.R](https://github.com/r-lib/usethis/blob/master/R/style.R) and identifiable concepts. As in, &quot;always apply this style to a path and that style when referring to an argument name and this other style for a string ...&quot;. I think, right now, you have to use common sense or look around at usage elsewhere in the package, which is slow and inconsistent.
---
> from: [**jimhester**](https://github.com/ropensci/unconf18/issues/61#issuecomment-389865320) on: **5/17/2018**

The long term plans for color styling in the tidyverse is to use [cli](https://github.com/r-lib/cli) to style the outputs, which would allow us to define a default style, but would also allow users to define a custom style that would automatically be used throughout our packages.

Also there are a few RStudio IDE issues related to automatically coloring messages / warnings / errors in red https://github.com/rstudio/rstudio/issues/2733, https://github.com/rstudio/rstudio/issues/2574, so at least there this behavior will likely change in the future.
---
> from: [**lcolladotor**](https://github.com/ropensci/unconf18/issues/61#issuecomment-390375996) on: **5/18/2018**

Hi. I&#x27;m just curious if you&#x27;ve checked https://github.com/jalvesaq/colorout and if whether this solves part of the problem you describe. 
