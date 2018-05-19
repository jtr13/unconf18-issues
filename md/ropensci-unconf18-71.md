# [Open Source Qualitative Coding Tool](https://github.com/ropensci/unconf18/issues/71)

> state: **open** opened by: **bduckles** on: **5/17/2018**

I would love to see a lightweight, non GUI, open source qualitative coding tool. I know that RQDA exists, but I’ve never gotten it to work and it appears it hasn’t been updated since 2012. I could be missing something (please tell me if I am!) but I rarely have seen anything that is open source, uses R and actually works to help with coding.

There are a myriad of text coding tools out there, many of which are quite sophisticated and complex (NVIVO, Atlas TI, MAX QDA). None of these are open source, all of them cost a lot of money. For most of what people need when doing basic qualitative analysis, this can be like bringing an industrial grade shredder when all you need is a paring knife. I’ve started using the mac program Annotations to do basic, small scale coding projects. It’s kind of a GUI paring knife. Cons: It&#x27;s only available for macs and is not being further developed, it’s not open source and it’s a GUI. 

I’d love to see something where the data analysis is more reproducible and open source. Can we please just make an open source paring knife for qualitative coding?

Most of what folks need when doing qual research is a way to highlight text and code it. There are complicated things you can do with those codes, there’s the issue of concatenated codes or multiple codes and there are more things to worry about once you have the codes etc. But if we had a straightforward way to yank quotes out of a text file, code them and then dump all of that into a dataset, I suspect people would happily use it so that they don’t have to shell out $$$ for a an industrial grade coding tool to do a simple text analysis project.  

One idea would be to use some form of markdown-like syntax to use with text files that would indicate the coding of quotes within the text. Then an R package would pull out the quotes with the codes attached and create a dataset from a text file, possibly also with the text file name as a variable. It’d be simple, it wouldn’t do all the things one might *want* but it would be a starting place. This is just an idea, I’d love more ideas/advice/thoughts on how to manage something like this. 

Also, IANA developer. I’m a noob R coder, but I do love mixed methods and R and know a lot of folks who would love to find a solution.    

### Comments

---
> from: [**stefaniebutland**](https://github.com/ropensci/unconf18/issues/71#issuecomment-389927157) on: **5/17/2018**

@bduckles a) love that you&#x27;re bringing qualitative research in here; b) so that others can better understand your idea, could you explain briefly what qualitative coding is? The word &quot;coding&quot; has a specific meaning to R folk that is different from what I think you mean. Maybe even modify the issue title?

Could you link to an example - not necessarily an academic paper - that illustrates an application of qualitative coding? Goal of this is to get people to understand the value of what you are proposing.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/71#issuecomment-389931628) on: **5/17/2018**

Big fan of this - we do a bunch of qualitative coding on both scientific literature and semi-structured interviews.  We work with MAXQDA but its outputs don&#x27;t fit super easily into an R analysis pipeline. 

