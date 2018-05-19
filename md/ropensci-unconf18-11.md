# [Screenshot tools in R](https://github.com/ropensci/unconf18/issues/11)

> state: **open** opened by: **maelle** on: **3/8/2018**

I&#x27;ve recently discovered that [&#x60;RSelenium&#x60;](https://github.com/ropensci/RSelenium) and [&#x60;seleniumPipes&#x60;](https://github.com/johndharrison/seleniumPipes) offer screenshot capabilities, including the use of CSS selectors. Their syntax might be easier to use than [&#x60;webshot&#x60;](https://cran.r-project.org/web/packages/webshot) when one needs to perform an action on the webpage before taking the screenshot. 📸 

I think it could be useful to 

* assess and compare the screenshot functionalities of these three packages 📄 

* design a new function or package using them that&#x27;d make screenshots even easier. 🔧 

A good tool for screenshots would:

* be well documented

* have all arguments &#x60;webshot&#x60; has (CSS selection, cliprect, expand, etc.)

* but would support not using JavaScript but instead the more &quot;intuitive&quot; commands one use in e.g. seleniumPipes

* would support different browsers

* cover both websites and Shiny apps like these three packages do

* would use &#x60;magick&#x60; for image processing and would return a &#x60;magick&#x60; object instead of writing the screenshot to disk (or would at least offer this possibility).

A bonus would be to also cover screencasts, cf [&#x60;rDVR&#x60;](http://johndharrison.github.io/rDVR/). 🎥 

### Comments

---
> from: [**jimhester**](https://github.com/ropensci/unconf18/issues/11#issuecomment-384268789) on: **4/25/2018**

I don&#x27;t have a ton of experience in this space, but the impression I have is Selenium is being phased out in favor of webdriver, which works across multiple browsers.

There is a long standing open issue https://github.com/wch/webshot/issues/2 about improving the interaction, maybe this project could work on a PR to provide a similar interface from seleniumPipes in webshot.
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/11#issuecomment-384271905) on: **4/25/2018**

Ah cool, and I like that issue text 😀 
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/11#issuecomment-388915137) on: **5/14/2018**

@wch before I summarize or close this, in theory would you be interested in a PR for the issue mentioned above? And could it be done independently of https://github.com/wch/webshot/issues/62#issuecomment-387785132 ? Probably not? 
---
> from: [**wch**](https://github.com/ropensci/unconf18/issues/11#issuecomment-389267089) on: **5/15/2018**

@maelle I would consider a PR, but I personally don&#x27;t think that it&#x27;s a good place to put time and effort.

Webshot uses CasperJS, and any interaction code would likely be built on CasperJS. CasperJS is a library specifically for PhantomJS, which in turn is no longer being developed.

As @jimhester mentioned, the [webdriver](https://github.com/rstudio/webdriver) package is a better way to do interaction. (The reason that webshot doesn&#x27;t use webdriver is that webdriver has several dependencies, and there are some applications where webshot is used it&#x27;s important to have few dependencies.)

---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/11#issuecomment-389279896) on: **5/15/2018**

Thanks!
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/11#issuecomment-390113585) on: **5/18/2018**

Summary: build a package based on webdriver to produce screenshots of websites and Shiny apps for documentation/presentation purposes.
