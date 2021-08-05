# FarmPi

[![Version](https://img.shields.io/github/v/release/mkevenaar/FarmPi.svg?color=brightgreen&label=version)](https://github.com/mkevenaar/FarmPi/releases/latest)
[![Released](https://img.shields.io/badge/dynamic/json.svg?color=brightgreen&label=released&url=https://api.github.com/repos/mkevenaar/FarmPi/releases&query=$[0].published_at)](https://github.com/mkevenaar/FarmPi/releases/latest)
![GitHub Releases (all releases)](https://img.shields.io/github/downloads/mkevenaar/FarmPi/total.svg)
[![Build status](https://img.shields.io/github/workflow/status/mkevenaar/FarmPi/Build%20Image.svg)](https://github.com/mkevenaar/FarmPi/actions/workflows/build.yaml)

<!--ts-->
* [FarmPi](#farmpi)
   * [Where to get it?](#where-to-get-it)
   * [Supported printers](#supported-printers)
   * [How to use it?](#how-to-use-it)
   * [Features](#features)
   * [Developing](#developing)

<!-- Added by: runner, at: Sun Jul 18 18:20:48 UTC 2021 -->

<!--te-->

***
:information_source: I released a blog post with more detailed information. You can find the blog post [here](https://kevenaar.name/farmpi-running-octofarm-on-a-raspberry-pi/)
***

A [Raspberry Pi](http://www.raspberrypi.org/) distribution for 3d printers. It includes the [OctoFarm](http://octofarm.net) software for managing and monitoring multiple Octoprint instances out of the box.

This repository contains the source script to generate the distribution out of an existing [Ubuntu](https://ubuntu.com/download/raspberry-pi) Raspberry Pi distro image.

## Where to get it?

Download the latest stable build:

[![Stable version](https://img.shields.io/github/v/release/mkevenaar/FarmPi.svg?color=brightgreen&label=version)](https://github.com/mkevenaar/FarmPi/releases/latest)

Download the latest stable build (mirror):

[![Stable version (mirror)](https://img.shields.io/github/v/release/mkevenaar/FarmPi.svg?color=brightgreen&label=version)](https://farmpi.octofarm.net/)

Download the latest nightly builds:

[![Nightly version](https://img.shields.io/badge/version-nightly-brightgreen)](https://farmpi.octofarm.net/nightly)

## Supported printers

Currently this table is a guesstimate, once this image is in play for a while, numbers could change

| Raspberry Pi | # of Printers |
|--|--|
| 3A+ | 5 |
| 3B / 3B+  | 10 |
| 4B - 2GB | 20 |
| 4B - 4GB / 400 | 40 |
| 4B - 8GB | 80 |

## How to use it?

> :warning: This image is not running [Raspberry Pi OS](https://www.raspberrypi.org/software/), therefore `raspi-config` is not available

* Unzip the image and install it to an sd card [like any other Raspberry Pi image](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
* Configure your WiFi by editing `farmpi-wpa-supplicant.txt` on the root of the flashed card when using it like a thumb drive, or use an UTP cable
* Boot the Pi from the card
* Log into your Pi via SSH (it is located at `farmpi.local` [if your computer supports bonjour](https://learn.adafruit.com/bonjour-zeroconf-networking-for-windows-and-linux/overview) or find the IP address assigned by your router), default username is "pi", default password is "raspberry".
  * To Change the password; run: `passwd`
  * Optionally: Change the configured timezone; run: `sudo dpkg-reconfigure tzdata`
  * Optionally: Change the hostname; run: `echo myhostname | sudo tee /etc/hostname`

    Your FarmPi instance will then no longer be reachable under `farmpi.local` but rather the hostname you chose postfixed with `.local`, so keep that in mind.

OctoFarm is located at [http://farmpi.local](http://farmpi.local) and also at [https://farmpi.local](https://farmpi.local). Since the SSL certificate is self signed (and generated upon first boot), you will get a certificate warning at the latter location, please ignore it.

## Features

* [OctoFarm](http://octofarm.net) software for managing and monitoring multiple Octoprint instances out of the box
* [Ubuntu](https://ubuntu.com/download/raspberry-pi) Raspberry Pi distro image.

## Developing

Development information has been moved [here](https://farmpi.kevenaar.name/development)

Code contribution would be appreciated!
