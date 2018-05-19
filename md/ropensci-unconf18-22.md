# [Git + R nirvana: how to get there](https://github.com/ropensci/unconf18/issues/22)

> state: **open** opened by: **jennybc** on: **4/11/2018**

The tools most of us use to accomplish Git/GitHub magic **from R** are the RStudio IDE and the [git2r](https://github.com/ropensci/git2r) package (part of the rOpenSci org).

Under the hood, these exploit different tools to enact Git operations: system Git (RStudio IDE) and libgit2 (git2r). This means that various aspects of Git configuration can be good to go for one but not the other. This is mostly about configuring credentials for Git remotes, e.g. setting up SSH keys.

I&#x27;ve done a fair amount of testing and documenting for [Happy Git](http://happygitwithr.com). But I think initial setup could become even easier and better documented with respect to tricky bits, such as using passphrase-protected SSH keys on Windows. I&#x27;d love to stress-test and improve setup instructions for Git so that more people have more success across Mac/Windows/Linux for command line Git (--&gt; RStudio IDE) and git2r (--&gt; devtools, usethis, etc.).

### Comments

---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/22#issuecomment-382194317) on: **4/17/2018**

&gt; But I think initial setup could become even easier and better documented with respect to tricky bits...

I totally agree. Considering the key role of Git and GitHub in data science workflows, and how nicely integrated these tools are with RStudio, I think the resources for people to learn remain scarce. For example, there is only one RStudio webinar on GitHub and RStudio ([Managing Change Part 2](https://www.rstudio.com/resources/webinars/)), which -- I believe -- doesn&#x27;t cover SSH keys, and was recorded before RStudio included a terminal.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/22#issuecomment-388659759) on: **5/13/2018**

A little off-topic but still related to git2r. A tool to [Automatically generate list of contributors](https://github.com/r-lib/devtools/issues/1279) has already been packaged up?

&gt;  I have local code to achieve this and will package up at some point
-- @hadley

