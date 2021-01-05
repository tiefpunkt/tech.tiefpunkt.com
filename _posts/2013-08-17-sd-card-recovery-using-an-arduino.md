---
title: "SD card recovery using an Arduino"
date: "2013-08-17"
layout: post
---

[![IMG_0719](/images/IMG_0719-500x375.jpg)](/images/IMG_0719.jpg)

One of my SD card "died" the other day. More specifically, my laptop wouldn't read it anymore, and neither would any other machines or cameras I tried. It did react (looking at the dmesg output), but would only throw errors, and not recognize any partitons on the card. So I decided to try and read it using an Arduino.

All software mentioned here is either included in your Arduino IDE (the CardInfo sketch), or available on [Github](https://github.com/tiefpunkt/arduino_sd_recovery). Feel free to check out some of my other stuff there as well.

### Background

**Attention**: _Dangerous half knowledge ahead_

SD cards have two modes in which they can be accessed. One is the SDIO SD bus mode\*, which is used by your average card reader, your camera, etc. It's fast, and somewhat complicated. The other mode is SPI mode. It's much slower, but it's fairly simple. That's what you use if you connect your SD card to a microcontroller such as an arduino.

### Hardware

[![IMG_0728](/images/IMG_0728-500x375.jpg)](/images/IMG_0728.jpg)

I used a Playduino One Arduino clone (Duemilanove compatible), that I had lying around, and a SD card shield I got from ElectroDragon. Just plugged them together, and ready is your own card reader hardware. I tried it with an Arduino Leonard clone as well, but that did not work. I guess that might be due to a different SPI pin setup, but I didn't investigate further, and instead just went straight for the Playduino.

### Software

I took 3 steps in the recovery process: Grabing the card information using

#### CardInfo

The SD card library in the Arduino IDE contains an example called ``CardInfo``. It connects to the card, and gets information such as size, filesystem type, and a list of files on the card.

[![IMG_0732](/images/IMG_0732-500x375.jpg)](/images/IMG_0732.jpg)

That worked, so I kept going.

#### sd_recovery_files

The sketch ``sd_recovery_files.ino`` tries to iterate over the filesystem, and outputs all files in a HEX encoded format over the serial port. If you save the output to a file on your machine, you can then parse the file using the supplied python script ``parse_files.py``.

[![IMG_0733](/images/IMG_0733-500x375.jpg)](/images/IMG_0733.jpg)

This surprisingly worked for a number of files, but the ``openNextFile()`` function doesn't seem to work all that well, so not all files were copied.

#### sd_recovery_raw

The sketch ``sd_recovery_raw.ino`` reads the SD card block by block, and outputs it in a HEX encoded format over the serial port. You can parse tduemillanovehe output back into a binary file using the supplied ``parse_raw.py`` python script.

This may just take forever, and I have not been successful in using that file, but I have yet to actually copy the entire SD card that way (might take a few days for the 4GB card I have).

I tried sending binary data directly over the serial port, which would have made the entire process much quicker, but that did not work at all.

### Conclusion

[![Screenshot - 08162013 - 01:51:37 AM](/images/Screenshot-08162013-015137-AM-500x361.png)](/images/Screenshot-08162013-015137-AM.png)

So even if no "normal" device reads an SD card anymore, all is not lost. Apparently, the SDIO SD bus interface\* can jump the sharks, without breaking the SPI interface completely. I still managed to get some of my data back, even though the stuff I was interested most in getting back seems gone. I could try to do a full backup of the card using my Arduino card reader, but that would take forever (I estimated about 4 days), since I'm transferring at least twice the necessary amount of data (thanks to the HEX encoding) over a 115200 baud serial line. Now my pictures weren't that important.

Again, if you want to try it for yourself, grab an SD card shield and an Arduino, grab the firmware from my [GitHub Repository](https://github.com/tiefpunkt/arduino_sd_recovery), and give it a shot. Feel free to make adjustments to the code, I'd be glad to try it out.

_\* Updated thanks to some [helpful comments](http://hackaday.com/2013/08/19/rescuing-an-sd-card-with-an-arduino/comment-page-1/#comment-1044477) on [hackaday](http://hackaday.com/2013/08/19/rescuing-an-sd-card-with-an-arduino/)._


## Comments
* Pingback: [Rescuing an SD card with an Arduino](http://hackaday.com/2013/08/19/rescuing-an-sd-card-with-an-arduino/)
* Pingback: [rndm(mod) » Rescuing an SD card with an Arduino](http://randommod.com/2013/08/19/rescuing-an-sd-card-with-an-arduino/)
* Pingback: [Rescuing an SD card with an Arduino - RaspberryPiBoards](http://www.raspberrypiboards.com/rescuing-an-sd-card-with-an-arduino/)
* Pingback: [Rescuing an SD card with an Arduino — Blog of MPRosa](http://www.mprosablog.info/?p=19069)
* Pingback: [Rescuing an SD card with an Arduino \| Daily IT News on IT BlogIT Blog](http://itblog.kubik.ws/rescuing-an-sd-card-with-an-arduino/)
* Shane Trent says 19. August 2013 at 18:27
	<blockquote>
	Very cool work.
	<br>
	Do you think it would be possible to reverse the flow and use the SPI port with a microcontroller to push images on to the SD card?
	<br>
	Combine that with a tiny wireless controller (ElectricImp perhaps) and you could turn any SD card digital picture frame into one that could add pictures from the internet. Just a thought.
	<br>
	-Shane
	</blockquote>

	* tiefpunkt says 19. August 2013 at 22:32
		<blockquote>
		Sure that’s possible. Depending on the size of the image, that’ll take some time, but the library allows you to both read from and write to the SD card. There are a few examples included with the Arduino IDE, just take a look at them, they’ll usually get you pretty far.
		</blockquote>

* Kevin Osborn says 19. August 2013 at 18:50
	<blockquote>
	The openNextFile() problem you mentioned is because you keep allocating new File objects and never close them. If you use just one, and close it after each file, you should be fine. This was also an error in one of the library examples, which I reported, and I think it was fixed, but I haven’t verified.
	</blockquote>

	* tiefpunkt says 19. August 2013 at 22:29
		<blockquote>
		So you mean I use up all the memory on the ATmega, by not closing the File objects? Haven’t thought of that, but it makes a lot of sense.
		But what would be the best way to take care of that then? Have a second variable, assign the returning object from openNextFile() to that, and then close the first?
		</blockquote>

* Ty Tower says 19. August 2013 at 23:35
	<blockquote>
	Hope Kevin answers that
	<br>
	What I want to do is fix the card . They used to cost hundreds and frequently give up.
	Anyone know how to do that?
	Ive got 6 stored
	</blockquote>

* Pingback: [Rescuing an SD card with an Arduino / Cooking Hacks Blog](http://www.cooking-hacks.com/index.php/blog/rescuing-an-sd-card-with-an-arduino/)

* foobar says 20. August 2013 at 14:14
	<blockquote>
	For higher speed you could use an ethernet shield, which by the way comes with a micro sd reader, or an wireless shield.
	</blockquote>

	* tiefpunkt says 25. August 2013 at 17:53
		<blockquote>
		Thought about using a RPi instead next time, since it also has SPI. That might give even more performance.
		</blockquote>

* Robert says 22. August 2013 at 08:02
	<blockquote>
	Nice tutorial.What linux setup are you running?thanks
	</blockquote>

	* tiefpunkt says 25. August 2013 at 17:52
		<blockquote>
		Currently it’s Crunchbang Waldorf, running on Debain unstable. Works fairly well.
		</blockquote>

* Pingback: [Links da semana #3 \| Blog do Sergio Prado](http://sergioprado.org/links-da-semana-3/)

* General Failure says 28. August 2013 at 13:04
	<blockquote>
	Doesn’t work for all issues.<br>
	Tested on a defective (not detected on windows/phone) 32G SDHC (detected as SDHC) and the last message was:<br>
	“Could not find FAT16/FAT32 partition.\nMake sure you’ve formatted the card”.
	</blockquote>

* Da Perl says 1. September 2013 at 23:35
	<blockquote>
	Very cool, but next time use a teensy 3.0. It can do close to 1MB/sec over USB.
	</blockquote>

* alex says 7. September 2013 at 19:09
	<blockquote>
	I had the same problem with my SD card and I bought the same hardware(UNO+SD shield from electrodragon). I thought SD was dead but suddenly cardinfo read the card! My problem now is that when i use parse_files my console freezes… Maybe it’s the problem that you don’t close files and Atmega can’t handle it? I don’t know I’am new with this but now that I found sd isn’t dead I really want to bring back the photos but I can’t..
	</blockquote>

	* al1x says 7. September 2013 at 23:47
		<blockquote>
		sorry, I meant to say when I use sd_recovery_files.ino not parse_files.py
		</blockquote>

* Thomas says 16. September 2013 at 08:31
	<blockquote>
	Hallo,

	wollte gerade eine Mail zu dem Thema an severin (at) tiefpunkt (punkt) de schicken – scheiterte an too many hops.

	Gibts ne andere Möglichkeit dir ne Nachricht mit ein paar Anhängen zukommen zu lassen ?

	Thomas
	</blockquote>

* alex says 18. September 2013 at 01:10
	<blockquote>
	Finally I recovered my photos from SD by binary stream and not HEX. Binary is way faster and does the job easier. No need 2nd program to convert HEX to photo.
	</blockquote>

* Pingback: [Saving Data From Dead SD Cards Using an Arduino! \| labratsgonewild](http://labratsgonewild.com/blog/saving-data-from-dead-sd-cards-using-an-arduino/)

* felix says 10. February 2014 at 07:26
	<blockquote>
	hello no new info how to run from raspberry pi , or teensy ? how to work and make 😉 thank you
	</blockquote>

* mike eddy says 27. March 2014 at 21:23
	<blockquote>
	I successfully copied a jpg file from an SD card via SPI to computer and displayed the image.
	<br><br>
	I used a modified version of the “DumpFile” sketch that comes with the IDE.
	<br><br>
	However, there are caveats. 🙂
	<br><br>
	– ran it on Linux IDE<br>
	– used “picocom” to direct serial interface to a file<br>
	– “touched up” file with “ghex” (hex editor)<br>
	<br>
	Editing the hex was necessary to remove header/trailer messages like “Terminal ready” which either come across the serial interface or are inserted by picocom. The header and trailer are constant strings, so not hard to remove … I just hate the kluge. Should be able to write some python to automate, if I can’t find a setting to avoid.
	<br><br>
	This approach only works one file at a time. But, could be used to rescue individual important files.
	<br><br>
	I have some other ideas … a little success encourages me to proceed.
	</blockquote>

* G Hareesh says 13. June 2014 at 10:50
	<blockquote>
	Please send the details about the Hardware & software which can recover video & still files<br>
	also send the exact cost of the product
	</blockquote>

* timothy says 29. September 2014 at 20:58
	<blockquote>
	great article.. but if there is a tutorial how to use the py file would be very helpful..
	</blockquote>

* Daniel Eaton says 13. October 2014 at 09:29
	<blockquote>
	Nice and interesting article! I more help please, could you help me to recover video as well as still picture.
	</blockquote>

* Philip Booth says 13. October 2014 at 09:32
	<blockquote>
	Wonderful tutorial! Could you tell me which Linex set up are you using?
	</blockquote>

* The Data Hospital says 14. October 2014 at 11:41
	<blockquote>
	Here the SD card recovery process is very informative. At first HEX encoded format data copied and then it is parsed by python script parse_files. py. Very interesting to recovery JPG and text file. Nice interesting article.
	</blockquote>

* Porsche Fans says 27. October 2014 at 11:06
	<blockquote>
	Nice. finally get my old picture with someone <3
	<br><br>
	dude, i want your X201T 🙁<br>
	sorry, miss focus. lol
	</blockquote>
