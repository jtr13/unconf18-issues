# [Summarize change of packages since previous versions](https://github.com/ropensci/unconf18/issues/31)

> state: **open** opened by: **czeildi** on: **4/19/2018**

In a bigger project or if you take up a project after some period you may want to update your packages and after such an update you may need to make several changes to your code. This can happen without any package management system or with packrat / checkpoint / docker etc. Even if you use packrat / checkpoint / docker in order to ensure reproducibility you would like to update dependencies from time to time: either you need somehing specific from a newer version or you just know that sooner or later you have to update and the longer you wait the more difficult it will be. However, you should be able to assess beforehand the amount of work needed after an update.

I propose a package which could generate a digestible summary of all the changes in the dependencies of your project between current state and newest versions. It would ideally work with or without an existing depedency manager.

- identify current versions of dependencies and their newest versions
- collect news from cran (+github) (+ any other repository)
- create an html / web page from these, ideally organized by breaking changes / new features / fixes

Improvement possibilities:

- work for subset of packages
- work for cran newest and dev versions as well
- idetify usages in your code
- propose how to change your code: copy pastable code / functions to reformat if possible (ie only rename)
-  parse changes from code instead of news.md: would be more accurate

related:

- generate news.md skeleton based on code changes since last package version

I believe we could build on several existing packages: possibly containerit to identify dependencies, gh to pull news from github

related:
https://twitter.com/noamross/status/989904927093936128

### Comments

