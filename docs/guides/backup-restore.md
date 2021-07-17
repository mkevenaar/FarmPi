---
layout: default
title: Backup/Restore MongoDB
parent: Guides
nav_order: 1
---

## Table of contents
{: .no_toc}

1. TOC
{:toc}

***
:information_source: This should also work migrating from another OctoFarm instance to FarmPi or the other way around.
***

## Creating a backup

For creating a backup, we are going to use the [MongoDump](https://docs.mongodb.com/database-tools/mongodump/) tool. This tool is installed by default on your FarmPi.

To create a backup you first need to login to your Raspberry Pi using [SSH](ssh.md). You'll find the default credentials in the [FAQ](../faq.md#what-are-the-default-credentials-for-farmpi)

Once logged in, you should stop OctoFarm. To do this, enter the OctoFarm and stop OctoFarm. Execute these commands:

```bash
cd OctoFarm
npm stop:delete
```

There should be a message in **red**{: style="color: red"} saying that it's **stopped**{: style="color: red"}

We now can crate the dump. To create the dump, execute this command:

```bash
mongodump --archive=/home/pi/octofarm.archive
```

This command creates an export of all the databases into the `octofarm.archive` file. This file contains all the data required to restore the database.

## Transter to your local machine

For transferring the dump, we are going to use `scp` (Secure CoPy). This tool allows us to transfer files from and to another linux machine, like the FarmPi. There are also other tools available like [WinSCP](https://winscp.net/) (Windows, Free) or [Cyberduck](https://cyberduck.io/) (Windows / MacOS, Free)

I am assuming you have followed the directions shown in the [SSH](ssh.md) documentation. If you have done that correctly, these commands should work.

From a shell (Powershell, Terminal, CMD), enter a folder (using `cd`) where you want to store the file. For example your Desktop. If this is the target

```bash
scp pi@farmpi.local:octofarm.archive .
```

You could replace `farmpi.local` in the command above to the IP of your FarmPi or the source machine.

If you get an message asking to confirm the host key and continue connecting, type `yes` and press enter.

You should now enter your password. The transfer will now start.

## Transfer to the target

> :warning: Make sure the target FarmPi machine is accessable. This would probable be by reflasing the image and booting it up, but can be different on your environment.  
You'll need to make sure that the installation wizard for OctoFarm shows in your browser.

To transfer the file back to your new image, execute the following command.

```bash
scp octofarm.archive pi@farmpi.local:
```

You could replace `farmpi.local` in the command above to the IP of your FarmPi or the source machine.

If you get an message asking to confirm the host key and continue connecting, type `yes` and press enter.

You should now enter your password. The transfer will now start.

If you have used the same hostname, you will most likely recieve an error message stating that the host key is changed. This is expected, there is no man in the middle attack or anything. The host keys on the FarmPi image are generated at first boot and therefore unique on each image.

If this happens for you, open the `known_hosts` file that is shown in the message in your favorite editor (Notepad++, vim, or any other tool) and remove the line thats shown in your error message, save the file and try again.

## Restoring a backup

SSH into your new FarmPi image, using the same method when you created your backup before and stop OctoFarm again.

After stopping OctoFarm, you can restore your backup. To restore your backup, run the following commands:

```bash
mongorestore --archive=/home/pi/octofarm.archive
```

Depending on the size of your database, this can take a while.

Once the import is completed, you should make sure you are inside the OctoFarm folder and start OctoFarm again using these commands:

```bash
cd ~/OctoFarm/
npm run start
```
