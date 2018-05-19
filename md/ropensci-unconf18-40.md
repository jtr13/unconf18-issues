# [Modular tools for a drat / mini-cran repository](https://github.com/ropensci/unconf18/issues/40)

> state: **open** opened by: **cboettig** on: **4/25/2018**

rOpenSci maintains a [drat](https://github.com/eddelbuettel/drat) repository that is built nightly by Circle-CI (with the help of [drat.builder](https://github.com/richfitz/drat.builder)) at http://packages.ropensci.org.  At the moment the utility of this is somewhat minimal; it provides an alternative to &#x60;devtools::install_github()&#x60; an hosts some supplemental data packages too large for CRAN.

Maintaining a cran-like repo of development versions could be a lot more compelling if we explored some additional features.   I think some of these could also be seen as useful services / perks of for a maintainer having their package on-boarded. Ideally these would be implemented in modular tools other groups could adopt on ad-hoc basis as well.  What would you like to see?

- prebuilt binaries (Mac, Windows, even Linux?)  Could significantly reduce install times when downloading packages, possibly useful for CI setups too.   (I believe @jeroen has some thoughts here). 

- Nightly builds.  Particularly useful for packages that interact with an API that might introduce a breaking change.  Currently we do this already via Travis, but with so many rOpenSci packages that can back up Travis builds of packages under active development.

- Dashboard summaries: a convenient dashboard to see which rOpenSci packages are failing tests on what platform, how frequently they have been downloaded (from the drat/mini-cran, also from CRAN), GitHub issues, other information.  

- security features.  Previous unconfs (@hrbrmstr and others) have brainstormed about what a secure package repository might look like, signed packages etc.  A working platform (with binaries too!) might give us an interesting platform to try out these ideas? 

- reverse dependency checks. particularly for packages in our ecosystem that depend on other rOpenSci packages. 

- ... Other ideas?


Would love to see feedback / interest flushing out any of the above as well as suggestions for other related services you could imagine for such an rOpenSci central repository.  

### Comments

