---
title: "ThinkVantage key to lock your screen under Windows 7"
date: "2013-03-19"
layout: post
---

At home, I use Debian on my ThinkPad, and have remapped the ThinkVantage key on top of the keyboard to lock my screen. It's just a single press of a button, and it makes you feel a little safer if you have your laptop standing in a semi-public space.

At work, I also have a ThinkPad, but with Windows 7 on it. Now, I wanted the same functionality on there as well. I tried doing so using AutoHotkey, but that would not recognize the key press. So some digging got me to the following solution:

1. Create a small batchfile, let's say under "C:\\lock.bat", with the following contents:

    ```
    @echo off
    rundll32 user32.dll, LockWorkStation
    ```

2. In you registry, create (I had to do so, along with the directory) or change the following key:

   ```
    [HKEY_LOCAL_MACHINE\SOFTWARE\IBM\TPHOTKEY\8001]
    "File"="c:\\lock.bat"
   ```

    Make sure, the path matches the path to the file you created. Every backslash is converted into two backslashes.

And there you have it. For me, it worked right away. No reboot, no logging in again, it just worked immediately.


### Comments
* Thomas Vanhoutte says 28. May 2013 at 16:41
    <blockquote>
    Hi
    <br>
    I have a Lenovo Carbon X1 and I was trying to do something similar with the ThinkVantage key.
    However, you method does not seem to work for me, not even after a reboot.
    The bat file, of course, works perfectly when executing. So it’s the ThinkVantage key that does not seem to open the .bat file.
    <br>
    Any ideas?
    I was wondering if the ThinkVantage software should be installed or not?
    <br>
    Thanks for your help!
    <br>
    PS: You can also e-mail me on the given e-mail address 🙂
    </blockquote>


* Larry Standage says 26. September 2013 at 21:20
    <blockquote>
    Under just about all versions of Windows there is an easy way to lock the screen. Hold down the Windows key and press ‘L’. That locks the screen. Granted, its a two-button press…
    </blockquote>

* Thomas says 28. October 2013 at 15:17
    <blockquote>
    It’s not about locking it, I would use it for opening another application.
    </blockquote>
