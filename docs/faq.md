---
layout: default
title: FAQ
nav_order: 4
---

## Table of contents
{: .no_toc}

1. TOC
{:toc}

## What Hardware do I need to run FarmPi?

FarmPi requires a Raspberry Pi that has 64 bit capabilities. A Raspberry Pi 3 and up has this. You'll might need a different Raspberry Pi based on the number of printers you are controlling with it. See [I have # printers, what Raspberry Pi should I use?](#i-have--printers-what-raspberry-pi-should-i-use){:target="_blank"} below.

* Raspberry Pi 3 or 4, based on the number of printers and expected growth.  
  
  If you currently have 15 printers, I would suggest the 4GB Raspberry Pi. This gives you a lot of room for growth.
* Cooling for your Raspberry Pi by using a Fan or heatsinks.
* An Class 10 micro SD card, 8GB or greater.  
  
  More printers and/or a more print history, require a bigger SD card. I would like to suggest a 16GB or 32GB SD card. Don’t go cheap on the SD card, get one of the bigger brands like SanDisk or Kingston.
* A power adapter compatible with your Raspberry Pi.  
  
  The Pi 3 uses a Micro USB connector and the Pi 4 uses an USB-C connector. If available I would like to suggest the original Raspberry Pi adapter.
* An Raspberry Pi case, you can print or buy one.  
  
  The cases for a Pi 3 and Pi 4 are not compatible. Make sure you have the correct case for your Pi
* Ethernet cable and a switch / router where you can plug the other end of the cable in or Wifi.  
  
  An Ethernet cable is more stable than Wifi. Therefore I would like to **strongly suggest** Ethernet over Wifi
* An SD Card reader and, depending on your reader, an adapter.

## Can I run FarmPi and OctoPi on the same Raspberry Pi?

FarmPi and [OctoPi](https://github.com/guysoft/OctoPi){:target="_blank"} are two different Raspberry Pi images. You cannot run two images on the same Raspberry Pi. You'll need an extra Raspberry Pi for FarmPi.

## I am running more OctoPrint instances on a Raspberry Pi than that's in the documentation

We are currently figuring out the limits of a Raspberry Pi vs OctoPrint instances. Please leave a comment on our discussion [#6](https://github.com/mkevenaar/FarmPi/discussions/6){:target="_blank"} so we can take your feedback into account.

## I have # printers, what Raspberry Pi should I use?

Currently we are figureing out the number of OctoPrint instances a Raspberry Pi can handle. The numbers below are a guesstimate. It's better to be on the safe side. For example, if you currently have 18 printers, it would be better to get a Raspberry Pi 4B 4GB than a 2GB.

|  Raspberry Pi  | # of Printers |
|:---------------|:--------------|
| 3A+            | 5             |
| 3B / 3B+       | 10            |
| 4B - 2GB       | 20            |
| 4B - 4GB / 400 | 40            |
| 4B - 8GB       | 80            |

## I cannot find the FarmPi on my network, could you help?

If you are unable to find the IP address in your router's DHCP configuration and you are using Wifi, you probably made a typo in the `farmpi-wpa-supplicant.txt` file. If you are able to do so, attach a screen and a keyboard to check if your Pi has an IP address. This should show up once you login.

## What are the default credentials for FarmPi?

The default login username is `pi` with password `raspberry`. You should change this password to make your Pi secure!

## FarmPi is showing on my network, but farmpi.local does not work

To make `farmpi.local` work, you'll need `bonjour` installed / configured. Have a look at the documentation over [here](https://learn.adafruit.com/bonjour-zeroconf-networking-for-windows-and-linux/overview){:target="_blank"} to get your system setup.

## I want to update to a new version of FarmPi how can I make a backup of my data?

We have created a [guide](./guides/backup-restore.md) for that.

## I have an issue with FarmPi, can you help?

If you have an issue with FarmPi, you can open an issue on [GitHub](https://github.com/mkevenaar/FarmPi/issues){:target="_blank"}. If you have an issue with OctoFarm itself, please join our Discord or open an issue on the OctoFarm [GitHub](https://github.com/OctoFarm/OctoFarm/issues){:target="_blank"}.
