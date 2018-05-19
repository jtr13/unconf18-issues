# [Datasets search](https://github.com/ropensci/unconf18/issues/26)

> state: **open** opened by: **elinw** on: **4/16/2018**

When I&#x27;m writing tutorials or documentation or when I&#x27;m teaching I often fall back on the same sample data sets over and over. At the same time, when I need something specific such as an ordered factor I have to search around to find one.  I try to stick to the base datasets.  I was thinking that it would be neat to have something (a package or a shiny app or a combination) that would let you search for a specific class of data structure (data frame, matrix, ts, dist, cube etc (there are a lot))  an also for specific variable types for those types that support multiple types. Maybe also experimental versus observational?  https://vincentarelbundock.github.io/Rdatasets/datasets.html  has a list of the data sets, but the purpose of that archive is more to put them all into csv format in a consistent manner.

An added bonus would be to be able to make the api generic enough to search other packages but my initial goal would be the ones in datasets.

### Comments

---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/26#issuecomment-382140279) on: **4/17/2018**

Cool idea! Trying to figure if I understand correctly. Do you mean something like:

&#x60;&#x60;&#x60;
check_dataset(package &#x3D; &quot;datasets&quot;)
# A tibble: 8 x 6
  Package  Item          Title                                                        Rows  Cols Class     
  &lt;chr&gt;    &lt;chr&gt;         &lt;chr&gt;                                                       &lt;int&gt; &lt;int&gt; &lt;chr&gt;     
1 datasets ability.cov   Ability and Intelligence Tests                                  6     8 list      
2 datasets airmiles      Passenger Miles on Commercial US Airlines, 1937-1960           24     2 ts        
3 datasets AirPassengers Monthly Airline Passenger Numbers 1949-1960                   144     2 ts        
4 datasets airquality    New York Air Quality Measurements                             153     6 data.frame
5 datasets anscombe      Anscombe&#x27;s Quartet of &#x27;Identical&#x27; Simple Linear Regressions    11     8 data.frame
6 datasets attenu        The Joyner-Boore Attenuation Data                             182     5 data.frame
7 datasets attitude      The Chatterjee-Price Attitude Data                             30     7 data.frame
8 datasets austres       Quarterly Time Series of the Number of Australian Residents    89     2 ts   
&#x60;&#x60;&#x60;
Then you narrow down if you are look for data.frame, list etc?. So a function that a) returns a tibble and b) accepts a package(s) as an argument?
---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/26#issuecomment-382300867) on: **4/18/2018**

