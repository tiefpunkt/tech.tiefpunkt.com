---
title: "Missing ESC key on the MacBook Pro Touch Bar"
date: "2021-01-19"
layout: post
---

This is one of those short posts which is kind of like a digital post-it note for me, which might also help you out as well.

Every now and then, the ESC "key" would disappear from the Touch Bar of my MacBook Pro. A bit of googling brought out the solution in a [StackExchange thread](https://apple.stackexchange.com/questions/379627/esc-button-from-touchbar-has-disappeared): You have to restart the Touch Bar server. Takes a few seconds and then everything is back to normal again:

```
sudo pkill TouchBarServer
```
