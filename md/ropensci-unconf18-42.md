# [Workflow for publications using Rmarkdown with users that won&#x27;t get passed Word/Google docs](https://github.com/ropensci/unconf18/issues/42)

> state: **open** opened by: **lauracion** on: **4/25/2018**

This is a specific issue related to #27 (and somewhat to #22). How to to successfully and painlessly collaborate in a publication workflow using Rmarkdown with researchers (or others) that are not interested at all in getting passed Google docs.

I have no idea how to tackle this. I know this is something I would use *a lot*.

There is some discussion and ideas in this thread: https://twitter.com/CMastication/status/942151771627155457

And a deeper discussion here: https://community.rstudio.com/t/publishing-rmarkdown-to-google-docs/832 where @jennybc says &quot;The problem we ran into is that compiling .Rmd to Google Doc is not that hard. But for the whole workflow to truly be useful, you then want to go the other direction. And that is really hard.&quot; Wondering if this got any easier since last time this was discussed.

FWIW, my 2 cents for the 2018 unconf :slightly_smiling_face:   

### Comments

---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384467358) on: **4/25/2018**

This is maybe a bit off-topic here, but has anyone come up with a way to make the gdoc/work -&gt; RMD conversion work s/t the R sections are retained? This would go for any backwards conversion from a &#x27;final&#x27; document format a non-RMD user might use (TeX, Word, etc). For me, this would really close the collaboration loop for folks who want to edit the text but don&#x27;t care at all about the nuts and bolts of a literate programming/data science document.
---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384501943) on: **4/25/2018**

@jzelner The only practical approach I&#x27;ve found for letting collaborators edit the text in Word is to just paste the raw Rmd into a word document.  Like you say, I&#x27;ve found these collaborators are focused only on the text anyway, and are going to skip over any equations or code, so it doesn&#x27;t matter a jot that equations aren&#x27;t rendered and code isn&#x27;t pretty or highlighted.  

Of course you get a few errors pasting the Word edits back into Rmd (mostly rich-text characters corrupting some ascii code characters) but these are easy to spot and fix with a diff.  I know this is low-tech but relatively robust, I picked this up from a mathematician who works in TeX but also frequently collaborates with Word-only folks.  
---
> from: [**mmulvahill**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384509743) on: **4/26/2018**

The best approach I&#x27;ve found* is using Rmd-&gt;Word &amp; markdown on my end.  I send the Word doc to the collaborator(s) who edit(s) w/ track changes. When I get the edits back, I accept all changes and use pandoc to convert Word to markdown.  I can then diff the two markdown files, resolve changes into my Rmd, build report, commit, and send off a new version as necessary.   Pandoc does a pretty good job of Word-&gt;markdown.   (I haven&#x27;t thought about it until now, but could the word-&gt;md and diff/resolve be built into a pkg and possibly integrate w/ RStudio in a slick way?)

In my consulting biostats work, I&#x27;m never on a project with someone who knows our R/markup/Git toolkit and getting MDs to use anything but Word is a massive endeavor in cultural change.  The other option a colleague tried was requiring collaborators to use the GitHub/GitLab/BitBucket web editor and save via commits.  [This project](https://www.researchgate.net/profile/Egon_L_Van_den_Broek/publication/314102138_HealthInf_2017_Proceedings_of_the_10th_International_Conference_on_Health_Informatics/links/58b59837aca27261e51659ff/HealthInf-2017-Proceedings-of-the-10th-International-Conference-on-Health-Informatics.pdf#page&#x3D;249), though, had an MD/PhD primary investigator who was very motivated to conduct the study with reproducible tools and had the clout to enforce it. 


(this comment may be more #27, but sort of both)
*Edited - a colleague and I started doing this in our RA consulting lab.
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384592933) on: **4/26/2018**

All are great suggestions. I am wondering if we could settle on a very good way to do this. Including both word and google docs as options for interacting with folks not interested in getting involved further.

&gt; could the word-&gt;md and diff/resolve be built into a pkg and possibly integrate w/ RStudio in a slick way?

For example, this :point_up_2:, particularly the integration in RStudio part :wink: 
Having google docs as an starting option would be a nice have too.
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384605858) on: **4/26/2018**

