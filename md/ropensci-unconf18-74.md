# [Providing documentation for the &#x60;asis&#x60; engine](https://github.com/ropensci/unconf18/issues/74)

> state: **open** opened by: **lauracion** on: **5/18/2018**

## Another of the projects that came up while discussing #42 

@jtr13 wrote: &quot;there&#x27;s one small piece of the puzzle that I doubt would be hard to implement and would make a big difference. That is, having an &#x60;echo&#x3D;FALSE&#x60; option for text, to provide the same flexibility for text in progress as we have with code in progress. I can think of so many uses: the ability for example to create assignments with and without solutions (... there are workarounds using comments in code chunks but that&#x27;s not the same).&quot;

### Comments

---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390335828) on: **5/18/2018**

Good idea! 

I recently got something like this to work using another kind of workaround. I was using knitr hooks to hide the results of a chunk until a button is pressed:

&#x60;&#x60;&#x60;r
knitr::knit_hooks$set(
  hide_button &#x3D; function(before, options, envir) {
    if (is.character(options$hide_button)) {
      button_text &#x3D; options$hide_button
    } else {
      button_text &#x3D; &quot;Show solution&quot;
    }
    block_label &lt;- paste0(&quot;hide_button&quot;, options$label)
    if (before) {
      return(paste0(sep &#x3D; &quot;\n&quot;,
                   &#x27;&lt;button class&#x3D;&quot;btn btn-danger&quot; data-toggle&#x3D;&quot;collapse&quot; data-target&#x3D;&quot;#&#x27;, block_label, &#x27;&quot;&gt; &#x27;, button_text, &#x27; &lt;/button&gt;\n&#x27;,
                   &#x27;&lt;div id&#x3D;&quot;&#x27;, block_label, &#x27;&quot; class&#x3D;&quot;collapse&quot;&gt;\n&#x27;))
    } else {
      return(&quot;&lt;/div&gt;&lt;br /&gt;\n&quot;)
    }
  }
}
&#x60;&#x60;&#x60;

Then you can add something like this to the Rmd: 

&#x60;&#x60;&#x60;
&#x60;&#x60;&#x60;{r hide_button &#x3D; &quot;Show Answer&quot;, results &#x3D; &#x27;asis&#x27;, echo &#x3D; FALSE}
cat(
  &quot;The answer.&quot;
)
&#x60;&#x60;&#x27;
&#x60;&#x60;&#x60;

It would be great if I did not have to use &#x60;cat&#x60; and &#x60;results &#x3D; &#x27;asis&#x27;, echo &#x3D; FALSE&#x60;. Perhaps there is / could be a &quot;plain text&quot; chunk type. Perhaps something like:

&#x60;&#x60;&#x60;
&#x60;&#x60;&#x60;{text  echo &#x3D; FALSE}
## Something entirely not thought out

I really would rather people not see this yet.
&#x60;&#x60;&#x27;
&#x60;&#x60;&#x60;

This would also allow for varaibles to determine which parts of the rmd are shown, like:

&#x60;&#x60;&#x60;
&#x60;&#x60;&#x60;{r  include &#x3D; FALSE}
show_in_progress &#x3D; TRUE
&#x60;&#x60;&#x27;

bla bla 

&#x60;&#x60;&#x60;{text  echo &#x3D; show_in_progress}
## Something entirely not thought out

I really would rather people not see this yet.
&#x60;&#x60;&#x27;

&#x60;&#x60;&#x60;
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390336724) on: **5/18/2018**

Adding a knitr engine might work:

https://yihui.name/knitr/demo/engines/
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390337985) on: **5/18/2018**

Oh wait, it already exists, you can use the &#x60;asis&#x60; chunk type to put markdown in chunks and use &#x60;echo &#x3D; FALSE&#x60; to not include them. I just tried it and it works.
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390339232) on: **5/18/2018**

That was a fast resolution! Thank you!
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390342458) on: **5/18/2018**

No problem!
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390344952) on: **5/18/2018**

Thanks... The problem though with &#x60;asis&#x60; is that you still need &#x60;cat()&#x60; which is a pain. In addition, with math equations you have to double escape the tex stuff, which is difficult. (See here:  https://community.rstudio.com/t/echo-false-type-option-for-rmarkdown-text/2384 -- this has been on my mind for a while!)

I have in mind being able to write markdown paragraphs that are included or not, without having to wrap each line in r code.
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390345939) on: **5/18/2018**

I dont think you need &#x60;cat&#x60;. I meant the chunk engine &#x60;asis&#x60;, not  the chunk option &#x60;results &#x3D; &quot;asis&quot;&#x60;. Like so:

&#x60;&#x60;&#x60;

# Show

&#x60;&#x60;&#x60;{asis  echo &#x3D; FALSE}
## Something entirely not thought out

I really would rather people not see this yet.
&#x60;&#x60;&#x27; # (&#x27; instead of &#x60; is for github markdown formatting)

# Dont show

&#x60;&#x60;&#x60;{asis  echo &#x3D; FALSE}
## Something entirely not thought out

I really would rather people not see this yet.
&#x60;&#x60;&#x27;
&#x60;&#x60;&#x60;
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390349841) on: **5/18/2018**

Aha... brilliant! Where can I apply to get back the time I lost on workarounds??? :-) Also, is that documented anywhere? Not here: https://yihui.name/knitr/demo/engines/
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390350251) on: **5/18/2018**

&gt;Where can I apply to get back the time I lost on workarounds???

Haha, there is probably a form you can fill out somewhere. 

&gt; Also, is that documented anywhere?
 
Not that I saw. I had to look through the source code to find it: 

https://github.com/yihui/knitr/blob/dc028f4c9698f84999b53edc5f6f255b29d7e5a2/R/engine.R#L390-L392

---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390350670) on: **5/18/2018**

Ok, so I hereby change this issue to providing documentation for the &#x60;asis&#x60; engine! 
---
> from: [**apreshill**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390355072) on: **5/18/2018**

A related tool I was just made aware of from issue #63 is &#x60;assignr&#x60;: https://github.com/coatless/assignr

I have not used, but looks promising @jtr13!
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/74#issuecomment-390394597) on: **5/19/2018**

Summary: engine &#x60;asis&#x60; in &#x60;knitr&#x60; can be used to easily exclude from the final report chunks of text that are still in progress. &#x60;asis&#x60; needs to be documented.
