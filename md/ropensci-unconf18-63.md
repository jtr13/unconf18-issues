# [Connecting R educators &quot;in the wild&quot;](https://github.com/ropensci/unconf18/issues/63)

> state: **open** opened by: **apreshill** on: **5/15/2018**

I know it is late to propose a new project, so consider this an invite to talk with me more about this idea at unconf if it resonates with you!

**Problem:** 
People who teach R create awesome R markdown, blogdown, and bookdown materials for teaching, most of which are stored on GitHub. But, they can be hard to find (everyone knows @STAT545-UBC, but discoverability of even these materials is low for people not fully steeped in #rstats). The [tidyverse site](https://www.tidyverse.org/learn/) has some links to courses, but the materials are variable: some are PDF syllabi, some are full repos, some are formal university course listings. 

**Idea:** 
Inspired by @batpigandme&#x27;s idea (#48), I&#x27;ve been thinking of a website to aggregate existing educational materials from GitHub. Ideally, one could search GitHub for repos that include words in the title/tag/README like &quot;curriculum&quot;, &quot;course&quot;, &quot;workshop&quot;, &quot;bootcamp&quot;, and tag them as such (I want to catch repos like @hadley&#x27;s Data Challenge Labs: https://github.com/dcl-2017-04/curriculum). Other items on my &quot;would be nice&quot; list:

- Tag with blogdown, bookdown, or R markdown site
- Tag with type of license, if there is one, re: reuse/attribution/etc.
- Provide a &quot;tidyverse&quot; percentage: something like, of the packages loaded in the repo, what percent are in the tidyverse ecosystem?
- Provide way to see &quot;last updated&quot; easily, and perhaps in navigable interface allow users to sort by this
- Some kind of topic tagging: like statistics, machine learning, data science, data visualization, natural language processing, etc.
- Perhaps a level tag, like undergrad, grad, K-12, etc.

Selfishly, I would find this type of resource very useful! But past-me would have found it invaluable. I frequently see professors in my own computer science group using Matlab for example because they don&#x27;t know how to start teaching material they know using a language they don&#x27;t know. It would be great to be able to forward them to [courses on machine learning using R](https://github.com/m-clark/introduction-to-machine-learning), for example. Just overheard yesterday a student lamenting that all course materials for ML are in Matlab, the TA only knows python, and she wants to use R, so I think this could also help students. 

More broadly, I would love to establish an *educator&#x27;s collaborative* around teaching R or with R. My university created [one](https://www.ohsu.edu/xd/education/schools/school-of-medicine/education/educators-collaborative/), and they worded it so nicely I&#x27;m just going to plagiarize:
&gt; &quot;The Educators&#x27; Collaborative (EC) is a community of practice for people who are interested in education, including direct teaching, innovation, scholarship, curriculum design and mentoring. A community of practice is a group of skilled practitioners who interact regularly to learn from and with one another for the purpose of professional and personal development. Through in-person or online engagement, they create a shared understanding of purpose and develop communal resources to enhance their respective practices. (Lave &amp; Wenger, 1991; Wenger, 1998).&quot;

I have increasingly been working on team-taught courses and see real value in collaborating on curricula with other R educators. But not everyone has this luxury- it would be great to provide an organization to support innovative R education efforts.

Tagging folks that @stefaniebutland tagged on the Slack channel for interest/involvement in education:
@jennybc @laderast @hadley @jtr13 @czeildi @elinw @seankross @aurielfournier (I can&#x27;t find Jenny Draper on GitHub, so I&#x27;m sorry for not tagging here!)

### Comments

---
> from: [**cboettig**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389255445) on: **5/15/2018**

I think this is a brilliant idea.  

- I currently think of https://community.rstudio.com/c/teaching as my go-to place for an R-based teaching community, would have obvious synergy with such an EC, but doesn&#x27;t meet the goal of an place to find course material.

- A possible venue for collating course material might be new https://jose.theoj.org/about ? (following the JOSS model around content on GitHub).  Not sure if that fits the bill or would be too constrained.  

- Another related effort is maybe the R4DS community https://medium.com/@kierisi/r4ds-the-next-iteration-d51e0a1b0b82, with a very active slack community, but again more forum that catalog of resources. 

- The Carpentries lessons are well-recognized but more narrow example of community + curated workshop material, e.g. http://www.datacarpentry.org/workshops/.    


I do think the whole issue of cataloging resources is really hard though.  As you point out, there&#x27;s such a mix of content, even on a very short and curated collection:

&gt; The tidyverse site has some links to courses, but the materials are variable: some are PDF syllabi, some are full repos, some are formal university course listings.

Personally, I&#x27;ve found examples for whole-semester material, like @jennybc &#x27;s 545 and @hadley&#x27;s data challenge labs, immensely influential to my own approach, because it is nice to see how the parts fit together, in what order, and guided by what philosophy (@hadley&#x27;s analogies with learning baseball still stick with me).  But then I&#x27;m also trying to teach a semester-length course, so that&#x27;s my bias as well (my blogdown-based site is https://espm-157.carlboettiger.info/  )

I know @lwasser and @coatless have both thought a lot about the issue of cataloging resources in this space, so tagging them here.  

---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389265941) on: **5/15/2018**

Neato. Another project I am on (CTSA data to health, CD2H) is trying to do this in terms of data science competencies and finding paths through different courses, as well as assessing any possible gaps. As @cboettig mentioned, it&#x27;s a very difficult process, and the question is how to make it dynamic, since compentencies change. I&#x27;d love to talk to everyone. 

(edit: I&#x27;d like to talk with everyone - but I removed the description of the project. don&#x27;t want to dominate this conversation)
---
> from: [**apreshill**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389305442) on: **5/15/2018**

@cboettig Thank you, yes- my main motivation is to collate long-form materials, of which your ESPM course is currently living in my unwieldy bookmarks folder of inspiring courses! And I agree- seeing others&#x27; whole semester material has shaped so much of how and what I teach. I think having community discussion forums like R4DS and https://community.rstudio.com/c/teaching are also invaluable, but there is a gap to fill. The Carpentries have great content resources, but they tend to be short-form. I do think what is lacking is field-tested quarter/semester-long materials with integrative syllabi, labs, homeworks, grading rubrics, datasets, good in class activities, project ideas, etc. (@jennybc&#x27;s @STAT545-UBC being probably the main exception). As you know, a lot of blood/sweat/tears goes into designing curricula, especially the flow and sequencing for whole courses, with important differences compared to short-form tutorials or code-throughs (which I find really helpful as a learner and teacher, and @batpigandme&#x27;s #48 may improve discoverability of those materials). 

So you got me thinking more about the elements of a [community of practice](http://wenger-trayner.com/introduction-to-communities-of-practice/):

- **The domain:**
   - R
- **The community**:
   - Definition: *In pursuing their interest in their domain, members engage in joint activities and discussions, help each other, and share information. They build relationships that enable them to learn from each other; they care about their standing with each other.*
   - Current communities: 
      - R4DS 
      - https://community.rstudio.com/c/teaching
      - &quot;birds of a feather&quot; groups at @Rstudio conf for example
- **The practice:** 
    - Definition: *Members of a community of practice are practitioners. They develop a shared repertoire of resources: experiences, stories, tools, ways of addressing recurring problems—in short a shared practice.*
   - Current education + R-based practices: 
      - Carpentries instructors perhaps? But this is for workshop formats; need one for &quot;whole course&quot; practitioners.
       - Some university departments may have this, but you need a quorum. There are lots of faculty who are little R islands in their department/university (this is me!).

So, I think we have the first two, but the third element of practice specific to education is the missing piece. In the short-term, having some kind of navigable course repository would allow members to reuse assets- which would be a great start 🎆 

In the long-term, an educational collaborative could aim to:
- Problem solve best practices for teaching certain topics/domains/tools
- Seek experience from people who have already thought about this
- Help other educators build an argument for funding to develop and teach new courses at their institution 
- Grow confidence for new educators 
- Map knowledge and identify gaps (this seems in line with @laderast&#x27;s C2DH project, although probably a higher order goal once a community of practice is in full swing)

I have not heard about The Journal of Open Source Education, thank you for the link!

Also tagging my R education partners in crime: @ismayc @andrewpbray @rudeboybert @DJAnderson07, plus @kierisi and @jthomasmock to join in convo
---
> from: [**coatless**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389322099) on: **5/15/2018**

@cboettig thanks for the ping. I&#x27;m more than happy to join a collective like this. 

On Friday, May 18th, 2018, we&#x27;ll start to open source some of the drawings used in STAT 385 @ UIUC this term in:

https://github.com/coatless/draw-r. 

**Note:** The drawings have largely been done in _Omnigraffle_ or _Keynote_ ( cc&#x27;ing my inspiration / person I blame for my fascination in diagramming @hrbrmstr ). We&#x27;re looking into the ability to generate drawings of _R_ objects dynamically via base or ggplot2 graphics.

Outside of that, we&#x27;ll be working this summer on releasing an _R_ textbook covering &quot;Statistical Programming Methods&quot; or &quot;Data Science Programming Methods&quot; depending on the zeitgeist spirit:

https://github.com/coatless/spm

In the interim, consider some of the other education tech that we&#x27;ve built:

- [&#x60;assignr&#x60;](https://github.com/coatless/assignr):  Tools for Educators Writing Assignments in RMarkdown (joint w/ @daviddalpiaz)
- [&#x60;errorist&#x60;](https://github.com/coatless/errorist):  Automatic Error and Warning Search
- [&#x60;dropcli&#x60;](https://github.com/coatless/dropcli): Dropbox CLI for working on a Linux environment within R.
    - Allows for the live distribution of code via RStudio Server based on [Michael Levy&#x27;s Dropbox Idea at UseR 2016!](https://channel9.msdn.com/Events/useR-international-R-User-conference/useR2016/Teaching-R-to-200-people-in-a-week#time&#x3D;07m20s).
    - We&#x27;ll likely move over to an embedded code environment in lecture slides in Spring 2019.
- [&#x60;rcpp-api&#x60;](https://github.com/coatless/rcpp-api): Unofficial Rcpp API Documentation (Lots of Examples!)
- &#x60;coursetools&#x60;: Administrative Tools to Manage Online Courses (GitHub + Blackboard)
- &#x60;autograder&#x60;: Automatically Grade Models ([screenshot](https://twitter.com/axiomsofxyz/status/979775789192437761))

The later two are somewhat restricted to UIUC personnel at the moment.
---
> from: [**datalorax**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389327604) on: **5/15/2018**

I love this idea! (and thanks for including me in the convo!) Just a few thoughts:

Part of what I think can be difficult, both as a learner and as an instructor, is just the sometimes overwhelming amount of stuff out there. There are lots of good resources, but navigating what to teach (or learn) and when can be difficult. I would imagine a collaborative like this sort of serving as a curator of open-source teaching materials, and the wisdom of the community could help inform the topic sequence.

In terms of the content itself, I wonder if it might make sense to have people/organizations actually submit their materials to a repo for inclusion, rather than actively gathering existing materials (although gathering known materials of high quality would be a great starting point). Then, they could potentially even go through some sort of peer review process, which would (potentially) not only help the community (through the addition of the new content) but also the instructor (by getting feedback on their materials).

I also tend to think a lot about the match between the learner and the content. This may be a few steps down the line, but I wonder if, after the content was curated, it might be worth thinking about developing some sort of survey or even pre-tests that would ultimately recommend where to start, i.e., - what level of programming background do you/your students have? How much experience do you/your students have with statistics? This could potentially help align learner needs with content that is not too easy/difficult.

---
> from: [**kierisi**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389352331) on: **5/15/2018**

hey y&#x27;all, I&#x27;m a former high school science teacher with a lot of opinions about how we can integrate best practices from K-12 education as a means of equipping learners with the skills and confidence needed to teach themselves, with the ultimate goal being the (further) democratization of data science education (with R). 

always happy to chat - this is an area I&#x27;m currently researching and actively beginning to develop resources in, many which will begin to find their way back into the R4DS online learning community (which I&#x27;m also always happy to talk about!)
---
> from: [**jthomasmock**](https://github.com/ropensci/unconf18/issues/63#issuecomment-389353076) on: **5/15/2018**

Honored and many thanks for including me in this conversation! 

I think as @DJAnderson07 mentioned, it is hard as a learner to sift through the blogs, Quora posts, SO answers, various package vignettes and figure out an efficient learning path. A curated, organized list of proper coursework would be huge for self-directed learners, many of whom may not have access to Data Science at the college level or even MOOCs such as Coursera, DataCamp, Udacity, etc.

All that being said, I lack the teaching expertise of likely everyone in this group, but am happy to contribute by reviewing or gathering material, and generally acting as a student advocate.  Excited to see what comes of this!
---
> from: [**lwasser**](https://github.com/ropensci/unconf18/issues/63#issuecomment-390301065) on: **5/18/2018**

A few of us started this effort a few years back including tracy teal and matt jones!! We started a prototype site but nothing ever came of it. Happy to be involved in the discussion and to share what we learned from it as well! Il post our beta website here when I&#x27;m back to my computer!
---
> from: [**jthomasmock**](https://github.com/ropensci/unconf18/issues/63#issuecomment-390326635) on: **5/18/2018**

Found some great content from UC Berkeley&#x27;s Data Science Program, unfortunately appears to be exclusively Python, but some great frameworks. 

https://data.berkeley.edu/undergraduate-ds-pedagogy
http://data8.org/
http://data8.org/sp18/