I vaguely remember being told this was all old hat when I shared it on Twitter awhile back, but possibly relevant nonetheless:
[How to convert a Google Doc to RMarkdown and publish on Github pages](http://www.storybench.org/convert-google-doc-rmarkdown-publish-github-pages/)
---
> from: [**Pakillo**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384616380) on: **4/26/2018**

Great thread! A common bottleneck for many, I think.

For some time I thought that using Authorea or Overleaf, which can be easily synced to GitHub (e.g. see [here](https://support.authorea.com/en-us/article/syncing-articles-to-github-zubain/) &amp; [here](https://www.overleaf.com/help/233-how-do-i-connect-an-overleaf-project-with-a-repo-on-github-gitlab-or-bitbucket)) could be a solution: just pull changes from github repo. But then you would have to persuade coauthors to switch platform, which is very hard (even the transition from Word to GDocs).

By now I incorporate changes manually into the Rmd, or use diff/merge of different versions. Now that we are at it, may I ask for a good tool to make diff &amp; merge for manuscripts? I have been using SourceDiffMerge, but it would be great to be able to accept/reject changes word by word, rather than by line or paragraph. Does that tool exist?

Many thanks, and looking forward to seeing what you develop.

P.S. I think the Word -&gt; markdown conversion can be done through rmarkdown::pandoc_convert
---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384633913) on: **4/26/2018**

This is great! To me, the ultimate outcome would be to let someone edit and
use track changes on a Word/GDoc compiled from RMD, and to then be able to
accept changes, convert back to RMD and continue on with the underlying RMD
document. I think this would make collaboration about 100x easier, and also
potentially serve as a kind of &#x27;gateway drug&#x27; to RMD for the Word-addled.

From the bad old days of using Endnote, I remember fields in Word
&lt;https://support.office.com/en-us/article/insert-edit-and-view-fields-in-word-c429bbb0-8669-48a7-bd24-bab6ba6b06bb&gt;.
These may be going the way of the dodo, but it seems like they can be used
to reference potentially dynamic values. For example, if you want to use
Word to make a bunch of envelopes for a big mailing, etc., you can perform
a mail merge using an excel sheet full of addresses and a Word doc with the
underlying formatting. (I recall doing something like this in high school
using a Visual Basic macro...). I wonder if fields could be used to
demarcate inline R output, with the underlying R block in a hidden field or
something like that? Or perhaps have a companion document containing all of
the R chunks? Just thinking this out does make me somewhat queasy because
it feels like it would be brittle, but if there were a consistent way to do
it, I think it could be very powerful.

I think the path forward for TeX is more straightforward.  For example, R
output could be inserted in the document in the form of commands that are
auto-defined in the preamble (see here
&lt;https://tex.stackexchange.com/questions/151367/put-from-external-file&gt;),
or by sourcing from an external file, which I believe is possible without
any non-TeX dependencies. R chunks could just be commented out in the TeX
during conversion and uncommented on the TeX -&gt; Rnw or TeX -&gt; RMD
conversion.

In an ideal world, I think any approach to this would look a bit like the
JSON/html relationship, in which an omnibus external data file is used to
populate dynamic fields in the resulting static document. In this setup,
results in the JSON would be referred to by automatically generated keys in
the document, and the true values would be populated at compile-time. I try
to take this approach when writing papers, but it still leaves me with
external R dependencies to pull the values out of the JSON/Yaml blob.
Perhaps getting all non-TeX languages out of the pipeline for the
&#x27;last-mile&#x27; in a document that can still be reversed to RMD is unrealistic,
but it would be ideal if possible...

-Jon

On Thu, Apr 26, 2018 at 8:04 AM, Francisco Rodriguez-Sanchez &lt;
notifications@github.com&gt; wrote:

&gt; Great thread! A common bottleneck for many, I think.
&gt;
&gt; For some time I thought that using Authorea or Overleaf, which can be
&gt; easily synced to GitHub (e.g. see here
&gt; &lt;https://support.authorea.com/en-us/article/syncing-articles-to-github-zubain/&gt;
&gt; &amp; here
&gt; &lt;https://www.overleaf.com/help/233-how-do-i-connect-an-overleaf-project-with-a-repo-on-github-gitlab-or-bitbucket&gt;
&gt; could be a solution: just pull changes from github repo. But then you would
&gt; have to persuade coauthors to switch platform, which is very hard (even the
&gt; transition from Word to GDocs).
&gt;
&gt; By now I incorporate changes manually into the Rmd, or use diff/merge of
&gt; different versions. Now that we are at it, may I ask for a good tool to
&gt; make diff &amp; merge for manuscripts? I have been using SourceDiffMerge, but
&gt; it would be great to be able to accept/reject changes word by word, rather
&gt; than by line or paragraph. Does that tool exist?
&gt;
&gt; Many thanks, and looking forward to seeing what you develop.
&gt;
&gt; P.S. I think the Word -&gt; markdown conversion can be done through
&gt; rmarkdown::pandoc_convert
&gt;
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub
&gt; &lt;https://github.com/ropensci/unconf18/issues/42#issuecomment-384616380&gt;,
&gt; or mute the thread
&gt; &lt;https://github.com/notifications/unsubscribe-auth/AAIUg9o0KFLjKR6_RCwAoeIGDjIWbcKmks5tsbe-gaJpZM4TkRk2&gt;
&gt; .
&gt;

---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384637268) on: **4/26/2018**

Apologies for the weird HTML links inserted via gmail!
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384696258) on: **4/26/2018**

To play the crotchety veteran, this too (or at least parts of it) has been an Unconf project before 🙂

https://github.com/ropenscilabs/gdoc
---
> from: [**mmulvahill**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384713350) on: **4/26/2018**

I suspected so --  at least that it had at least been thoroughly considered by the R/rOpenSci/Rstudio community.  Curious if there&#x27;s anything specific/narrow here for a smaller post-Unconf project or side-conversation?  I saw somewhere that file diff in the Rstudio text editor has been considered, but that&#x27;s outside our realm.

I&#x27;ve personally tried to come up with a system that allow me to avoid using MS Office/Gdocs as much as possible, and humbly prefer that to digging into VBA/Office internals.  A distant colleague has been developing StatTag -- a Word plugin that reverses our typical workflow (R/SAS/SPSS code goes in the the document and StatTag handles executing/printing it) -- which will work for some folks.
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/42#issuecomment-384714703) on: **4/26/2018**

&gt; at least that it had at least been thoroughly considered by the R/rOpenSci/Rstudio community

And the goal of being able to un-knit is ... on the radar? Discussed? I want to convey that it&#x27;s absolutely A Recognized Thing but also that no one should expect anything on a specific date or even at all. It&#x27;s a very big task.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385284321) on: **4/29/2018**

I started writing a response summarizing my attempts to solve this problem and realized it was becoming essay-length, so I put it here: https://github.com/noamross/rmd-rant . I do think there&#x27;s some space to carve out an unconf-scale project on this issue, possibly along the lines of strategy No. 2 that I describe there.
---
> from: [**njtierney**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385309431) on: **4/30/2018**

On @jennybc &#x27;s note of gdoc - @milesmcbain has a nifty R package for rendering google docs into markdown that could be handy? [markdrive](https://github.com/milesmcbain/markdrive)
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385707179) on: **5/1/2018**

I am super interested in this topic, particularly in terms of advising students on how best to collaborate on projects. While the students are working individually on homework assignments, they&#x27;re all in rmarkdown-lalaland. Then final projects come along and it&#x27;s crash and burn for that model.  They are all coders but yet they will not collaborate on text w/Git/Github; feedback on this approach from one group: &quot;It&#x27;s insane to deal with merge conflicts involving text. No way.&quot; This group switched to Google Docs and then copied and pasted back to Rmd. Quite ironic, since Rmd was supposed to eliminate the copy and paste approach: now we&#x27;ve just flipped the model on its head and copy and paste text instead of code and output (an improvement I suppose but still). 
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385708004) on: **5/1/2018**