Concur here too: cool idea! It would also be pretty straightforward to integrate that within [&#x60;flipper&#x60;](https://github.com/ropenscilabs/flipper). The [mooted extension](https://github.com/ropensci/unconf18/issues/25) to [trawling all &#x60;/man&#x60; directories](https://github.com/ropensci/unconf17/issues/78) is technically straightforward, and could very easily include functionality to trawl any &#x60;@docType data&#x60; to enables those to be text-searched, and to group by return type (&#x60;@format&#x60;).
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/26#issuecomment-382907788) on: **4/19/2018**

Cool, yes something similar to what @boshek has,  I started playing a bit just to see what the complications would be.  My basic idea would be to be able to 
1. Search for a data set of a particular type (e.g. data frame, ts, mts, matrix etc)
2. Be able to search (within data frames I guess) for presence of variables with specific classes.
So if you take a package name as an argument get all the information about the data into a tibble and then you&#x27;d be able to say give me all the data frames with a factor.

So this is just a quick script for making a data frame from the core data. I wanted to see what some of the complications would be and they are having spaces + extra words in the Item field and having multiple classes. 

&#x60;&#x60;&#x60;
dataset_list &lt;- data(package&#x3D;&quot;datasets&quot;)
datasets_df &lt;- as.data.frame(dataset_list[[&quot;results&quot;]], stringsAsFactors &#x3D; FALSE)
datasets_df$short &lt;- gsub( &quot; .*$&quot;, &quot;&quot;, datasets_df$Item )

for (i in 1:nrow(datasets_df)){
  dataset_name &lt;- get(datasets_df$short[i])
  # Get the first class name when there is more than one. 
  class_name &lt;- class(dataset_name)
  datasets_df$class[i] &lt;- class(dataset_name)[1]
  datasets_df$n_classes[i] &lt;- length(class(dataset_name))
}
&#x60;&#x60;&#x60;
And then something like the below to get the classes but the question would be how to organize the information to make it most useful.
For example maybe something like a set of logical variables: has_numeric, has_factor, has_logical, has_integer, has_character etc. 
&#x60;&#x60;&#x60;
# Figure out what would work best for people in terms of searching
unlist(lapply(get(datasets_df$Item[i]), class))
&#x60;&#x60;&#x60;
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384119179) on: **4/24/2018**

Love this idea.  Beyond class, it would be helpful to have information about the data types. Often I need several categorical variables, and while I do love the Titanic dataset, some more diversity would be a good thing.  When writing exams I searched through [the Sleuth3 manual](https://cran.r-project.org/web/packages/Sleuth3/Sleuth3.pdf) for particular criteria but it was very time-consuming.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384121916) on: **4/24/2018**

A helpful starting point might be last year&#x27;s project examining data packages on CRAN: https://github.com/ropenscilabs/data-packages.
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384124394) on: **4/24/2018**

@jtr13  That&#x27;s what I mean by class. There are so few ordered factors! So actually it would be good to know the number of each type. E.g. 3 factors, 2 ordered factors,5 numeric.  I agree that it&#x27;s the combinations that get really frustrating.  When you want a simple example  having  to convert types can be a distraction from the main lesson. 

@noamross If packages documented like that it would be cool and we could definitely include in a dashboard.   We could at least provide a url for the description (although we can also try to scrape them).The other thing is packages that wrap APIs for accessing data. The main thing is to make it automated. 

Then maybe if we have a sense of what is there that let&#x27;s us think about what&#x27;s missing. 
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384125492) on: **4/24/2018**

@elinw Got it. When do you use ordered factors? I never do! (This probably isn&#x27;t the right place to discuss this...)
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384125997) on: **4/24/2018**

All those “too much, too little, about right” questions for one …  

Which leads to a whole other set of things.

One of the big issues for me in the base categorical data is that they have it formatted into table classes but I want my students to see them like they are a data frame meaning a more realistic s setting where there are variables of at least two types.

&gt; On Apr 24, 2018, at 8:51 PM, Joyce Robbins &lt;notifications@github.com&gt; wrote:
&gt; 
&gt; @elinw &lt;https://github.com/elinw&gt; Got it. When do you use ordered factors? I never do! (This probably isn&#x27;t the right place to discuss this...)
&gt; 
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub &lt;https://github.com/ropensci/unconf18/issues/26#issuecomment-384125492&gt;, or mute the thread &lt;https://github.com/notifications/unsubscribe-auth/AAuEfUTazsvs9GTAV4Z87zrR3YKNzUbQks5tr8iegaJpZM4TXcvS&gt;.
&gt; 


---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/26#issuecomment-384130194) on: **4/24/2018**

I&#x27;ve never had to use ordered factors for that kind of data for my purposes (usually visualization). I just order the levels of regular factors. 
---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/26#issuecomment-387761649) on: **5/9/2018**

Cool idea! One thought might be that oftentimes, when I&#x27;m looking for a teaching dataset, I&#x27;m looking for the presence of variable relationships in the data, such as smoking status (categorical) vs. BMI (continuous). So could this be another way of classifying the datasets?
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/26#issuecomment-388511681) on: **5/11/2018**

Yes so that&#x27;s what I was trying to say about getting the classes of the variables for the data frames.
https://github.com/elinw/dataestsearch/blob/master/R/datasetsearch.R

Is a concept but not that well coded (loops!! ) ... and it doesn&#x27;t handle getting the variable types for tibbles but it does work for data frames.  I mean this is just a concept but if we have a bunch of people we could make it really nice and figure out what is useful.  
---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/26#issuecomment-388589692) on: **5/12/2018**

Ah, ok, that makes sense. I did something similar with a shiny workshop in identifying variables from a &#x60;data.frame&#x60; so that factor, character, and continuous variables would populate the right dropdowns for any dataset that was loaded into an app. It&#x27;s the same idea as your code: https://github.com/laderast/gradual_shiny/blob/master/03_observe_update/helper.R
