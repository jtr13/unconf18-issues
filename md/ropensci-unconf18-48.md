# [Package usage &quot;in the wild&quot;](https://github.com/ropensci/unconf18/issues/48)

> state: **open** opened by: **batpigandme** on: **5/2/2018**

Related to #25 (see https://github.com/ropensci/unconf18/issues/25#issuecomment-384220571), but I think it&#x27;s a sufficiently distinct approach to merit its own thread.

### Overall idea
As a user, I often find it&#x27;s helpful to see use-cases for packages and/or functions &quot;in the wild&quot; (i.e. in the context of some workflow or task). Some packages have great vignettes that cover this, but (limited to just a few people) there&#x27;s simply no way for maintainers/developers to think of all the possible ways a package might come in handy. It can also be extremely helpful to read explanations from people who _didn&#x27;t_ write the package, since they have a sort of &quot;beginner&#x27;s mind.&quot; (I&#x27;ve done a few &quot;roundups&quot; of tweets, often of blog posts using various packages, e.g. for [purrr here](https://maraaverick.rbind.io/2017/09/-purrr-ty-posts/) for this reason).

I imagine (and have anecdotal twitter evidence 😏) that maintainers _also_ like seeing how their packages are being used, but don&#x27;t always get that feedback, even when it exists, since the avenues are somewhat limited.
#### A very roughshod diagram of relationships among packages/feedback that exists &quot;formally&quot;
![package_relationships](https://user-images.githubusercontent.com/831732/39514200-8a5fff60-4dc4-11e8-929e-8eeefa696de4.png)

Here&#x27;s where it gets fuzzy implementation-wise, but I&#x27;ve been wondering if there would be a good way to highlight package usage in blog posts or case studies (e.g. with blogdown), in such a way that users and maintainers would be able to easily find relevant content.

Carl Goodwin&#x27;s been doing something to this effect by including tables of packages and functions used in his blogposts (see example from [Surprising stories hide in seemingly mundane data](https://thinkr.biz/2017/12/20/geospatial/) below), but this is (to my knowledge) done by hand, and isn&#x27;t something one would be necessarily be able to find from any docs related to, say, [rgeolocate](https://github.com/Ironholds/rgeolocate).
&lt;img width&#x3D;&quot;554&quot; alt&#x3D;&quot;thinkr_biz_r_toolkit&quot; src&#x3D;&quot;https://user-images.githubusercontent.com/831732/39514941-9b29d454-4dc6-11e8-8122-69c12f4d90da.png&quot;&gt;

### Stumbling blocks

* Implementation (want to make it useful, without being platform-specific).
* Would want it to be opt-in for package maintainers(?)
* Possibly just a human communication issue that could be encouraged by, say, talking to other humans.
* Breaking changes — blog posts might be an ephemeral format for this very reason.


### Comments

---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/48#issuecomment-385919720) on: **5/2/2018**

Not related to feedback, but certainly to the broader &quot;usage in the wild&quot; issue is the option of trawling &#x60;.Rhistory&#x60; files for those who have/use them. This is an option we are pondering for the [&#x60;flipper&#x60;](https://github.com/ropenscilabs/flipper) package-discovery package. Users opt-in to allow trawling, with  relevant data extracted and uploaded for our analytic needs. Insight would be very crude, but better than nothing, and it would readily allow auto-extraction and analysis of a local code context in which package functions are used.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/48#issuecomment-385931336) on: **5/2/2018**

Often when I want to see how a function or package is used _in other packages_ I&#x27;ll do a GitHub search of CRAN packages using [the METACRAN org](https://github.com/cran). One could probably design some search patterns to identify R bookdown and blogdown sites on GitHub and crawl them to look at package or function usage. 
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/48#issuecomment-385932929) on: **5/2/2018**

@noamross precisely! That&#x27;s the piece I that has no loop, currently.
---
> from: [**apreshill**](https://github.com/ropensci/unconf18/issues/48#issuecomment-387233351) on: **5/7/2018**

I ❤️ this idea. I think about this a lot when teaching, because all the formal documentation (by design and by necessity) shows functions typically in isolation, or only in combination with other functions within a package. Some good examples are usage of &#x60;dplyr&#x60; functions like &#x60;between&#x60; or &#x60;na_if&#x60; which in practice will typically go inside a &#x60;mutate&#x60;, but in the docs those examples aren&#x27;t shown. _(A counter-example is for &#x60;case_when&#x60; where it is clearly shown how to use within a &#x60;mutate&#x60; 👍)_ These are just examples I&#x27;ve run into recently, but it is always a struggle when I teach.

&quot;In the Wild&quot; though, most people use functions across several different packages. A stumbling block I recently ran into learning &#x60;purrr&#x60; turned out to be that I failed to realize a function from &#x60;dplyr&#x60; was actually what I needed in my workflow (&#x60;bind_rows&#x60;!). So, I&#x27;m excited about the idea to help users better discover how functions are used in context, and perhaps which co-occur frequently (sort of like on Amazon, other users who used this package/function used it along with these other ones). 

I also like the idea of building off of and aggregating all the awesome &quot;real world&quot; code examples on blogs, like the R weekly [&quot;R in the Real World&quot;](https://rweekly.org/#RintheRealWorld) features and [&quot;code throughs&quot;](https://twitter.com/search?q&#x3D;from%3Adataandme%20code-through&amp;src&#x3D;typd) as @batpigandme labels on twitter. 
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388030549) on: **5/10/2018**

@apreshill yeah, I feel like there is so much great material out there, but it can be really hard to find — especially when you&#x27;re in the throes of getting something done, _but_ the bite-sized, real-world examples are often exactly what you need for that click 💡 !

As you (obviously) know, this is certainly true with blogdown (see the thread Alison started on the rstudio community site [here](https://community.rstudio.com/t/what-is-hard-about-blogdown/8108)), and I think one of the difficulties is that people end up submitting questions as GitHub issues, making it hard on the maintainer(s) (again, thinking of blogdown here).

Anyway, just spitballing at this point, but I have been thinking about this as I&#x27;ve been following the thread you started!
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388656770) on: **5/13/2018**

&gt; Carl Goodwin&#x27;s been doing something to this effect by including tables of packages and functions used in his blogposts

I like the idea of gathering all functions across multiple packages in a single searchable table. I would like to see/help-build such a thing for rOpenSci and the tidyverse. Using a &#x60;DT::datatable()&#x60;  this seems like a short unconf project ([example](https://forestgeo.github.io/fgeo/articles/fgeo.html#functions), [doc](https://forestgeo.github.io/fgeo/reference/fgeo_index.html)). 


---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388773438) on: **5/14/2018**

&gt; I like the idea of gathering all functions across multiple packages in a single searchable table.

They&#x27;re by no means mutually-exclusive, but I think these ideas differ in that the one is about navigating the _existing_ documentation.
---
> from: [**maurolepore**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388792316) on: **5/14/2018**

I also believe that it would be nice to have better ways to navigate the existing documentation. And in fact, you can think of  the table I suggest as a central interface to do precisely that -- a tool to navigate all the existing documentation of the packages in an onganization. I should clarify that my suggestion is not to generate a table manually but automaticaly. 

Here are some implementation details:

* For any list of installed packages (e.g. &#x60;pkgs &lt;- c(&quot;fgeo.base&quot;, &quot;fgeo.map&quot;, &quot;fgeo.tool&quot;)&#x60;) it is easy to table all functions by package (also of datasets by package).
* If those packages belong to a single github organization, the links to their corresponding pkgdown websites have a consistent structure (e.g. https://forestgeo.github.io/fgeo.base/, https://forestgeo.github.io/fgeo.map/, https://forestgeo.github.io/fgeo.tool/). It is then easy to create the links programatically for an organization with lots of packages such as rOpenSci.
* By using the &#x60;DT::datatable()&#x60; widget, the table can be searchable and clickable.

You can maintain this table with almost no extra effort. You can include the table in a vignette of a meta-package (e.g. __tidyverse__ and [__fgeo__](https://forestgeo.github.io/fgeo/articles/fgeo.html)). Because the meta-package tracks package versions, updating the vignette of the meta-package updates the table of functions by package.


---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388912451) on: **5/14/2018**

&gt; I also believe that it would be nice to have better ways to navigate the existing documentation. 

I agree, I&#x27;m wondering if it might be worth making this into its own thread, especially since you seem to have so much of the code in place, and it&#x27;s possible this could be accomplished pretty quickly (IIRC, there were a few indivs/groups who did more than one &quot;project&quot;/tackled more than one issue at last year&#x27;s unconf).

So, I think it&#x27;s worthwhile to be clear and disambiguate two potential projects
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/48#issuecomment-388930225) on: **5/14/2018**

**Summary**: [Design patterns to] identify, and aggregate applied usage of packages and constituent functions as they&#x27;re used in practice/conjunction with other packages). Implement some sort of option for package developers to easily point to package function use in &quot;R in the Real World&quot;/&quot;code-through&quot; examples.
