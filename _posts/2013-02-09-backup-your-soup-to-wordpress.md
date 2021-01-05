---
title: "Backup your Soup to Wordpress"
date: 2013-02-09T10:32:14+02:00
layout: post
---

![tiefpunkt's soup mirror](/images/soupexport00.png)

Let’s say you’ve spent a few minutes (or hours, or even days) of your precious lifetime on soup.io, and now you don’t want to loose your work. How would you do this? Thanks to the soup’s RSS export and a nice plugin, it’s fairly easy to copy all the content of your own soup to a WordPress installation. Including all the pictures, of course. So let’s start.

# 1. Download your soup.io RSS export

![soup export link](/images/soupexport01.png)

Login to [soup.io](http://soup.io), and click on "My Soup" in the top left corner. Go to the options, Privacy, and click on "Export (RSS)".

# 2. Install WordPress
Find some webspace, and install [WordPress](http://wordpress.org/). It might work on [wordpress.com](http://wordpress.com/) as well, but I haven’t tested that yet. Let me know if it does.

# 3. Change some PHP settings
*This is optional, there are ways to do it without this step. But it makes it easier.*

Your export might be quite large, and the import will take a while. There are two settings in PHP (and it’s configuration file php.ini) which have an impact on the success of your import. One is [upload_max_filesize](http://php.net/upload-max-filesize), and the other one [max_execution_time](http://php.net/max-execution-time). The first one is responsible for the maximum file size you can upload using PHP. Mine was set to 2M, but my export was larger than that, so I set it to 8M. The second one describes, how long a single PHP script is allowed to run on your server. The default setting was 30, allowing scripts to run for 30 seconds. Depending on the performance of your webserver and your database, as well as the size of your export, the import of the RSS file takes much longer. Fetching the pictures takes a while as well. I set it to 3000, as to not run into any further problems. Just remember to set them back to something reasonable when your done. The file you need to edit on Debian is ``/etc/php5/apache2/php.ini``. Restart your webserver afterwards.

*Alternative:* If you cannot change these settings, you may need to split your export. It is an xml file, with some meta information on the feed, and then a large set of <item> tags, which describe each single post. You can create several smaller files out of your large export, by keeping the stuff around the <item> tags, and just putting a subset of those items into each file.

# 4. Run the import

![install RSS importer](/images/soupexport02.png)

In your WordPress admin panel, go to Tools -> Import and click on RSS. It will ask you to install the importer (Sidenote: It works fine on my WP 3.5.1 installation, despite what the popup says.). Do so.

After it’s installed, open it again, select your export file, and click “Upload file and import”.

This will take a while, but after it’s done, you should be able to see all your soup.io posts in your WordPress installation.

# 5. Get your pictures
Now, you have all your posts locally. But the pictures are still all over at soup. Let’s copy them over. Fortunately, there’s a plugin for that. It’s called [Add Linked Images To Gallery](http://www.bbqiguana.com/wordpress-plugins/add-linked-images-to-gallery/), and you can get it via the Plugin search in your admin panel, or directly from [wordpress.org](https://wordpress.org/extend/plugins/add-linked-images-to-gallery-v01/).

Install and activate the plugin, and then go over to Settings -> Linked IMGs. Press the process button, and get some coffee or tea, as this will take a while.

Once it’s done, all pictures are stored on your server. You have now completed your backup.

# Additional Information
* I also added infinite scrolling to [my soup backup](http://soup.tiefpunkt.com). There’s a plugin for that as well, it’s called “Infinite Scroll”, and you can find it from your admin panel or on wordpress.org
* If you want to keep on souping in your new soup, I suggest you check out my WordPress plugin [mEintopf](https://github.com/meintopf/meintopf). It’s still under heavy development, but should work enough to have some fun with it. Also, take a look at my [blog post](http://tech.tiefpunkt.com/2013/01/your-own-soup-io-an-idea/) about it.
* If you have anything to add, feel free to do so in the comments.


## Comments

* Raphael says 9. February 2013 at 14:04
	<blockquote>
	Das traurige an der Geschichte: Es ist deutlich hübscher als soup.io 😀
	</blockquote>

	* tiefpunkt says 9. February 2013 at 14:11
		<blockquote>
		Vor allem auch schneller 😉
		</blockquote>

* tatonka says 16. February 2013 at 01:05
	<blockquote>
	Jetzt muss ich nur noch warten, bis der RSS wieder online kommt. Ich nutz da ein Script von neingeist (http://bl0rg.net/~neingeist/soup-backup) und hau das mal wiederholend auf die Server, bis es funktioniert.
	</blockquote>


* paul says 8. March 2013 at 12:53
	<blockquote>
	Danke danke danke!
	</blockquote>

* pockpock says 1. April 2013 at 13:41
	<blockquote>
	Der RSS-Importer importiert leider immer alles… Gibt es da auch eine Möglichkeit das inkrementell zu machen?
	</blockquote>

	* tiefpunkt says 10. April 2013 at 10:12
		<blockquote>
		Nicht, dass ich wüsste. Du kannst natürlich immer wieder das RSS-File runterziehen, und alle schon eingefügten Beiträge rausnehmen. Oder du baust den Importer um…
		</blockquote>
