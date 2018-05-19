# [Security/Safety &quot;Best Practices&quot; for rOpenSci Package Developers/Reviewers](https://github.com/ropensci/unconf18/issues/35)

> state: **open** opened by: **hrbrmstr** on: **4/24/2018**

We&#x27;ve done _a bit_ of this ad-hoc, but we _could_ spend some dedicated cycles ensuring that rOpenSci not only has the best technical and maintenance standards — which it _most certainly_ does — but is also the de-facto standard to replicate when considering safety/security.

### Comments

---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/35#issuecomment-384122092) on: **4/24/2018**

How are you thinking about safety/security?  I think this is a great concept.
---
> from: [**karthik**](https://github.com/ropensci/unconf18/issues/35#issuecomment-384123003) on: **4/24/2018**

We discuss this regularly in our staff channels and would be super grateful for your advice/help on this! cc @maelle 
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/35#issuecomment-384158274) on: **4/25/2018**

We&#x27;d like to link to  https://ropenscilabs.github.io/r-security-practices/  whenever it&#x27;s ready. Just sayin&#x27; 👼 
---
> from: [**mmulvahill**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389040337) on: **5/15/2018**

@hrbrmstr I&#x27;m interested in learning more about how to think about security/safety w.r.t. R.  That&#x27;s all I have to add for now 😉 
---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389123065) on: **5/15/2018**

I somehow missed the comment 20d ago @elinw (apologies). https://github.com/hrbrmstr/rpwnd provides some context for the evil one can do with R and https://ropenscilabs.github.io/r-security-practices/ (which  @stephlocke penned and @maelle noted) has a great start for that and other topics.

Packages with embedded other-lang libraries need care &amp; feeding and some way to inform users they are in need of an update. Package authors may be putting vulnerable researchers (some who may not even know they fit that classification) and users in harms way without even knowing it depending on what type of internet calls they make or system traces they leave around. 

We also started work last year on a way to help ensure package download safety (https://ropensci.org/blog/2017/07/25/notary/) but all of us who worked on it have been super busy and even if we weren&#x27;t, it&#x27;s somewhat moot b/c there&#x27;s no backing infrastructure for it nor support in R itself for it (which is where it&#x27;d need to be).

One thing from the &#x60;notary&#x60; work that&#x27;d be an interesting &quot;mandate&quot; from rOpenSci is the requirement that all contributors use PGP and sign all commits and no GH merges or releases happen w/o that. Since R has no way for us to have &quot;developer certs&quot; like Apple or Android have for their apps, and since the package ecosystem is more collaborative in nature, the &quot;everybody PGPs&quot; approach at least provides a better guarantee that we can truly trace commits back to the person and not just the GH account.

In the context of ^^ perhaps one &quot;fun&quot; (I have weird ideas of what constitute that) wld be to get everyone on Keybase at the unconf. I 💙💙💙 what @stephlocke is doing with that in her personal and professional R work and perhaps finishing https://github.com/hrbrmstr/keybase wld be a possible unconf project.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389156795) on: **5/15/2018**

In general, we try to make sure that mandates for RO packages go through a
process that includes internal use, recommendation, good tooling that
reduces effort and good docs/tutorials (not necessarily in that order)
before requiring them. So work that advances any of those would make a
mandate more likely.

&gt;
I&#x27;d be interested in starting with tooling that could add this check (using
**git2r**?)  to both our onboarding checks and our nightly builds, along
with other security best practices (goodpractices 😉).

---
> from: [**elinw**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389160738) on: **5/15/2018**

I’ve been on small projects that tried to mandate PGP and it was really painful and hard to enforce.

It does worry me how much trust a lot of packages put into API calls to download data, both assuming the source must be safe and assuming nothing happens in the space between requestor and requested (e.g. a redirect to a site distributing malware).  I don’t see a lot of validation or sanitizing. 


&gt; On May 15, 2018, at 8:57 AM, Noam Ross &lt;notifications@github.com&gt; wrote:
&gt; 
&gt; In general, we try to make sure that mandates for RO packages go through a
&gt; process that includes internal use, recommendation, good tooling that
&gt; reduces effort and good docs/tutorials (not necessarily in that order)
&gt; before requiring them. So work that advances any of those would make a
&gt; mandate more likely.
&gt; 
&gt; &gt;
&gt; I&#x27;d be interested in starting with tooling that could add this check (using
&gt; **git2r**?) to both our onboarding checks and our nightly builds, along
&gt; with other security best practices (goodpractices 😉).
&gt; —
&gt; You are receiving this because you were mentioned.
&gt; Reply to this email directly, view it on GitHub &lt;https://github.com/ropensci/unconf18/issues/35#issuecomment-389156795&gt;, or mute the thread &lt;https://github.com/notifications/unsubscribe-auth/AAuEfQY8iFu7G90SooS6wmryJqRTCdN1ks5tytDCgaJpZM4TijcH&gt;.
&gt; 


