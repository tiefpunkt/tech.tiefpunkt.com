---
title: "MediaWiki backup from the outside"
date: "2021-01-05"
layout: post
---

I decided to put some work into a project with a MediaWiki instance. In the past, one of their websites went off the web, so I wanted to make sure my (and others) work doesn't face a similar fate-

Luckily, MediaWiki has an API, and can be backed up without direct database or shell access to the wiki.

WikiTeam has created a script to backup wikis including media using that API: [dumpgenerator.py](https://raw.githubusercontent.com/WikiTeam/wikiteam/master/dumpgenerator.py) (via [MediaWiki docs](https://www.mediawiki.org/wiki/Manual:Backing_up_a_wiki#Without_shell_access_to_the_server)). It requires python2, and can be setup in a virtual env as follows:
```
virtualenv env
. env/bin/activate
pip install lxml mwclient kitchen
wget https://raw.githubusercontent.com/WikiTeam/wikiteam/master/dumpgenerator.py
```

I've created a little wrapper, which includes backup rotation:
```
#!/bin/bash

URL=$1

DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"

cd $DIR
./env/bin/python dumpgenerator.py --xml --images $URL >/dev/null
if [ $? -eq 0 ]; then
	ls -1dt *-wikidump | sed 1,7d | xargs -r rm -r
else
	date
	echo "error while backing up $URL"
fi
```

You can call this with ``./backup.sh <Wiki URL>``, e.g. ``./backup.sh https://altpwr.net/``.
