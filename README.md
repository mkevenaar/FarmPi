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
      * [Requirements](#requirements)
      * [Build FarmPi From within FarmPi / Raspbian / Debian / Ubuntu](#build-farmpi-from-within-farmpi--raspbian--debian--ubuntu)
      * [Building FarmPi Variants](#building-farmpi-variants)
      * [Building Using Docker](#building-using-docker)
      * [Building Using Vagrant](#building-using-vagrant)
      * [Usage](#usage)

<!-- Added by: runner, at: Fri Jul 16 09:40:06 UTC 2021 -->

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

- Unzip the image and install it to an sd card [like any other Raspberry Pi image](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
- Configure your WiFi by editing `farmpi-wpa-supplicant.txt` on the root of the flashed card when using it like a thumb drive, or use an UTP cable
- Boot the Pi from the card
- Log into your Pi via SSH (it is located at `farmpi.local` [if your computer supports bonjour](https://learn.adafruit.com/bonjour-zeroconf-networking-for-windows-and-linux/overview) or find the IP address assigned by your router), default username is "pi", default password is "raspberry".
  - To Change the password; run: `passwd`
  - Optionally: Change the configured timezone; run: `sudo dpkg-reconfigure tzdata`
  - Optionally: Change the hostname; run: `echo myhostname | sudo tee /etc/hostname`

    Your FarmPi instance will then no longer be reachable under `farmpi.local` but rather the hostname you chose postfixed with `.local`, so keep that in mind.

OctoFarm is located at [http://farmpi.local](http://farmpi.local) and also at [https://farmpi.local](https://farmpi.local). Since the SSL certificate is self signed (and generated upon first boot), you will get a certificate warning at the latter location, please ignore it.

## Features

- [OctoFarm](http://octofarm.net) software for managing and monitoring multiple Octoprint instances out of the box
- [Ubuntu](https://ubuntu.com/download/raspberry-pi) Raspberry Pi distro image.

## Developing

### Requirements

- [qemu-arm-static](http://packages.debian.org/sid/qemu-user-static)
- [CustomPiOS](https://github.com/guysoft/CustomPiOS)
- Downloaded [Ubuntu](https://ubuntu.com/download/raspberry-pi) image.
- root privileges for chroot
- Bash
- git
- sudo (the script itself calls it, running as root without sudo won't work)

### Build FarmPi From within FarmPi / Raspbian / Debian / Ubuntu

FarmPi can be built from Debian, Ubuntu, Raspbian, or even FarmPi.
Build requires about 2.5 GB of free space available.
You can build it by issuing the following commands:

```bash
sudo apt-get install gawk util-linux qemu-user-static git p7zip-full python3

git clone https://github.com/guysoft/CustomPiOS.git
git clone https://github.com/mkevenaar/FarmPi.git
cd FarmPi/src/image
wget -c --trust-server-names 'https://cdimage.ubuntu.com/releases/20.04/release/ubuntu-20.04.2-preinstalled-server-arm64+raspi.img.xz'
cd ..
../../CustomPiOS/src/update-custompios-paths
sudo modprobe loop
sudo bash -x ./build_dist
```

### Building FarmPi Variants

FarmPi supports building variants, which are builds with changes from the main release build. An example and other variants are available in [CustomPiOS, folder src/variants/example](https://github.com/guysoft/CustomPiOS/tree/CustomPiOS/src/variants/example).

docker exec -it mydistro_builder:

```bash
sudo docker exec -it mydistro_builder build [Variant]
```

Or to build a variant inside a container:

```bash
sudo bash -x ./build_dist [Variant]
```

### Building Using Docker

[See Building with docker entry in wiki](https://github.com/guysoft/CustomPiOS/wiki/Building-with-Docker)

### Building Using Vagrant

There is a vagrant machine configuration to let build FarmPi in case your build environment behaves differently. Unless you do extra configuration, vagrant must run as root to have nfs folder sync working.

Make sure you have a version of vagrant later than 1.9!

If you are using older versions of Ubuntu/Debian and not using apt-get [from the download page](https://www.vagrantup.com/downloads.html).

To use it:

```bash
sudo apt-get install vagrant nfs-kernel-server virtualbox
sudo vagrant plugin install vagrant-nfs_guest
sudo modprobe nfs
cd ../FarmPi
git clone https://github.com/guysoft/CustomPiOS.git
cd FarmPi/src
../../CustomPiOS/src/update-custompios-paths
cd FarmPi/src/vagrant
sudo vagrant up
run_vagrant_build.sh
```

After provisioning the machine, its also possible to run a nightly build which updates from devel using:

```bash
cd FarmPi/src/vagrant
run_vagrant_build.sh
```

To build a variant on the machine simply run:

```bash
cd src/vagrant
run_vagrant_build.sh [Variant]
```

### Usage

- If needed, override existing config settings by creating a new file `src/config.local`. You can override all settings found in `src/modules/farmpi/config`. If you need to override the path to the Raspbian image to use for building FarmPi, override the path to be used in `ZIP_IMG`. By default the most recent file matching `*-raspbian.zip` found in `src/image` will be used.
- Run `src/build_dist` as root.
- The final image will be created at the `src/workspace`

Code contribution would be appreciated!