One more thought: there&#x27;s one small piece of the puzzle that I doubt would be hard to implement and would make a big difference. That is, having an echo&#x3D;FALSE option for text, to provide the same flexibility for text in progress as we have with code in progress. I can think of so many uses: the ability for example to create assignments with and without solutions. (I know there are workarounds using comments in code chunks but that&#x27;s not the same.)
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385732874) on: **5/1/2018**

Writing prose, collaboratively, with plain text + version control tends to be WAY more difficult than working on code collaboratively.

https://twitter.com/emhrt_/status/740777537547173889

&gt; Writing a multi-author paper on github is a far bigger test of git skills than any coding I&#x27;ve done.
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385735412) on: **5/1/2018**

&gt; This group switched to Google Docs and then copied and pasted back to Rmd. Quite ironic, since Rmd was supposed to eliminate the copy and paste approach

Maybe it&#x27;s fine for them to do collaborative editing of prose as a Google Doc? You could even script the regular task of pulling that file down into the repo (possibly converting to a specific format?) and committing, so that the repo remains the definitive source of the entire project, even though a prose document has been vendored out to Google Docs, due to a more humane user interface for collaborative editing.
---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385738439) on: **5/1/2018**

I do wonder if there&#x27;s a solution to many of these problems that doesn&#x27;t
reinvent too many wheels and is more of a workflow solution. For example, I
try to construct my RMD, at least for manuscripts, so that there is minimal
computation going on in the document. Instead, I try to &#x27;compile&#x27; all of my
results to some kind of external data file. This way, the ultimate target
of all the analysis code is this omnibus data file, rather than the PDF.  When
I&#x27;m feeling extra-organized, it&#x27;s JSON or YAML. When I&#x27;m feeling lazy (i.e.
most of the time), it&#x27;s a bunch of R objects serialized to Rds files and
CSVs.

