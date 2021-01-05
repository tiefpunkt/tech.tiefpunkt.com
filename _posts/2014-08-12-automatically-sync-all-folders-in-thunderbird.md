---
title: "Automatically sync all folders in Thunderbird"
date: "2014-08-12"
layout: post
---

Man, that had been annoying me for years. To access my emails, I use Thunderbird and IMAP (no Gmail). I also make extensive use of server side email filtering/sorting. It took a while to set up, due to the interface my email hoster uses, but it works like a charm. The only annoyance was that Thunderbird only ever synced my main Inbox folder, not all subfolders. So I had to go through them manually to check for new email.

Today, I finally set out to find a solution to this, and I was surprised how little of an issue that actually was. Turns out, there's a flag in Thunderbird's extended configuration, that let's you enable automatic sync of all folders.

So what did I do? Start up Thunderbird, open the [Config Editor](https://support.mozilla.org/en-US/kb/config-editor) (Tools -> Options -> Advanced -> General -> Config Editor), and change the `mail.server.default.check_all_folders_for_new` setting to `true`.

And that was it. No more going-through-all-folders. I don't know how many hours I would have saved if I'd done that earlier.

Source of the solution was a [KB article on mozillaZine](http://kb.mozillazine.org/How_do_I_check_for_new_messages_in_other_folders).