---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389190682) on: **5/15/2018**

Aye. And there&#x27;s &quot;guidance&quot; that might be useful to note in some API packages. For instance, I wrote &#x60;epidata&#x60; to access the economic policy institute data and use the data from it for various classes. Each call out to that API I do from home is logged (Federal requirement and also a side-$-business) by Comcast and searchable by authorities or interested third-parties. They use that data to classify me as a left-leaning activist (when, in fact, I&#x27;m really just a non-affiliated anti-authority anarchist :-) I&#x27;ve seen evidence of that in various mailings, adverts on sites that manage to get through my ad-blocking infrastructure, etc. And, due to a job stint at one of the world&#x27;s largest network providers, I&#x27;ve also maybe even seen said databases. It&#x27;s worse in other countries/regions and many at-risk researchers (again, who don&#x27;t even realize they&#x27;re &#x27;at-risk&#x27;) do not realize they shld be using, say, a VPN for some API calls or using DNS-over-HTTPS or DNSCrypt since DNS leaks where you&#x27;re going.

I&#x27;m not suggesting rOpenSci can solve or provide guidance on all the issues, but we (I say &quot;we&quot; despite working in a rly strange proto-science vs a real one like y&#x27;all) cld definitely up the safety game for those using R.
---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389191822) on: **5/15/2018**

@elinw (re: PGP) aye, is is no panacea and unless you&#x27;re a die heard infosec geek or have a die hard infosec hobby, being religious about PGP configs and use is a pain, especially when setting up new systems. Keybase definitely helps alot and perhaps we (like @noamross was alluding to) cld develop a &quot;safety/security check&quot; package/function similar to &#x60;devtools::dr_devtools()&#x60; or &#x60;goodpractice&#x60; as part of this to help both identify gaps and provide helpers or at least friendly tips on fixing things.
---
> from: [**noamross**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389204809) on: **5/15/2018**

If you want to do live testing of a package, like seeing what system files/folders it modifies, I&#x27;m working on a Dockerized setup for our standard package tests: https://github.com/noamross/launchboat, so one could run tests in an isolated environment before installing.
---
> from: [**boshek**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389215400) on: **5/15/2018**

Oh this is all *so* interesting. After reading about &#x60;notary&#x60; last year and some linked horror stories I try to sign all my commits now. So thanks @hrbrmstr !

It occurs to me that this is related to this [possible project](https://github.com/ropensci/unconf18/issues/54) and in fact may be a key component. It is so easy to build packages/scripts and miss significant security considerations (at least for me) that this area likely has many spaces that could be improved upon. Providing means for reviewers to identify and even just consider that as part of a reviewer suite of tools would likely be useful.


---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389277380) on: **5/15/2018**

@noamross aye. been keeping an 👀 on &#x60;launchboat&#x60; and am also keen to also be watching the network calls pkgs make.
---
> from: [**jennybc**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389286848) on: **5/15/2018**

I&#x27;d appreciate knowing what the most realistic threat model is for the R package ecosystem and how that aligns against various measures to tighten things up.

Example: I am dimly aware of malicious packages in some other language&#x27;s repository that had names very close to the &quot;real&quot; packages. And the Bad People exploited mis-spellings to get users to install and run them. That&#x27;s a really different threat from, say, someone impersonating me and making commits to packages I maintain.

Which threats should we be most worried about and who has to do something to mitigate it?
---
> from: [**batpigandme**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389287635) on: **5/15/2018**

+1 to all of this…
Also, and maybe this is limited audience (or just unrelated), but basic file threat-assessment. Sometimes you&#x27;ve gotta deal with someone else&#x27;s data, and (e.g. with readxl) they have to get it to you some way…
---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389311760) on: **5/15/2018**

That&#x27;s a 👍 point @batpigandme. &quot;Thankfully?&quot; malicious XML and JSON docs are usually targeting browsers and wld have some serious impediments trying to account for various R interpreter environs. Similarly, malicious PDFs are usually targeting Acrobat or Preview or third-party Windows PDF readers. However, the pkgs in the R ecosystem are all using the same core, [vulnerable] libraries so there is room for caution. And, we all get Word docs, Excel docs, PDFs, etc which all have threat vectors.
---
> from: [**hrbrmstr**](https://github.com/ropensci/unconf18/issues/35#issuecomment-389312210) on: **5/15/2018**

@jennybc that&#x27;s definitely a good unconf working-group mind-meld/group convo (since I&#x27;m likely far from the typical R user and cld use some examples of daily use patterns to help with said threat modeling :-)
