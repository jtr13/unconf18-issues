# [Collaboration workflow for users who are willing to use RStudio](https://github.com/ropensci/unconf18/issues/75)

> state: **open** opened by: **lauracion** on: **5/18/2018**

## Summary for another of the projects that came up while discussing #42

@jzelner&#x27;s wrote: &quot;package approach for users who are willing to collaborate using RStudio:

1. Compile to a zipfile or other archive, with a) an RDS file containing all of the R objects needed in the course of generating the final PDF/HTML/MD document, b) a directory of binary or text files (e.g. figures, csv files), c) a requirements.txt style manifest listing both what is in the archive and any R dependencies. 

2. At document-generation time, the archive is mounted and accessed without expanding it into the filesystem, and executed like a normal RMD.&quot;

### Comments

