# [Extensions to R / RStudio&#x27;s autocompletion system](https://github.com/ropensci/unconf18/issues/65)

> state: **open** opened by: **jimhester** on: **5/16/2018**

This was proposed by @kevinushey for last year&#x27;s unconf, but he unfortunately Kevin had to miss the event last year. (https://github.com/ropensci/unconf17/issues/52)

In the meantime I have started a proof of concept package https://github.com/jimhester/completeme, that implements some of what he proposed, but it would be great to improve the RStudio IDE integration and discuss ways to make this more full featured and robust, both for terminal completions, things like https://github.com/REditorSupport/languageserver and in the IDE.

### Comments

---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/65#issuecomment-389549695) on: **5/16/2018**

I&#x27;d love to see this, as you well know @jimhester. readxl was an early target of your explorations (unmerged PR: https://github.com/tidyverse/readxl/pull/320).

For context, this would be a nice way to expose, say, a set of example inputs in a package. In the world of readr and readxl, you could make it easy for users to get the possible filenames in front of their eyeballs and then pick one.

While I&#x27;m wishing ... it would be interesting to see if the developer interface could be more like &#x60;match.arg()&#x60;, i.e. your wishes about auto-completion are expressed in the target function itself vs. elsewhere in the package.
