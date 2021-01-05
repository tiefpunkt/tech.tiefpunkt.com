---
title: "Pushing Mediawiki-powered Wikis to Github"
date: 2013-01-13T10:15:46+02:00
layout: post
---

Just yesterday, I set up a cronjob to regularly push the [RaumZeitLabor wiki](http://raumzeitlabor.de/wiki) to GitHub. Why? Because people wanted to search and aggregate the wiki like they would with normal text files. And because I like GitHubs repository graphs and wanted to use them for the wiki as well.

# Installation

So lets get to it. I used [Git-Mediawiki](https://github.com/Bibzball/Git-Mediawiki/wiki) for the job, which allows you to interact with a MediaWiki-installation just like a normal git repository. The installation is pretty easy (I'm using Debian Testing):

```
sudo apt-get install libmediawiki-api-perl libdatetime-format-iso8601-perl make
wget -O Makefile "https://git.kernel.org/?p=git/git.git;a=blob_plain;f=contrib/mw-to-git/Makefile;hb=HEAD"
wget -O git-remote-mediawiki "https://git.kernel.org/?p=git/git.git;a=blob_plain;f=contrib/mw-to-git/git-remote-mediawiki;hb=HEAD"
sudo make install
```

# Working with your wiki

That was it with the installation. Now you can clone a wiki like so:

```
git clone mediawiki::http://raumzeitlabor.de/w ~/wiki
```

Be careful, as this is usually not the URL you see when browsing the wiki, but the path you see when doing edits or similar operations on your wiki.

![Wrong path](/images/wiki_path01.png)
*Wrong path*

![Correct path](/images/wiki_path02.png)
*Correct path*

To update your repository to the current state of the wiki, use

```
git pull --rebase
```

# Automation

In the given scenario, the github repo was supposed to be updated regularly.

To do this, a deploy key pair for GitHub was needed.

```
tiefpunkt@tiefpunkt:~$ ssh-keygen -t rsa -C "wiki_deploy_key@tiefpunkt.vm.rzl"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/tiefpunkt/.ssh/id_rsa): /home/tiefpunkt/wiki_deploy_key
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/tiefpunkt/wiki_deploy_key.
Your public key has been saved in /home/tiefpunkt/wiki_deploy_key.pub.
```

The public key of this key pair was then added to the GitHub repository.

![Github deploy key](/images/github_deploy_key.png)

A custom SSH host was used to incorporate the key file. This was done in ``.ssh/config``

```
Host wiki.gh
Hostname github.com
User git
IdentityFile ~/wiki_deploy_key
```

Initializing the git repository may take a while, depending on the size of your wiki. Don't try Wikipedia.

```
tiefpunkt@tiefpunkt:~$ git clone mediawiki::http://raumzeitlabor.de/w ~/wiki
... Lots of text ...
tiefpunkt@tiefpunkt:~$ cd wiki
tiefpunkt@tiefpunkt:~/wiki$ git remote add github wiki.gh:raumzeitlabor/wiki.git
tiefpunkt@tiefpunkt:~/wiki$ git push github master
The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,207.97.227.239' (RSA) to the list of known hosts.
Everything up-to-date
```

The actual update script is pretty short.

```
#!/bin/sh
cd /home/tiefpunkt/wiki
git pull --rebase
git push github master
```

Don't forget to make it executable.

Last but no least, a cronjob was scheduled to run that script once a day.

```
tiefpunkt@tiefpunkt:~$ crontab -e
no crontab for tiefpunkt - using an empty one

0 0 * * * /home/tiefpunkt/update-wiki.sh >> /home/tiefpunkt/update-wiki.log 2>>&1

crontab: installing new crontab
```