The PDF highlighting workflow from the [tabulizer](https://github.com/ropensci/tabulizer) might be something to build off of - it&#x27;s an R-linked GUI for selecting tables in a PDF to convert to tabular data in R.  
---
> from: [**bduckles**](https://github.com/ropensci/unconf18/issues/71#issuecomment-389933956) on: **5/17/2018**

Yes! Thank you @stefaniebutland, let me see if I can do a bit of explaining - I realize the word coding is a problem in this, but really, this is what Qual researchers call it. I&#x27;d have to think about how best to talk about it in a world where R folks use the word coding. Maybe I&#x27;ll use the word QualCodes to distinguish in this description? 

A decent overview would be [this Saldana chapter](https://www.sagepub.com/sites/default/files/upm-binaries/24614_01_Saldana_Ch_01.pdf). Don&#x27;t get too bogged down with the details of how she does it as there are a variety of schools of thoughts on how to do it. But I&#x27;ve taken a screenshot from the chapter that I think illustrates what coding for Qual researchers is:
&lt;img width&#x3D;&quot;495&quot; alt&#x3D;&quot;screen shot 2018-05-17 at 10 32 30 am&quot; src&#x3D;&quot;https://user-images.githubusercontent.com/6986662/40191073-a2670fc2-59bd-11e8-98c2-bfc466c12a42.png&quot;&gt;

On the left is text (think of this as any textual qualitative data e.g. interview transcripts, field notes or notes you write up about your experiences in the field, documents written by people you are studying) on the right the researcher has come up with QualCodes which in this case are one word descriptions of how to categorize the quote on the left. 

Creating these Qual Codes is an iterative process for a qualitative researcher. They will often change, lump together, split or re organize these QualCodes as they go through more and more data. Depending on the type of QualCoding you do and the process you&#x27;re using there are a variety of ways to do this and schools of thought in terms of how to do it. As a starting place I don&#x27;t think we need to be too opinionated for a simple tool. Later on we could get more sophisticated but a simple tool would just let the researcher assign QualCodes and let the quotes be sorted with them, perhaps turning the quotes, codes and filenames into a dataset. Most researchers will also write a codebook or research notes for each QualCode that describes what they refer to. That may or may not be a part of this tool. I think it would be useful regardless. 
 
The biggest problem comes when there is a quote that fits into multiple QualCodes, or one subsection of a piece of text is evidence for a QualCode, but the longer quote is helpful for a different QualCode. Maybe there&#x27;s an elegant solution for this, or maybe not. I still think a very simple tool for using a text based interface to assign codes and turn that into data would be REALLY useful. 

I&#x27;ll think more about how I might explain the problem more succinctly. 
---
> from: [**dsholler**](https://github.com/ropensci/unconf18/issues/71#issuecomment-389987143) on: **5/17/2018**

I&#x27;ve been looking around for solutions to this very problem, so I&#x27;m glad you raised the issue here! I&#x27;m trained in using Atlas.ti, which is not bad, but comes with a ton of issues that you&#x27;ve laid out nicely (the big one being that it is proprietary). I&#x27;m probably going to end up repeating some of what Beth said, but here are my two cents:

To add a bit about one of the processes for QDA, particularly Strauss &amp; Corbin/Miles &amp; Huberman&#x27;s approaches, it can be thought of as layering interpretation onto the text. You start with open coding, meaning that you&#x27;re free to tag snippets of text with whatever descriptions you want. For instance, if I&#x27;m coding observation notes and I think conversations between two individuals will be relevant to my research questions, I&#x27;ll tag the instances in which the two individuals speak with &quot;A-B conversation.&quot; In the next round of coding, I might classify what they discuss with a finer tag, like &quot;A-B conversation - package maintenance.&quot; In another round, I might get even more specific with something like &quot;A-B conversation - package maintenance - no money to pay people.&quot; Later rounds involve conflating codes that might mean the same thing, relating codes to one another (often by documenting their meanings in a similar way to software documentation), and eliminating codes that no longer make sense. 

Sometimes we&#x27;ll also do some theoretical coding, where you look for instances that demonstrate some concept or mechanism from the academic literature on the subject. That&#x27;s more common toward the end of the process in my field (organization studies/management/whatever the heck I do), but is prominent as an approach from the beginning in fields with experimental or clinical roots (e.g., psychology).

The utility of using software for this is that you can nest codes, then begin to see the number of instances of a particular code you&#x27;ve applied. Maybe more importantly, you can see where codes co-occur (i.e., where multiple codes have been applied to the same snippets of text), and other linking kinds of things that help you see what&#x27;s thematic and what&#x27;s not. So I agree with Beth - we all need something very, very simple that doesn&#x27;t cost a million dollars. It would be nice, of course, to be able to visualize codes and the relationships between them in new and innovative ways, but for the most part the process is very simple and every qualitative researcher I&#x27;ve talked to desires a simple tool. Some even use Endnote things like that because, as Beth said, lightweight is best (especially for smaller projects). 
---
> from: [**dsholler**](https://github.com/ropensci/unconf18/issues/71#issuecomment-389995848) on: **5/17/2018**

I&#x27;ll also add - GUI would be very helpful from my end, and definitely for broader adoption as well. 
---
> from: [**bduckles**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390012374) on: **5/17/2018**

Thanks for your thoughts @dsholler, I&#x27;m really looking forward to a continued conversation on this topic and so glad I&#x27;m not alone with this problem! It&#x27;s helpful to hear how you think about qual coding process and agree with the layering interpretation. 

Honestly I think the simple tools are the most beneficial. Folks end up defaulting to printing things out and using sticky notes and folder because they can&#x27;t find a tool that actually works for them and doesnt cost a ton of money. Something simple would maybe not solve ALL the problems, but if it did what it was supposed to do elegantly and in a lightweight way, it&#x27;d be helpful for folks just trying to do some basic analysis. 

I&#x27;d say the reason that I don&#x27;t love GUI&#x27;s is that I find myself wanting keyboard shortcuts for the actual coding. I personally find a lot of clicking to be challenging to my wrists and I wonder about the reproducibility as changes are made. That said, I&#x27;m open if you think a GUI interface would be more effective and beneficial for the long term adoption. The primary thing for me would be something that actually works and is open source.   
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390019976) on: **5/17/2018**

As a veteran of hundreds of hours of NVivo…literally at least 200 interviews which I also had to transcribe (yay, undergrad-ness), I can definitely say that this&#x27;d be awesome!
---
> from: [**bduckles**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390059699) on: **5/17/2018**

Chatting with my brother about the idea he suggested we look at  https://web.hypothes.is/ and their code here: https://github.com/hypothesis/h 

He thought maybe this tool could offer a foundation for the solution. He says &quot;So you could imagine a way that your browser opens with a file, you annotate, then you have a coded dataset spit back into R.&quot; That would mean we&#x27;d need a JS developer, but it might be a way forward. 
---
> from: [**itcarroll**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390084561) on: **5/17/2018**

I built a relevant Shiny app for some workshoppers at [SESYNC](https://www.sesync.org), who were gearing up to do some mixed methods research. It&#x27;s a &quot;lightweight&quot; GUI to help with coding text scraped from a Wordpress blog. Feel free to &#x60;shiny::runGitHub(&#x27;ShAQDAS&#x27;, &#x27;itcarroll&#x27;)&#x60; and poke around at [itcarroll/ShAQDAS](https://github.com/itcarroll/ShAQDAS).

Thanks to Fellow @khondula for pointing me to this thread, motivating the push to GitHub.
---
> from: [**zachary-foster**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390347217) on: **5/18/2018**

I have never heard of qualitative coding before, but it sounds interesting!

 I found something that might help with making a shiny GUI that can select text and assign codes from https://stackoverflow.com/questions/42274461/can-shiny-recognise-text-selection-with-mouse-highlighted-text:

&#x60;&#x60;&#x60;r
library(shiny)

text1 &lt;- &quot;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce nec quam ut tortor interdum pulvinar id vitae magna. Curabitur commodo consequat arcu et lacinia. Proin at diam vitae lectus dignissim auctor nec dictum lectus. Fusce venenatis eros congue velit feugiat, ac aliquam ipsum gravida. Cras bibendum malesuada est in tempus. Suspendisse tincidunt, nisi non finibus consequat, ex nisl condimentum orci, et dignissim neque est vitae nulla.&quot; 
text2 &lt;- &quot;Aliquam ut purus neque. Maecenas justo orci, semper eget purus eu, aliquet molestie mi. Duis convallis ut erat at faucibus. Quisque malesuada ante elementum, tempor felis et, faucibus orci. Praesent iaculis nisi lorem, non faucibus neque suscipit eu. Ut porttitor risus eu convallis tristique. Integer ac mauris a ex maximus consequat eget non felis. Pellentesque quis sem aliquet, feugiat ligula vel, convallis sapien. Ut suscipit nulla leo&quot;
highlight &lt;- &#x27;
                function getSelectionText() {
var text &#x3D; &quot;&quot;;
if (window.getSelection) {
text &#x3D; window.getSelection().toString();
} else if (document.selection) {
text &#x3D; document.selection.createRange().text;
}
return text;
}

document.onmouseup &#x3D; document.onkeyup &#x3D; document.onselectionchange &#x3D; function() {
var selection &#x3D; getSelectionText();
Shiny.onInputChange(&quot;mydata&quot;, selection);
};
&#x27;

coded_text &lt;- character(0)

ui &lt;- bootstrapPage(
  tags$script(highlight),
  fluidRow(
    column(4,
           tags$h1(&quot;Text to code&quot;),
           tags$h2(&quot;From table&quot;),
           tableOutput(&quot;table&quot;),
           tags$h2(&quot;From raw text&quot;),
           verbatimTextOutput(&quot;text&quot;)
    ),
    column(4,
           tags$h1(&quot;Coding options&quot;),
           actionButton(&quot;code1&quot;, &quot;Assign selected text to Code1&quot;),
           tags$h1(&quot;Code1 output&quot;),
           verbatimTextOutput(&quot;selected_text&quot;)
    )
  )
)


server &lt;- function(input, output) {
  output$table &lt;- renderTable({
    data.frame(paragraph &#x3D; 1:2, text &#x3D; c(text1, text2))
  })

  output$text &lt;- renderText(paste(text1, text2))

  coded &lt;- eventReactive(input$code1, {
    coded_text &lt;&lt;- c(coded_text, input$mydata)
    coded_text
  })

  output$selected_text &lt;- renderPrint({
    coded()
  })

}

shinyApp(ui &#x3D; ui, server &#x3D; server)
&#x60;&#x60;&#x60;

@itcarroll, looks good! I did see on your repo:

&gt; Highlighting would be nice; any idea how to implement?

Would the above trick help with that?

---
> from: [**itcarroll**](https://github.com/ropensci/unconf18/issues/71#issuecomment-390350138) on: **5/18/2018**

@zachary-foster Glad you got it working :)

For me, the question about highlighting is more about how to store the data on what&#x27;s selected. Do you input a &#x60;&lt;span&gt;&#x60; element into the text? Do you store starting and ending character positions? Both have drawbacks.
