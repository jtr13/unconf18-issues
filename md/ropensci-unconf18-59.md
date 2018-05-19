# [Building meta-packages (e.g. tidyverse) to centralize multiple packages](https://github.com/ropensci/unconf18/issues/59)

> state: **open** opened by: **maurolepore** on: **5/14/2018**

Do you find yourself repeatedly installing or loading the same packages? How about building a meta-package? 

The main goal of a meta-package is to install and load other packages (a famous example is the __tidyverse__ package). But also you may use the pkgdown website of a meta-package as a kind of meeting point for all the packages it gathers (e.g. [tidyverse](https://www.tidyverse.org/); [fgeo](https://forestgeo.github.io/fgeo/)).

It turns out that building a meta-package is surprisingly simple. The source code of the __tidyverse__ is an excellent template. You could use it to build your own meta-package, or we could generalize it to create a package that creates a meta-package. Is this getting too meta?
:)

### Comments

---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/59#issuecomment-390099150) on: **5/18/2018**

Summary: Building a package to create a meta-package, such as the __tidyverse__.
