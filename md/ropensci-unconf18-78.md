# [Code of conduct template package + tools/packages for promoting a diverse and welcoming environment](https://github.com/ropensci/unconf18/issues/78)

> state: **open** opened by: **lcolladotor** on: **5/18/2018**

Hi,

I have a simple idea (I think) that could maybe grow into one or more packages/tools.

The initial idea is the following one. I&#x27;ve seen that my co-workers have felt more comfortable and empowered by the code of conduct we have at http://research.libd.org/rstatsclub/#coc that is adapted from http://unconf18.ropensci.org/coc.html. I know that the R Consortium requires code of conducts (based on https://wiki.r-consortium.org/view/R_Consortium_and_the_R_Community_Code_of_Conduct) for activities they sponsor. So I was thinking that it would be useful to have a small package that has a set of code of conduct templates that helps you make your own for your website, conference, event, GitHub repo, etc. The minimal version would be to change the name of the event and the set of emails of those whom participants should contact. I think that if code of conducts were in many more websites that it could help make the community even more welcoming than what it is right now.

From this idea, I thought that it could be expanded a bit more. Some ideas were:

* Maybe something like http://blog.revolutionanalytics.com/2018/03/twitter-bot-or-not.html that predicts if someone is supporting diversity? Could be by inferring a gender ratio of those the account follows. Could be based on language sentiment (is that the right term?) and if the account tweets &quot;angry&quot; stuff or not. Could be a package + shiny app. I mention gender ratio with the idea that if you follow a narrow set of individuals, you will miss out on other perspectives that can potentially influence the way you act. For example, I&#x27;ve seen others call out some types of aggressions that I wasn&#x27;t noticing, which then lead me to ask myself if I was doing them or not. Could be adapted and made useful for helping https://github.com/ropensci/unconf18/issues/57.
* Using the above tool to check how supportive were the tweets from a given conference (by checking a hashtag or a set of hashtags), as a way to help conference organizers identify potential issues that are in conflict with the code of conduct. Here I&#x27;m thinking that it&#x27;s easier to diffuse a situation earlier rather than later.
* A shiny app or tool where others can sign up to help rate as either a tweet is supportive or unsupportive (or other categories). You could use it when you are not sure that your tweet was ok and want to get some feedback from others (probably others wouldn&#x27;t be allowed to see your name/twitter handle) or if you want to study a select number of tweets from a user(s). This could then help inform the model for the first bullet point. This app/tool could be expanded to posts in the rstudio community website or elsewhere -- though it&#x27;s probably best if you can then get the content of the text automatically like you can for tweets.

I&#x27;m thinking about Twitter for several of these because you can get the tweet content programatically. But it could be expanded beyond this. Also, I have some experience with shiny apps and R packages, but not with analyzing tweets, text sentiment and other skills needed for implementing these suggestions. Plus, these are rough ideas and they would need to be polished to make sure that they can be used to promote diversity and a welcoming environment rather than discriminate.

Summary:

* Package or app with code of conduct templates as a way to help disseminate them.
* Discuss other tools (shiny apps? packages?) that could help:
  - predict if a twitter account is diverse/supportive,
  - help check tweets with a given hashtag to identify potential problematic tweets and take action early rather than later (from a conference organizer&#x27;s perspective),
  - use humans to help check tweets&#x27;s supportiveness and generate data that could then help these models.



Best,
Leo

### Comments

