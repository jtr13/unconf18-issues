# [teach clean code principles with examples in R](https://github.com/ropensci/unconf18/issues/32)

> state: **open** opened by: **czeildi** on: **4/19/2018**

Writing clean code is important for efficient work in every programming language. However, most of the resources available (at least what I encountered so far) contain examples in primarily object oriented languages making it less accessible for R programmers who are not software engineers.

Clean code makes it easier to collaborate, to avoid bugs and write working code faster. It also helps with understanding code written by others.

I envision a blog post series / bookdown with the relevant principles adopted from the Clean Code book with examples in R, focusing on every day R users and not necessarily those writing production R code. (i.e. do not mention error classes or R6 classes but focus on the most common use cases) 

See:
- https://cran.r-project.org/web/packages/cleanr/index.html 
- [Robert C Martin: Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

### Comments

---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/32#issuecomment-388029375) on: **5/10/2018**

Is there an online version of this book anywhere? I&#x27;d be curious to see what it&#x27;s all about!
---
> from: [**czeildi**](https://github.com/ropensci/unconf18/issues/32#issuecomment-388569857) on: **5/12/2018**

@batpigandme afaik the book is not available for free but there&#x27;s ebook version.
---
> from: [**czeildi**](https://github.com/ropensci/unconf18/issues/32#issuecomment-388890765) on: **5/14/2018**

We just held a workshop on this topic with @paljenczy at [eRum 2018](http://2018.erum.io/#talk-2-303) and we created a [cheatsheet](https://github.com/czeildi/erum-2018-clean-r-code/blob/infra/clean_r_code_cheatsheet_2018-05-08.pdf) which could be a starting point for a more in-depth material.

@hadley I also thought about differences and similarities with your styleguide book http://style.tidyverse.org For one part the styleguide seems to be a subset of the clean code topic. I think style as a more local thing and clean code (like organizing functions) as a more global topic which makes sense at a somewhat larger scale. But you also touch these topics, like in the section on function design [here](http://style.tidyverse.org/functions.html#design).

Actually I think that at the unconf I&#x27;d like to work on a project more about actual coding but outside the unconf I&#x27;d love to think more and possibly collaborate around this topic. 
---
> from: [**hadley**](https://github.com/ropensci/unconf18/issues/32#issuecomment-389226936) on: **5/15/2018**

@czeildi I think your cheatsheet is a little too prescriptive; we should chat about it in person.
