---
title: "Firefox debugging"
date: 2013-02-10T10:32:40+02:00
layout: post
---

Just lost my Firefox session after a restart. Apparently, it had problems parsing the ``sessionstore.js`` file. While I didn’t fix that problem, I found out how to get firefox to be much more verbose about what it does. You have to set an environment variable, and then firefox will spit out a whole lot more on the console than it usually does.

```
tiefpunkt@tiefpunkt ~ $ export NSPR_LOG_MODULES=all:5
tiefpunkt@tiefpunkt ~ $ firefox > stdout.log 2> stderr.log
```
