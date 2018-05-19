# [Test project / package after hypothetical package update](https://github.com/ropensci/unconf18/issues/62)

> state: **open** opened by: **czeildi** on: **5/15/2018**

Related to #31 and also the following comment of @noamross in #35 

&gt; If you want to do live testing of a package, like seeing what system files/folders it modifies, I&#x27;m working on a Dockerized setup for our standard package tests: https://github.com/noamross/launchboat, so one could run tests in an isolated environment before installing.

Before updating a dependency to the newest version see which tests would break.

I can imagine this as a service (or maybe Rhub can already do this??) or a local version with Docker ensuring a separate environment. 

### Comments