If you had one omnibus RDS file or JSON/YAML, etc. file, that was the input
to the RMD, you could still allow fields w/in the RMD to update in response
to changing results, etc. And you could even do some computation, e.g. if
whole MCMC traces were stored in the input file.  But the analysis and
writing pipelines would be more-or-less decoupled. I&#x27;m not sure this is a
package-level solution, but something that enforced the mindset of a
database/client or json/html relationship in RMD could make it so that
anyone with a working Rstudio installation could edit and compile and RMD
written this way.

That would solve about 97% of my collaboration problems. It&#x27;s just that
when I try to do it in the ad-hoc way I usually do, I end up breaking the
discipline of keeping everything in one place and introduce little hacks (a
million CSVs w/4 lines each, an RDS with a model object in it) and the
document is no longer truly shareable. I could imagine an rstudio plugin
that shows specific data hooks in the document and connects them to the
input data, etc. Wonder if something like this exists in the web-oriented
world that we could pirate?

-Jon

On Tue, May 1, 2018 at 1:39 PM, Jennifer (Jenny) Bryan &lt;
notifications@github.com&gt; wrote:

&gt; This group switched to Google Docs and then copied and pasted back to Rmd.
&gt; Quite ironic, since Rmd was supposed to eliminate the copy and paste
&gt; approach
&gt;
&gt; Maybe it&#x27;s fine for them to do collaborative editing of prose as a Google
&gt; Doc? You could even script the regular task of pulling that file down into
&gt; the repo (possibly converting to a specific format?) and committing, so
&gt; that the repo remains the definitive source of the entire project, even
&gt; though a prose document has been vendored out to Google Docs, due to a more
&gt; humane user interface for collaborative editing.
&gt;
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub
&gt; &lt;https://github.com/ropensci/unconf18/issues/42#issuecomment-385735412&gt;,
&gt; or mute the thread
&gt; &lt;https://github.com/notifications/unsubscribe-auth/AAIUg5GnMljnbpVHq7qk6B-kEIy0oCmsks5tuJ25gaJpZM4TkRk2&gt;
&gt; .
&gt;

---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385742249) on: **5/1/2018**

&gt; I do wonder if there&#x27;s a solution to many of these problems that doesn&#x27;t
reinvent too many wheels and is more of a workflow solution

Yes, I have definitely counselled students working on group projects to solve this by breaking their report or website up into smaller pieces or pages with an index. This greatly reduces the problem of multiple people touching the same things at the same time.
---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385748143) on: **5/1/2018**

&gt; I do wonder if there&#x27;s a solution to many of these problems that doesn&#x27;t
reinvent too many wheels and is more of a workflow solution. For example, I
try to construct my RMD, at least for manuscripts, so that there is minimal
computation going on in the document. Instead, I try to &#x27;compile&#x27; all of my
results to some kind of external data file. This way, the ultimate target
of all the analysis code is this omnibus data file, rather than the PDF.  When
I&#x27;m feeling extra-organized, it&#x27;s JSON or YAML. When I&#x27;m feeling lazy (i.e.
most of the time), it&#x27;s a bunch of R objects serialized to Rds files and
CSVs.

