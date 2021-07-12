---
layout: default
title: FAQ
nav_order: 4
---

## Table of contents
{: .no_toc}

1. TOC
{:toc}

## Can I run FarmPi and OctoPi on the same Raspberry Pi?

FarmPi and [OctoPi](https://github.com/guysoft/OctoPi) are two different Raspberry Pi images. You cannot run two images on the same Raspberry Pi. You'll need an extra Raspberry Pi for FarmPi.

## I am running more OctoPrint instances on a Raspberry Pi than that's in the documentation

We are currently figuring out the limits of a Raspberry Pi vs OctoPrint instances. Please leave a comment on our discussion [#6](https://github.com/mkevenaar/FarmPi/discussions/6) so we can take your feedback into account.

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

## I want to update to a new version of FarmPi how can I make a backup of my data?

We have created a [guide](./guides/backup.md) for that.

## I have an issue with FarmPi, can you help?

If you have an issue with FarmPi, you can open an issue on [GitHub](https://github.com/mkevenaar/FarmPi/issues). If you have an issue with OctoFarm itself, please join our Discord or open an issue on the OctoFarm [GitHub](https://github.com/OctoFarm/OctoFarm/issues).
