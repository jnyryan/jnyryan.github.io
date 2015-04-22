---
layout: post
title:  "VagrantUP: Creating a custom base image"
date:   2014-11-20 00:00:00
categories: playing-with-technology
description: a guide to creating a base image for Ubuntu on VagrantUp
tags: [virtualization, development]

---
# Vagrant Ubuntu Desktop Server

Create a VagrantUp base image for an ubuntu 14.01.1 Virtual Machine

##Prerequisites

- [Virtual Box](https://www.virtualbox.org/)
- [Vagrant](http://www.vagrantup.com/)
- [Ubuntu ISO](http://www.ubuntu.com/download/desktop/)

## Create a Ubuntu Desktop Server in VirtualBox

The creation of a virtual machine on VirtualBox straight forward. Just start VirtualBox, click **New** and follow the instructions with the following details:

Name and Operating System

- Name: ubuntu-trusty-desktop-64
- Type: Linux
- Version: Ubuntu64

Memory Size

- 2048

Take defaults for the rest

Now click Start the VM, when the machine boots it will ask for a disk image. Select the Ubuntu ISO you downloaded above. Follow all on screen instructions.

Create a new Administrator user called ***vagrant*** with a password of ***vagrant***

The installation process will take a few minutes. Once done and restarted, be sure to run an update to get all the latest patched and updates. The script below will install updates.

``` bash
sudo apt-get update
```

Install [Virtual Box Guest additions](http://www.virtualbox.org/manual/ch04.html#additions-windows)

Customise it in any way you want. The following will install Google Chrome Browser.

``` bash

cd /tmp
wget https://dl.google.com/linux/direct/google-chrome-stable_current_i386.deb
sudo dpkg -i google-chrome-stable_current_i386.deb
```
If an error occurs, run this.
``` bash
sudo apt-get -f install
```
Finally, power down the VM

## Create the Vagrant base

To package a Virtual Machine created in VirtualBox, set the `base` to the NAME of the box in VirtualBox.

```Note``` You may need to be in the location of the VM image for this to work.

``` bash
cd ~/VirtualBox\ VMs/

vagrant package --base ubuntu-trusty-desktop-64 --output ubuntu-trusty-desktop.box
```

Add the box to Vagrants Index

```
vagrant box add ubuntu-trusty-desktop-64 ubuntu-trusty-desktop.box
```

Create a vagrant file if you don't have one already

```
vagrant init ubuntu-trusty-desktop-64
```

## Distribute the VM

Boot the VM

## Test the dsitribution

```
vagrant up jnyryan/ubuntu-trusty-desktop-64 --provider virtualbox
```
