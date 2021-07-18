---
layout: default
title: Setup FarmPi
parent: Guides
nav_order: 1
---

## Table of contents
{: .no_toc}

1. TOC
{:toc}

***
:information_source: Make sure you have the correct hardware available. See the [FAQ](../faq.md#what-hardware-do-i-need-to-run-farmpi) for more information.
***

## Where to get it

You'll first need to download the latest available FarmPi image. When running production, please use a stable build.

Download the latest stable build:

[![Stable version](https://img.shields.io/github/v/release/mkevenaar/FarmPi.svg?color=brightgreen&label=version)](https://github.com/mkevenaar/FarmPi/releases/latest){:target="_blank"}

Download the latest stable build (mirror):

[![Stable version (mirror)](https://img.shields.io/github/v/release/mkevenaar/FarmPi.svg?color=brightgreen&label=version)](https://farmpi.octofarm.net/){:target="_blank"}

## How to get started

Once you have downloaded the image, we can start flashing the SD card with our image.

The image comes compressed using the commonly known Zip compression. Most, if not all, of the operating systems have a tool available to extract a Zip archive. I would like to suggest one of the following tools:

* [7-Zip](https://www.7-zip.org/){:target="_blank"} (Windows)
* [The Unarchiver](http://unarchiver.c3.cx/unarchiver){:target="_blank"} (Mac)
* [Unzip](https://linux.die.net/man/1/unzip){:target="_blank"} (Linux)

> :warning: Make sure there isn’t anything on that SD card that you want to save, after flashing all data on that card will be gone!

When you have extracted the image, you can write it. How you write the image to the SD card depends on the operating system you are using. I would like to suggest to have a look at the Official Raspberry Pi documentation for flashing the image.

* [Windows](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md){:target="_blank"}
* [Mac OS](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md){:target="_blank"}
* [Linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md){:target="_blank"}
* [Chrome OS](https://www.raspberrypi.org/documentation/installation/installing-images/chromeos.md){:target="_blank"}

## Configure Wifi (optionally)

> :information_source:  Note: If you intend to connect your Raspberry Pi to your network using an Ethernet cable, you should skip this step. In the case of using Ethernet make sure to connect the UTP cable now.

To make sure your operating system has read the SD card correctly, safely eject the card and insert it again. Your operating system might ask you to format a volume or disk on your SD card. **Do NOT format your SD card volume!** If you did this by accident, you’ll need to go back and flash your SD card again.

Depending on your OS configuration, an File Explorer window might pop up. If it does not show, there should be a volume that is named `boot`. Inside that volume there are a couple of .txt files. One of them is “farmpi-wpa-supplicant.txt” Open this file in a suitable text editor. Suggestions for better text editors are shown on top of the file.

I am assuming your Wifi network is configured with WPA or WPA2. If you are not sure, you should check your router configuration.

Inside the `farmpi-wpa-supplicant.txt` file that you just opened in your editor, you’ll find a section that starts with `##WPA/WPA2 secured`. Remove the hashtag (#) before the four (4) lines underneath that line and edit the ssid (Wifi network name) and psk (Wifi network password) values. Both the SSID and psk should stay surrounded with double quotes (“).

Almost at the bottom, a line with "country=GB" is shown. Change the letters of the country to match your two country letters. In my case this would be “NL”. Check [this](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2){:target="_blank"} list if you are not sure what letters to use.

Once you have changed your settings, save the file and close the editor.

## Booting your Pi

When finished with flashing and your (optional) Wifi configuration, attach you heat sinks and/or your Fan (read the documentation for the fan on how to attach it correctly), insert the Raspberry Pi into your case if you have one and insert the SD card into your Raspberry Pi. If you are using an UTP cable, make sure it’s connected. After that, insert the USB connector of your adapter into your Pi and the adapter in a power outlet. You should wait a couple of minutes before you can continue. The Raspberry Pi is booting and will require some minutes to boot. During first boot the Raspberry Pi will extend its diskspace, create some certificates and keys.

Once the Raspberry Pi is booted and your [network allows it](https://learn.adafruit.com/bonjour-zeroconf-networking-for-windows-and-linux/overview){:target="_blank"}, you can connect to it using [http://farmpi.local](http://farmpi.local){:target="_blank"}. If your network does not allow it, you’ll need to find the IP address in your DHCP server, usually this is your router. Refer to the router documentation to find the DHCP server and the IP address.

If you are unable to find the IP of your Pi, you could attach a HDMI screen with an (micro) HDMI cable and an USB keyboard. You should be able to login to your Pi using the default credentials pi/raspberry.

You should now be able to configure OctoFarm!

## Additional changes

There are some additional changes that I would like to suggest that you should make. The image comes with a default password for the “pi” user: “raspberry” and is set to the GMT time zone. I believe you should change these.

With your favorite SSH tool, connect to your FarmPi machine on the “farmpi.local” address or the IP address you found in your router.

Due to the fact that we are not using a Raspberry Pi OS, the well known tool “raspi-config” is unavailable. We need to make changes manually.

* To change the password type `passwd` and follow the instructions on the screen.
* To change the timezone run `sudo dpkg-reconfigure tzdata` and select the correct time zone for your location.
* Optionally: change the hostname run `echo myhostname | sudo tee /etc/hostname` where myhostname is the new hostname of your Pi, you’ll need to reboot for the changes to take effect using `sudo reboot`.
