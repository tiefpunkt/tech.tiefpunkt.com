---
title: "Your own soup.io? – An idea."
date: 2013-01-14T10:31:27+02:00
layout: post
---

*tl;dr at the end of the post.*

Let's face it, [soup.io](http://soup.io) is pretty much dead. Yes, it's still breathing, somewhat heavily. But a lot of people are jumping the ship, and moving to Tumblr, or they just stop <del>wasting their time</del> souping around.

I loved soup. I spent hours and hours scrolling and scrolling. I haven't done it as much recently, because it's so slow, and I just can't seem to find the time. But if it were gone, or at least if everyone left, it would be pretty sad. I would definitely miss it. And I have a hard time believing Tumblr is the solution. I have used it for a very different purpose in the past, so for using it as a soup replacement, I would have to either get a new account (which I don't want; too much switching around), or give up the way I currently use it (also not really an option).

So why not build something new?


Because if you look at it closely, what is soup? For a single user, it's a feed reader. And a blog. And some magic to integrate those two together, like easy reposts, or a follower list on your blog. Add some sparkles around it, like /everyone and Groups, and that's pretty much it. Sure, for thousands of users, things get a lot more complex, but if you look at one user alone, that should be all there is. And please correct me if I'm wrong.

So let's take a piece of popular blogging software, like e.g. [WordPress](http://wordpress.org/), attach a feed reader to it, add the magic (sparkles can wait), and there we have it, your very own soup-clone. You can follow your friend's feeds, no matter if they're on Tumblr, still on soup.io, or if they happen to run the same stuff as you do. You can share your content and your reposts with them via your blog and its feeds.

A few hours ago, I talked to [@\_rami\_](https://twitter.com/_rami_/) about this. He happens to have built an open-source feedreader, which you can take a look at over at [geek's factory](http://reader.geeksfactory.de/). I was hoping to use that as a starting point. While he basically told me that that wouldn't work out that well, he called out a few issues and also got me another idea for the feed reader part. But the issues first.

1. Distributed social media foo has a strong tendency to fail \
Well, true story. Diaspora, 12many, … But, I feel that this soup clone does not need the same kind of connectivity between nodes as e.g. a twitter clone would need. So it might be worth a try

2. What about the non-nerds? \
Getting a soup.io account is easy. It's not fast, but at least it's not that complicated. Setting up WordPress however is. It's not rocket science, but it's harder than choosing a nickname and password, and clicking "Yup, I want to join this awesome piece of the interwebs". Nail on the head, again. But maybe we can manage that. You as a tech-savy person can setup a (let's use some Worprass wording here) multisite server, and invite your non-nerd friends.

3. Cost \
Your soup clone might not run on your $2-webspace. Honestly, I have no clue on this one. I don't know what the requirements would be. Let's do it and try.

So while his feed reader wouldn't work, he pointed me to [planet](http://www.planetplanet.org/). Looks neat. But written in Python. I like Python, but that won't integrate with WordPress. Luckily, there's a PHP clone, called [Moonmoon](http://moonmoon.org/). It doesn't cache the feeds, which came to me as quite brilliant. You want to cache all your soup stuff? Well, issue 3 is just having a party.

So let's summarize. We take WordPress, make this Moonmoon into a plugin, create an endless-scrolling dashboard in the admin area with that, add some simple repost magic, and there we have it. Soup-clone v0.1 alpha. I call it "mEintopf".

What do you think? Let me know, in the comments or over on [twitter](https://twitter.com/tiefpunkt/).

**tl;dr**: WordPress + Moonmoon + $magic = Soup.io-clone ? Want to try it? Let me know.

## Comments

* FlowFX says 14. January 2013 at 12:13
	<blockquote>
	Hei tiefpunkt. I feel this is a really neat idea! It closely relates to Johnny Haeusler’s request to create new tools for the web (http://www.spreeblick.com/2012/12/28/2013-das-web-zuruck-erobern/). Making it easy for the non-nerds will be the really hard part, though. As it is with everything.
	<br><br>
	Even a default WordPress installation is not easy to understand for unexperienced users. But let’s see if we can figure it out!
	<br><br>
	I’ll be happy helping with testing and providing user experiences via my non-tech friends. I want this!
	</blockquote>

* Pingback: [Wie geht das eigentlich mit diesem git pull? \| FlowFX](http://flowfx.de/blog/1753/wie-geht-das-eigentlich-mit-diesem-git-pul/)
* Pingback: [Backup your Soup to WordPress \| tiefpunkt tech](http://tech.tiefpunkt.com/2013/02/backup-your-soup-to-wordpress/)

* Marian says 1. March 2013 at 01:02
	<blockquote>
	Wir (paar Leute von http://spline.de/) hatten die Idee, da was mit Tent (https://tent.io/) zu bauen. Das bietet das ja alles (Follow, Repost, …) schon. Sind aber noch nicht weit über die Idee hinaus. (Falls da aber jemand Interesse dran hätte da dran weiterzuspinnen, kann sich ja mal melden, $name@spline.de)
	</blockquote>

	* tiefpunkt says 7. March 2013 at 11:36
		<blockquote>
		Klingt interessant, allerdings auch ein wenig nach einem geschlossenen System. Habt ihr da irgendwo mal Details auf digitales Papier gebracht?
		<br><br>
		Ansonsten gibt es bereits die erste mEintopf Version. Werd ich später wohl endlich mal was drüber schreiben.
		</blockquote>

* Schlingel says 25. March 2013 at 16:12
	<blockquote>
	Hi,
	<br><br>
	ich bin ein ein Software-Dev aus Wien und finde die Idee interessant. Bin zwar mehr bei JS zuhause aber wenn du hier mal ernsthaft anfangen möchtest, lass es mich wissen.
	<br><br>
	Ich könnte zwar nicht jede Woche ein festes Kontingent an Zeit zusagen aber ich kann auf jeden Fall ernsthaft Mitarbeit zusagen.
	<br><br>
	Bei Interesse entweder auf Soup anschreiben (@schlingel) oder Twitter @structerer.
	</blockquote>