Sorry if I have been repeating myself too much, but [&#x60;drake&#x60;](https://github.com/ropensci/drake) was designed to accommodate this use case. The user specifies a declarative workflow with intermediate data objects and files, R Markdown reports included. Here, a dynamic report is just a target in the workflow rather than the overarching workflow manager (minimal computational burden on &#x60;knitr&#x60;), and there are ways to tell &#x60;drake&#x60; about the dependencies of each report. Example: https://ropensci.github.io/drake/articles/drake.html. As @ldecicco-USGS pointed out in #30, things get tougher once we try to integrate with Google Drive / Google Docs.
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385752703) on: **5/1/2018**

@jennybc I don&#x27;t have a problem with Google Docs, at least until the tools get better. I haven&#x27;t done an ethnography of how students work, but I hypothesize that they need different tools than seasoned researchers who can divvy up the work more readily (you do the abstract, I&#x27;ll write up the methods...) Many are out of their comfort zone writing. They struggle together with how to write each piece of a report and then put the pieces together.  All that to say that some of them at least are truly working together on each sentence and derive a great deal of benefit from the Google Docs platform.
---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385783918) on: **5/1/2018**

Hi Will,

Thanks! I think drake is definitely a big part of the solution here
(currently trying to wean myself off of Makefiles towards drake to ease
collaboration with those are are not so-inclined). Although I do still
think that last step of how to construct the input data, what format it
should be in, what goes into it and what doesn&#x27;t, etc. remains to be worked
out. This may be something of a standards issue, and would be something I&#x27;d
love to chat about more at the unconf or whenever/wherever else!

-Jon

On Tue, May 1, 2018 at 2:25 PM, Will Landau &lt;notifications@github.com&gt;
wrote:

&gt; I do wonder if there&#x27;s a solution to many of these problems that doesn&#x27;t
&gt; reinvent too many wheels and is more of a workflow solution. For example, I
&gt; try to construct my RMD, at least for manuscripts, so that there is minimal
&gt; computation going on in the document. Instead, I try to &#x27;compile&#x27; all of my
&gt; results to some kind of external data file. This way, the ultimate target
&gt; of all the analysis code is this omnibus data file, rather than the PDF.
&gt; When
&gt; I&#x27;m feeling extra-organized, it&#x27;s JSON or YAML. When I&#x27;m feeling lazy (i.e.
&gt; most of the time), it&#x27;s a bunch of R objects serialized to Rds files and
&gt; CSVs.
&gt;
&gt; Sorry if I have been repeating myself too much, but drake
&gt; &lt;https://github.com/ropensci/drake&gt; was designed to accommodate this use
&gt; case. The user specifies a declarative workflow with intermediate data
&gt; objects and files, R Markdown reports included. Here, a dynamic report is
&gt; just a target in the workflow rather than the overarching workflow manager
&gt; (minimal computational burden on knitr), and there are ways to tell drake
&gt; about the dependencies of each report. Example:
&gt; https://ropensci.github.io/drake/articles/drake.html. As @ldecicco-USGS
&gt; &lt;https://github.com/ldecicco-USGS&gt; pointed out in #30
&gt; &lt;https://github.com/ropensci/unconf18/issues/30&gt;, things get tougher once
&gt; we try to integrate with Google Drive / Google Docs.
&gt;
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub
&gt; &lt;https://github.com/ropensci/unconf18/issues/42#issuecomment-385748143&gt;,
&gt; or mute the thread
&gt; &lt;https://github.com/notifications/unsubscribe-auth/AAIUgwlaQNjdlLlA50rJp5tvdQXPk0hXks5tuKiDgaJpZM4TkRk2&gt;
&gt; .
&gt;

---
> from: [**wlandau**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385855795) on: **5/1/2018**

Sure! Basically, that data frame is like a Makefile, your recipes are R code chunks, and you declare dependencies just by using them in the recipes. I am happy to receive questions as [new issues](https://github.com/ropensci/drake/issues), especially since they help build up the [FAQ](https://ropensci.github.io/drake/articles/faq.html).
---
> from: [**jzelner**](https://github.com/ropensci/unconf18/issues/42#issuecomment-385968901) on: **5/2/2018**

Here&#x27;s what I&#x27;m envisioning. This would work for most of my collaboration
headaches, but I don&#x27;t know how many other folks&#x27; problems it would solve:

1) Compile to a zipfile or other archive, with a) an RDS file containing
all of the R objects needed in the course of generating the final
PDF/HTML/MD document, b) a directory of binary or text files (e.g. figures,
csv files), c) a requirements.txt style manifest listing both what is in
the archive and any R dependencies.

