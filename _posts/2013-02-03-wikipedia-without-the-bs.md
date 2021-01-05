---
title: "Wikipedia without the BS"
date: 2013-02-03T10:31:54+02:00
layout: post
---

The german Wikipedia wiki is the second biggest Wikipedia wiki there is. Which is awesome, because if you are looking for some kind of information on pretty much any topic, there is usually something to find in [de.wikipedia.org](http://de.wikipedia.org).

<blockquote class="twitter-tweet">
<p>Es ist wieder offiziell: Das @<a href="https://twitter.com/raumzeitlabor">raumzeitlabor</a> ist irrelevant. <a href="https://t.co/CIMCRud9" title="https://de.wikipedia.org/wiki/Wikipedia:L%C3%B6schkandidaten/24._Dezember_2012#RaumZeitLabor_.28gel.C3.B6scht.29">de.wikipedia.org/wiki/Wikipedia…</a></p>
<p>&mdash; Felix Arndt (@silsha) <a href="https://twitter.com/silsha/status/297743749423984640">February 2, 2013</a></p></blockquote>
<p><script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script></p>

But it is also known for its ridiculously tight rules/decisions on what is relevant or not. These discussions sometimes take quite bizarre forms, as they grow longer than the wiki article itself. A perfect example is the German hackerspace [RaumZeitLabor](http://raumzeitlabor.de),  which has now been [deleted](https://twitter.com/silsha/status/297743749423984640) twice, after more than a [month of discussion](https://de.wikipedia.org/wiki/Wikipedia:L%C3%B6schkandidaten/24._Dezember_2012#RaumZeitLabor_.28gel.C3.B6scht.29) about its relevance for the Wikipedia project (Disclaimer: I am a member of that hackerspace).

One can certainly argue that a hackerspace with less than 100 members is not the most important thing one could look for in a encyclopedia, but on the other hand, a neutral, well written and researched article (which, in my opinion, was certaily true for the article I'm talking about) does not hurt anyone, and can serve people as an (at least somewhat) independent source of information and a good starting point to find more detailed material on a place, person, or topic. It is also a hub for important news, at least if the article is regularly updated.

So let's stop this deletion madness. Well-researched knowledge should be made available, even if it is not “relevant” for a large community. Why ignore the few people, for whom it may be interesting? Who has the right to decide what's important? One could certainly see this as an act of censorship. A lot of potentially interesting and well-written articles may be deleted each day. Sounds to me like we should do something about it.

# What can we do?
Well, there may be a few things. Let's start off by something simple.

## 1. Be a part of the Wikipedia community
I have to admit, I am not. And I am not sure if I would find the time to do so regularly and properly. But this is most certainly the best approach to change the way, the German Wikipedia is governed. Take part in deletion discussions. See what can be done to change their stupid guidelines.

## 2. Fork it
There is a large number of Wikipedia mirrors. This is made possible by dumps, which are made “at the very least monthly and usually twice a month”. Handled in a certain way, these dumps could potentially be used to preserve deleted articles. How?

* Download all available [database dumps](http://dumps.wikimedia.org/dewiki/) (For this method, the ``dewiki-latest-pages-articles.xml.bz2`` files)
* Insert them into your own MediaWiki installation database, in their correct order, without truncating tables before a new dump, but overwriting changes to existing pages.

What does this do?

* It updates pages to the most recent version (or at least the version in the most recent dump file)
* It does not delete articles which have been deleted in the “real” wiki in between two dumps.

This should work (I have yet to try it), but has its shortcomings:

* Dumps are created every 2-4 weeks. Your fork will be somewhat out of date.
* Articles created and deleted between two dumps will be lost.
* There will be no history (at least with the files I chose). Using other dump files, history may be restorable, but more work will have to be done on the files before they can be imported. Also, the size of your fork will be a lot bigger.

Is it worth a try? I think so. If we assume, that articles which are updated often are also seen as relevant enough, they will not be deleted. And deletion discussions for good and interesting articles might take long enough for the article to appear in at least one dump. If you need the editing history of an important, you can always go look at the original.

## 3. Active detection of deletions
If you crawl the deletion discussions, you should be able to recognize, which articles are about to be deleted. Then you can download those and put them in your fork.

This would save much more articles. However, it would be much more work as well. Could be a great addition to number 2.

So I would love to see 2 or 3 in action. Please let me know in the comments if you have done something like that, or plan to do so, or if you have any other idea or criticism.
