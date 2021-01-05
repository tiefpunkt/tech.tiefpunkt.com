---
title: "Headless RaspberryPi 2 installation with Raspbian Jessie"
date: "2015-06-02"
layout: post
---

Last night, I wanted to setup my new RaspberryPi 2. I don't have a TV, and also no spare monitor with HDMI around the appartment, so it had work without it. I ran into an issue with the Raspbian update to Jessie, so here's how to avoid that.

1. Download the Raspbian image from the [Raspberry Pi Foundation](https://www.raspberrypi.org/downloads/). You'll have to extract it and write it to your Micro SD card. That's pretty well explained in their [documentation](https://www.raspberrypi.org/documentation/installation/installing-images/README.md), so I will let you read that. Unfortunately, the image  is based on Raspbian Wheezy, so we'll have to update to Jessie by ourselves later.
2. Put the flashed SD card into your Raspberry Pi 2, connect a network cable to it, and power it up.
3. I used SSH to connect to my newly booted RPi. To do that, you need to find out its IP address. The simplest way for me was to log into my router, and get a list of all connected computers. Your RPi will have the hostname "raspberrypi".
4. Login with SSH (Linux or OS X, for Windows use a client like PuTTy):

    ```sh
    ssh pi@<IP address>
    ```

    You'll be asked for a password. Use raspberry .
5. Run through the configuration wizard, which you can start with the following command:

    ```sh
    sudo raspi-config
    ```

    Importantly, expand your file system, and set a new password.
6. It's time to update to Jessie. To do that, you need to adjust Raspbian's sources lists. You can do so manually, by replacing "wheezy" in `/etc/apt/sources.list` and all files in the `/etc/apt/sources.list.d/` directory with "jessie" using an editor like `vi`  or `nano` , or just use the following to commands.

    ```sh
    sudo sed -i 's/wheezy/jessie/g' /etc/apt/sources.list
    sudo sed -i 's/wheezy/jessie/g' /etc/apt/sources.list.d/\*
    ```

    Now, update your package list:

    ```sh
    sudo apt-get update
    ```

    and start the upgrade to Raspbian Jessie:

    ```sh
    sudo apt-get dist-upgrade
    ```

    You'll be asked a few times whether you want to replace certain files with newer versions. I did confirm all those with "y", but feel free to check the actual changes and decide on each individually.

7. Now to the thing that kept me up a few hours longer than I planned. You'll have to reboot after the update (because the init system changed during the update, which means Raspbian starts programs a bit differently with the new version). However, some part of the upgrade does not clean up properly after itself, and leaves you with some files that will stop the RPi from booting properly, and not letting you login via SSH after a reboot. To avoid that problem, run the following command before issuing the reboot:

    ```sh
    sudo apt-get purge cgroup-bin
    ```

    There's a [bug report](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=785484) with Debian on the issue, if you want to get more details. If you already rebooted, like I did, there's a way to recover. Unplug your RPi, put the SD card into a linux machine, and delete the file `/etc/init.d/cgroup-bin`  from its file system (make sure you remove it on the SD card, not your local system). Afterwards, your RPi should boot properly again, and you can run the above command to clean up properly. In this case, no need to reboot again.

8. Reboot your Raspberry Pi to apply the new init system

    ```sh
    sudo reboot
    ```
