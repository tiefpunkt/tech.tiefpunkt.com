---
title: "MySQL query log"
date: 2013-02-10T10:32:57+02:00
layout: post
---

So I was doing some work on mEintopf last night, and wanted to see, if my changes to SQL queries made it to the MySQL database or whether they got stuck somewhere in the WordPress framework. Turns out you can enable and disable query logging in MySQL with two simple SQL commands.

```
SET GLOBAL general_log_file = '/tmp/mysql.log';
SET GLOBAL general_log = 'ON';
```

The first one sets the location of your log file, and the second enables logging. Now, just do a ``tail -f /tmp/mysql.log``  to see all queries coming to your RDBMS.

Once you’re done, don't forget to disable it again.

```
SET GLOBAL general_log = 'OFF';
```
