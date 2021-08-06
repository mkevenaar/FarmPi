---
layout: default
title: Build environment
parent: Development
nav_order: 2
last_modified_at: 2021-08-06T16:29:03+02:00
---

## Table of contents
{: .no_toc}

1. TOC
{:toc}

## Requirements

- [qemu-arm-static](http://packages.debian.org/sid/qemu-user-static){:target="_blank"}
- [CustomPiOS](https://github.com/guysoft/CustomPiOS){:target="_blank"}
- Downloaded [Ubuntu](https://ubuntu.com/download/raspberry-pi){:target="_blank"} image.
- root privileges for chroot
- Bash
- git
- sudo (the script itself calls it, running as root without sudo won't work)

## Build FarmPi From within FarmPi / Raspbian / Debian / Ubuntu

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

## Building FarmPi Variants

FarmPi supports building variants, which are builds with changes from the main release build. An example and other variants are available in [CustomPiOS, folder src/variants/example](https://github.com/guysoft/CustomPiOS/tree/CustomPiOS/src/variants/example){:target="_blank"}.

docker exec -it mydistro_builder:

```bash
sudo docker exec -it mydistro_builder build [Variant]
```

Or to build a variant inside a container:

```bash
sudo bash -x ./build_dist [Variant]
```

## Building Using Docker

[See Building with docker entry in wiki](https://github.com/guysoft/CustomPiOS/wiki/Building-with-Docker){:target="_blank"}

## Building Using Vagrant

There is a vagrant machine configuration to let build FarmPi in case your build environment behaves differently. Unless you do extra configuration, vagrant must run as root to have nfs folder sync working.

Make sure you have a version of vagrant later than 1.9!

If you are using older versions of Ubuntu/Debian and not using apt-get [from the download page](https://www.vagrantup.com/downloads.html){:target="_blank"}.

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

## Usage

- If needed, override existing config settings by creating a new file `src/config.local`. You can override all settings found in `src/modules/farmpi/config`. If you need to override the path to the Raspbian image to use for building FarmPi, override the path to be used in `ZIP_IMG`. By default the most recent file matching `*-raspbian.zip` found in `src/image` will be used.
- Run `src/build_dist` as root.
- The final image will be created at the `src/workspace`