2) At document-generation time, the archive is mounted and accessed without
expanding it into the filesystem, and executed like a normal RMD.

Most of my collaborators are willing to install (or have installed) RStudio
and are comfortable using the GUI tools to generate a PDF from an RMD. But
they may be a bit more reticent about the filesystem, and almost all will
be using windows, whereas most of my stuff is coming from Linux.

This might be a package kind of solution, particularly if there are tools
needed to grease the process of making an archive and for enforcing a
standard archive structure that is transportable across projects. It also
might be useful to think about a &#x27;tidy data&#x27; style paper? I would be
excited to spearhead something like that. My gut feeling is that the
solution here is 90% practice and 10% technology, maybe 80/20?

-Jon



On Tue, May 1, 2018 at 11:37 PM, Will Landau &lt;notifications@github.com&gt;
wrote:

&gt; Sure! Basically, that data frame is like a Makefile, your recipes are R
&gt; code chunks, and you declare dependencies just by using them in the
&gt; recipes. I am happy to receive questions as new issues
&gt; &lt;https://github.com/ropensci/drake/issues&gt;, especially since they help
&gt; build up the FAQ &lt;https://ropensci.github.io/drake/articles/faq.html&gt;.
&gt;
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub
&gt; &lt;https://github.com/ropensci/unconf18/issues/42#issuecomment-385855795&gt;,
&gt; or mute the thread
&gt; &lt;https://github.com/notifications/unsubscribe-auth/AAIUg7QTPOzR25eilcxiyjHSh1QeClZJks5tuSoVgaJpZM4TkRk2&gt;
&gt; .
&gt;

---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/42#issuecomment-387569634) on: **5/8/2018**

Wow, such a great discussion is happening here. Thank you, everyone! I lost track of this until @stefaniebutland made me noticed the discussion was far from over. There is a lot to digest here for me. I will try to come back to it in the upcoming days before the unconf and see if I can summarize all the directions proposed for this issue thus far so we can choose which direction may be worth tackling in Seattle.
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/42#issuecomment-388027297) on: **5/10/2018**

There&#x27;s a pre-emptive unconf-y-thing happening as I write that overlaps somewhat with this issue: the [eLife Innovation Sprint](https://elifesciences.org/events/c40798c3/elife-innovation-sprint-2018) aiming

&gt; to collaboratively prototype new innovations that bring cutting-edge technology to open research communication.

The outputs of that will be well-worth keeping an eye on, and feeding back into this issue, and potentially the broader unconf in general.
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/42#issuecomment-388975356) on: **5/14/2018**

Ok, folks, initial step before getting to @noamross summary request. I summarize the items I see could conduct to unconf projects*:

1. Develop further @noamross [strategy 2 ](https://github.com/noamross/rmd-rant#strategy-2-having-collaborators-provide-input-text-only)

2. Add &#x60;echo &#x3D; FALSE&#x60; for text in progress, a nice-have feature suggested by @jtr13  

3. @jzelner&#x27;s package approach for users who are willing to collaborate using RStudio: 

&gt; 1) Compile to a zipfile or other archive, with a) an RDS file containing
all of the R objects needed in the course of generating the final
PDF/HTML/MD document, b) a directory of binary or text files (e.g. figures,
csv files), c) a requirements.txt style manifest listing both what is in
the archive and any R dependencies.

&gt; 2) At document-generation time, the archive is mounted and accessed without
expanding it into the filesystem, and executed like a normal RMD.

I can open new issues for 1) and 2) (but Noam and Joyce may be better authors for those issues than I - please let me know your preference).

I can&#x27;t open a new issue for 3) because I don&#x27;t follow the idea completely :grimacing:. Could you please do the honors, Jon?
 
\*  I am omitting workflow descriptions posted not because they lack interest, but &#x27;cause I don&#x27;t see a project there - if you see a project from something I am omitting, please open an issue with it :pray:
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/42#issuecomment-390334824) on: **5/18/2018**

Summary: All projects I identified from the discussion for this issue are now summarized in #73, #74, and #75.
