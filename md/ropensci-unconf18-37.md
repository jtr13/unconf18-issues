# [Discussion: Expanding peer review of code](https://github.com/ropensci/unconf18/issues/37)

> state: **open** opened by: **noamross** on: **4/24/2018**

rOpenSci has long been interested in incubating projects that adopt our approach to open peer review of code in areas outside our [scope](https://github.com/ropensci/onboarding/blob/master/policies.md#aims-and-scope), such as in other languages or, especially for implementations of statistical algorithms.  A few unconf attendees (inc. @mmulvahill, @dynamicwebpaige, @jenniferthompson) have expressed interest in this, so it would be good to set aside time to discuss prospects for new code review projects. I suggest this would be a second-day 60-90 minute lunch discussion rather than a full two-day project, but depending on people&#x27;s interest some of us could run with it!

### Comments

---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/37#issuecomment-384131575) on: **4/24/2018**

🙋 I also am very interested in this, for software review at Methods in Ecology and Evolution and other domain-specific journals publishing software descriptors. The main problem I&#x27;ve faced handling these papers at MEE is that the pool of potential reviewers has very little experience reviewing code and usability. 

Lunch discussion sounds like a great idea! 
---
> from: [**jenniferthompson**](https://github.com/ropensci/unconf18/issues/37#issuecomment-384143386) on: **4/24/2018**

Sounds like a plan! 🎉 
---
> from: [**mmulvahill**](https://github.com/ropensci/unconf18/issues/37#issuecomment-384155364) on: **4/25/2018**

A colleague and I have been looking into ways to improve the availability/quality/dissemination of new biostats tools &amp; methods.  We started with a series of 30+ interviews ~2 yrs ago with biostatisticians and others with related experience (including @karthik).  The overall outcome was that there&#x27;s room for biostats-trained software devs within departments with some forethought (if funding is included in grants), and that rOpenSci had already made great progress on the curation and quality issues we also came across.  

We&#x27;ve been working on the software dev side but not the curation/quality, so hearing you&#x27;re interested in incubating other domains made my ears perk up.

Our focus has been on methods developed within [CTSA&#x27;s](https://ncats.nih.gov/ctsa) and the Biostats, Epi, &amp; Research Design (BERD) arms of these institutional grants, for no other reason that&#x27;s been our funding source.  Combining forces with others from other domains would be 👍 👍 👍

Look forward to talking more -- lunch would be great!



---
> from: [**seaaan**](https://github.com/ropensci/unconf18/issues/37#issuecomment-384509190) on: **4/26/2018**

I would be interested in this too. 
---
> from: [**lauracion**](https://github.com/ropensci/unconf18/issues/37#issuecomment-384627479) on: **4/26/2018**

I am also interested in this discussion - mostly as a listener I believe.
---
> from: [**jhollist**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385119292) on: **4/27/2018**

While I won&#x27;t be in Seattle, I am very interested in the outcome of this discussion.  

We are currently working on implementing some level of code review in our internal EPA review process.  My plan was to borrow heavily from rOpenSci onboarding.  Will anxiously watch this issue over the next few weeks!
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385220955) on: **4/28/2018**

Count me in. I would love to learn more about the current review process and its potential for expansion.
---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385476154) on: **4/30/2018**

@goldingn: I think this is quite a good problem statement. 

&gt; The main problem I&#x27;ve faced handling these papers at MEE is that the pool of potential reviewers has very little experience reviewing code and usability.

I get the feeling that this is a bigger task that I realize but I wonder about the feasibility of a suite of code review tools. Off the top of my head I can think of the following packages that would be useful when evaluating code:

- lobstr
- usethis
- goodpractice
- codetools
- profvis
- lintr
- styler

I wonder if it would be possible to develop a sort of devtools for reviewers (&#x60;revtools&#x60;?) whereby someone approaching a potential review project could expand on the tools available in [pkgreviewr](https://github.com/ropenscilabs/pkgreviewr). If one could develop a clear API, it could help a possible reviewer. The idea here is that it would give a possible reviewer the flexibility to ask some questions of the code itself. For example &#x60;lobstr::cst()&#x60; comes to mind as a useful function to provide a reviewer when you have function call upon function call. The idea here would be to provide flexible, rather than prescriptive, tools. 
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385478861) on: **4/30/2018**

@stephlocke started working on sthg similar in https://github.com/lockedata/PackageReviewR
---
> from: [**stefaniebutland**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385487775) on: **4/30/2018**

@annakrystalli &#x60;pkgreviewr&#x60; mentioned 👆
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385496229) on: **4/30/2018**

@boshek +1 for the name &#x60;revtools&#x60;!

Yeah, something like that would be super helpful (though even just a written guide/rubric to get people started would help people in our case).

I had checking out &#x60;pkgreviewer&#x60; on my to do list, but &#x60;PackageReviewR&#x60; looks awesome too! 
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385537755) on: **4/30/2018**

Just bookmarking this: we had a conversation a bit ago with an organization interested in our review process.  It wasn&#x27;t public, but they asked good questions about initiating the process, so I just (very roughly) edited the notes down to our one-sided responses: https://docs.google.com/document/d/14m1Rkp4WKPpGn585r21g3xcb0mVDHy3Ov9N2qUdqetA/edit
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385539571) on: **4/30/2018**

And, many might have already seen these, but some relevant posts:
- https://ropensci.org/blog/2016/03/28/software-review/
- https://ropensci.org/blog/2017/09/01/nf-softwarereview/

@goldingn we feel you, building and maintaining the reviewer base is one of the biggest challenges, one I&#x27;m happy to chat more about.  From the second post:

&gt; One of the core challenges and rewards of our work has been developing a community of reviewers. Reviewing is a high-skill activity. Reviewers need expertise in the programming methods used in a software package and also the scientific field of its application. (“Find me someone who knows sensory ecology and sparse data structures!”) They need good communications skills and the time and willingness to volunteer. Thankfully, the open-science and open-source worlds are filled with generous, expert people. We have been able to expand our reviewer pool as the pace of submissions and the domains of their applications have grown.
&gt;
&gt;Developing the reviewer pool requires constant recruitment. Our editors actively and broadly engage with developer and research communities to find new reviewers. We recruit from authors of previous submissions, co-workers and colleagues, at conferences, through our other collaborative work and on social media. In the open-source software ecosystem, one can often identify people with particular expertise by looking at their published software or contribution to other projects, and we often will cold-email potential reviewers whose published work suggests they would be a good match for a submission.
&gt;
&gt;We cultivate our reviewer pool as well as expand it. We bring back reviewers so that they may develop reviewing as a skill, but not so often as to overburden them. We provide guidance and feedback to new recruits. When assigning reviewers to a submission, we aim to pair experienced reviewers with new ones, or reviewers with expertise on a package’s programming methods with those experienced in its field of application. These reviewers learn from each other, and diversity in perspectives is an advantage; less experienced developers often provide insight that more experienced ones do not on software usability, API design, and documentation. More experienced developers will more often identify inefficiencies in code, pitfalls due to edge-cases, or suggest alternate implementation approaches.

I remember when JOSS launched we both wanted to help and were worried about cannibalizing our own reviewer pool, but it&#x27;s grown organically, and I think we could definitely use our own reviewer pool to help incubate a new organization again.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385540130) on: **4/30/2018**

Expanding &#x60;pkgreviewer&#x60; and&#x60;PackageReviewR&#x60;, and perhaps integrating them, might be a full-blown unconf project if folks want to take it up.
---
> from: [**stephlocke**](https://github.com/ropensci/unconf18/issues/37#issuecomment-385619039) on: **5/1/2018**

I&#x27;m happy for PackageReviewR to be cannibalised into ropensci or worked on standalone. I&#x27;m not at the unconf this year but can facilitate/assist/mentor remotely.
---
> from: [**annakrystalli**](https://github.com/ropensci/unconf18/issues/37#issuecomment-386540216) on: **5/4/2018**

Sorry to arrive late to this party. Very happy for &#x60;pkgreviewr&#x60; to be integrated into a more comprehensive suite of tools. And absolutely love &#x60;revtools&#x60; as a name! 💜💯
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/37#issuecomment-387901398) on: **5/9/2018**

I&#x27;ve been working on a tool to create a package diagnostic report.  I had originally thought of it as giving a quick scan for us rOpenSci editors to use, and also provide a standardized build environment, but I&#x27;ve expanded its scope to try to cover numerous things that reviewers could use.  Working on this [here](https://github.com/noamross/launchboat) (draft report [here](https://noamross.github.io/launchboat/pkg-report.html), but 100% intend to fold it into &#x60;pkgreviewr&#x60; or its successors.   The thing I&#x27;ve gotten into recently is trying to provide a report about package functions, their [relative complexity and relationships amongst each other using static code analysis]().

Anyway, it sounds like we have two potential ideas here:

-  A Day 2 conversation about review from a social/institutional/planning perspective
-  A unconf _project -to expand package review tools specific to R and rOpenSci.  To this idea I would throw in the idea of adding some [new goodpractice checks](https://github.com/MangoTheCat/goodpractice/issues).

I&#x27;ll open a new issue for the 2nd bullet.
---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/37#issuecomment-389276942) on: **5/15/2018**

I did mention the rOpenSci reviewing guidelines to the software working group in our center for data to health (CD2H) project. This is a group that is encouraging software best practices in CTSA (Clinical &amp; Translational Sciences Award) centers, and they are looking for a similar kind of review process.

They seemed very interested, and I&#x27;m happy to facilitate any conversations rOpenSci people might want to have with them.
