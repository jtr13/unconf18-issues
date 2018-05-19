# [Collaborating with NOT-users of R, RStudio, or Git](https://github.com/ropensci/unconf18/issues/27)

> state: **open** opened by: **maurolepore** on: **4/17/2018**

(For more on RStudio, Git and GitHub see #22.)

In my experience, valuable collaborators often stay out of the collaboration loop that happens on GitHub.  Not only I miss their input but also I struggle to integrate the contributions they make outside my GitHub-based workflow. They may not want to learn complex tools and have little motivation (often they are already at the peak of their academic careers).  

* What is a good workflow to collaborate with those who don&#x27;t use R, Rstudio or Git (but might use e.g. Google sheets and GitHub)?
* How can we maximize their input?
* How can we minimize the problems caused by contributions outside the GitHub workflow?




### Comments

---
> from: [**ldecicco-USGS**](https://github.com/ropensci/unconf18/issues/27#issuecomment-382511428) on: **4/18/2018**

(unfortunately) I have a decent amount of experience on this. I think the best thing to do captured in #22 ...basically...figure out why we are having a hard time getting people using git and fix that.  As my understanding, comfort, and overall dependency of git has increased over the years...so has my dedication for getting others on-board with using git. And...each time I&#x27;ve made a &quot;convert&quot; to git, it&#x27;s been easier and easier.

As for non-R users...the tools do exist to take their input from Google Sheets/Google Drive and incorporate it in your R workflow. You lose the version control, but &#x60;googlesheets&#x60; and &#x60;googledrive&#x60; have helped immensely. 

All that being said, I&#x27;d love to hear more of this conversation.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/27#issuecomment-383294420) on: **4/21/2018**

&gt; I think the best thing to do captured in #22 ...basically...figure out why we are having a hard time getting people using git and fix that.

-- @ldecicco-USGS 

I&#x27;m totally with you and #22 , in trying to help those who choose learn Git and friends. The main challenge I suggest in this issue has less to do with technical aspects and more with whatever drives humans to accept or reject change. 

Although [I&#x27;m interested in this aspect of human behavoiour](https://github.com/ropensci/unconf18/issues/13#issuecomment-382182444), I accept that some people will simply choose to not use the workflow I like (GitHub and friends). To deal with this, I appreciate you suggest googlesheets and googledrive, and I would love to hear as many ideas as possible and summarize them, maybe on a blog, as a kind of &#x27;Manual for happy collaboration with non-R/GitHub users&#x27;.



---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/27#issuecomment-385285516) on: **4/29/2018**

 I&#x27;m more enamored by browser-based tools that require _zero install and zero signup_.  I have had some moderate success with using [hypothes.is](https://web.hypothes.is/) to get input in the form of comments on Rmd outputs, but it can also trip people up who are unfamiliar, isn&#x27;t optimal for private repos, does require a sign-up. I wish it could use another service such as Google for sign-up so people didn&#x27;t have the barrier of creating new accounts.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/27#issuecomment-385287840) on: **4/29/2018**

&gt; I have had some moderate success with using hypothes.is to get input in the form of comments on Rmd outputs

Wow, I didn&#x27;t know about this. It may not be perfect now but it seems like a great step forward. Thanks for sharing!
---
> from: [**AmeliaMN**](https://github.com/ropensci/unconf18/issues/27#issuecomment-385515320) on: **4/30/2018**

This is related to an issue I know a lot of educators have (e.g. @mine-cetinkaya-rundel, @beanumber, @rudeboybert, myself, etc). If we ask students to submit R work for courses, how do we provide feedback to them? If they submit &#x60;Rmd&#x60;s, we can insert comments and send back, but annotating HTML pages is hard. Nothing approaches the annotation in, say, Word. (I&#x27;ll try hypothes.is, thanks @noamross!). I think Mine has students submit via PR and provides comments through GitHub somehow, but for intro classes that&#x27;s not very reasonable. 
---
> from: [**mine-cetinkaya-rundel**](https://github.com/ropensci/unconf18/issues/27#issuecomment-385576548) on: **4/30/2018**

Yup, I do use GitHub issues and/or PR comments, but that&#x27;s for a course where learning Git/GitHub is part of the learning objectives. I would hesitate to bring Git into the mix only for the sake of submission.

One possible solution is Rmd -&gt; Google Docs, but then that&#x27;s where the reproducibility cycle ends and it&#x27;s not that different from Rmd -&gt; Word.
---
> from: [**jenniferthompson**](https://github.com/ropensci/unconf18/issues/27#issuecomment-389296945) on: **5/15/2018**

I&#x27;m late to this party, but am interested in this conversation! As someone who is typically not &quot;in charge&quot; on my group&#x27;s projects (in my case, I&#x27;m not the first or senior author), I don&#x27;t contribute most of the text; my work gets inserted into documents at least half written (and usually started by) other people. I would l-o-v-e a better system than sending Word versions back and forth (though we have at least upgraded to Box version control lately). But with clinical collaborators, I&#x27;m skeptical about something as technically involved as Github being part of the general solution. Some kind of middle ground would be a huge step for us. Google Docs has tons of potential for our manuscripts, but our group is so tied to reference management systems that work with Word and not GDocs that I&#x27;ve hesitated to even bring it up for clinical papers. (If anyone has a solution to _that_, I&#x27;m all ears!)

And thanks @noamross for bringing up hypothes.is - I was unaware, and that could be really helpful for Rmd documents specifically!
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/27#issuecomment-389363550) on: **5/15/2018**

&gt; Google Docs has tons of potential for our manuscripts, but our group is so tied to reference management systems that work with Word and not GDocs that I&#x27;ve hesitated to even bring it up for clinical papers. (If anyone has a solution to that, I&#x27;m all ears!)

In [this blog](https://simplystatistics.org/2016/04/21/writing/) Jeff Leek proposes a solution with gdocs and paperline (I haven&#x27;t tried myself).

---
> from: [**jenniferthompson**](https://github.com/ropensci/unconf18/issues/27#issuecomment-389384896) on: **5/15/2018**

Ah, thanks @maurolepore - I read that when he wrote it but had forgotten!
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/27#issuecomment-390174921) on: **5/18/2018**

Thought it would be interesting to suss out the different components of Word/Google Docs that make it easier for collaborators (or us, in certain cases!)
e.g.
&gt;  If we ask students to submit R work for courses, how do we provide feedback to them? If they submit Rmds, we can insert comments and send back, but annotating HTML pages is hard.

**Feedback** (I&#x27;m definitely a fan of hypothes.is, but I can imagine use-cases where it doesn&#x27;t do the trick – admittedly I haven&#x27;t used it in a while).

&gt; As for non-R users...the tools do exist to take their input from Google Sheets/Google Drive and incorporate it in your R workflow. You lose the version control, but googlesheets and googledrive have helped immensely.

**Version control** (there are good workflows around this, but, it _does_ depend on ⇩

**Technical resistance** I imagine there are some collaborators who don&#x27;t _do_ google docs/sheets, etc.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/27#issuecomment-390370809) on: **5/18/2018**

Summary: How to maximize input from those who don&#x27;t use R, RStudio or Git, but might use GitHub?
(1) Google sheets and docs (collaborative editing + some version control; (2) hypothes.is (comment on html); (3) find why people resist better tools and try to help them; (4) accept some people will always resist.
