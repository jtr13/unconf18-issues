# [Understanding CRAN Incoming](https://github.com/ropensci/unconf18/issues/38)

> state: **open** opened by: **elinw** on: **4/24/2018**

Recently in the Slack channel I semi jokingly suggested creating an app to run a cron job to scrape the incoming folder at CRAN in order to better understand empirically how long packages stay in each state and where they move to and potentially what the bottlenecks are and what the most common kinds of problems are (for example what kinds of Notes are most common and what operating system environments have the most failures and why).  Maybe the CRAN managers already know this, but maintainers don&#x27;t seem to.  Ideally if we had the data we could use it to make suggestions about how to deal with bottle necks or to improve documentation to help people avoid problems or (my pet issue) improve the understandability of notes. 
 

### Comments

---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384158789) on: **4/25/2018**

I non-jokingly think it&#x27;s a cool idea. It&#x27;d also be cool to have a dashboard because currently to find where your package is you need to click in the subfolders right?
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384242586) on: **4/25/2018**

Yes, that&#x27;s right, it&#x27;s kind of annoying that you have to keep trying different folders.
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384263939) on: **4/25/2018**

Possibly related(ish) package: François Michonneau&#x27;s foghorn:
https://github.com/fmichonneau/foghorn .
The aim is different (it reports CRAN Check results), but I think it would be interesting information to integrate…
---
> from: [**hadley**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384278299) on: **4/25/2018**

This is such a good idea that we have already been doing it 😉 

@edgararuiz did all the hard work, and he&#x27;s going to look into sharing our scripts and the data we&#x27;ve collected sofar
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384301018) on: **4/25/2018**

@batpigandme Yes! I saw foghorn and it would be great to integrate some parts,
@hadley @edgararuiz that would be amazing!  I should have suspected you&#x27;d have thought about this.
---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384716264) on: **4/26/2018**

Great idea. 

I&#x27;ll ask, what is probably, a naive question. Is this something that we can work on *with* the folks at CRAN? This amounts to some sort of oversight of CRAN particularly if this took the form of a package. I fully understand the need for this. But I wonder if some communication with the folks at CRAN about this may useful in the long run. 
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384717960) on: **4/26/2018**

When we have something to show them I definitely would do so.  If we find some solve-able bottlenecks I think that could help everyone.

&gt; On Apr 26, 2018, at 1:04 PM, Sam Albers &lt;notifications@github.com&gt; wrote:
&gt; 
&gt; Great idea.
&gt; 
&gt; I&#x27;ll ask, what is probably, a naive question. Is this something that we can work on with the folks at CRAN? This amounts to some sort of oversight of CRAN particularly if this took the form of a package. I fully understand the need for this. But I wonder if some communication with the folks at CRAN about this may useful in the long run.
&gt; 
&gt; —
&gt; You are receiving this because you authored the thread.
&gt; Reply to this email directly, view it on GitHub &lt;https://github.com/ropensci/unconf18/issues/38#issuecomment-384716264&gt;, or mute the thread &lt;https://github.com/notifications/unsubscribe-auth/AAuEfXLID3ZW8_pPHLxo8Df-tX810-DNks5tsf4sgaJpZM4TiqcA&gt;.
&gt; 


---
> from: [**hadley**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384738897) on: **4/26/2018**

@boshek I think that&#x27;s a question best answered in person
---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384768701) on: **4/26/2018**

@hadley I&#x27;ll look forward to it.

@elinw:
&gt; If we find some solve-able bottlenecks I think that could help everyone

Such a great point.
---
> from: [**edgararuiz**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384806168) on: **4/26/2018**

Hi all, I cleaned up and move what I have to this repo: https://github.com/edgararuiz/cran-stages

It includes @hadley &#x27;s diagram that contains our conclusions about the flow.  It also has the data we gathered from the snapshots of the CRAN Incoming folder, scripts you can use to recreate the analysis, and a quick analysis of the data. 
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/38#issuecomment-384809481) on: **4/26/2018**

That&#x27;s fantastic! Lots to think about. 
---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/38#issuecomment-388514319) on: **5/11/2018**

Shouldn&#x27;t it also be possible to scrape the errors and notes packages generate? One of my things is that sometimes making the notes more understandable would make the whole thing less painful.  Or just to have a list of common problems would be helpful.  

