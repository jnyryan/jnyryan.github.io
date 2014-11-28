---
layout: post
title:  "VagrantUP: Using virtualization for local development"
date:   2014-11-20 00:00:00
categories: playing-with-technology
description:
tags: [virtualization, design, development]

---

Ever needed a quick local Ubuntu Server for testing? How about a Windows 7 with IE6 for some odd reason. Or a private network with your own gateway, ldap server, domain controller, and clients? That's what VagrantUp provides, a very quick scripted way to bootstrap virtual machines and blow them away when you're done with them!

That's what VagrantUp provides, a way to create virtual machines and networks on your local PC/Laptop for testing and development. It's a great tool that takes the repetitive nature of creating short lived servers and finally gives you an excuse to boost the RAM on your Development Laptop.

##What is VagrantUp?

Simply put, VagrantUp is a wrapper around your virtualization software (e.g. VirtualBox or VMWare Player) that through the **command line interface** and a configuration file will allow a user to:

- download operating system image(s) (and add them to a local library for future use)
- start the operating system or systems
- NAT or Bridge the network to your host system
- forward any ports from your host to the virtual machine(s)
- provision the system (run a script to install software on the virtual machine)
- allow users to SSH, RDP to the virtual machine, or just run it in VirtualBox.

<linebreak>

## How do i get up and running with minimal fuss?

Install the following:

- [VirtualBox](https://www.virtualbox.org/) - free virtualization tool
- [VagrantUp](http://www.vagrantup.com/) - free virtualization management tool

Now to create a virtual machine with the default setup, open a terminal/command window and using command below, you will create a file called ***Vagrantfile*** with a default setup - see [example](https://gist.github.com/jnyryan/390afc62c1de8893b771). There's not much to the file (the example shows lots of options but most are commented out!)

``` bash
vagrant init
```

Now spin up the virtual machine with:

``` bash
vagrant up
```

> That's it!!!

## So what did I just do?

Well you did a few things here, but the net result was you spun up a fresh Ubuntu server that you can ssh to.

``` bash
vagrant ssh
```

In more detail, here's what happened:

- First it will read the Vagrantfile to check what OS **base** image to use and if it cannot find it it it's local library, will download it from the [archive](http://www.vagrantbox.es/) and store it in the ***.vagrant*** folder in the root directory. The default opeating system is ***Ubuntu*** so is you need another you will have to edit the **config.vm.box_url** setting in the Vagrantfile.
- Then the image will be unpacked, the OS started and all ports, network settings, shared folders will be setup.
- Finally VagrantUP will run a provision script if one is available. This will install any software that is needed.

Finally you can stop the VM, or destroy it with the following commands. Halt will suspend it and can be restarted with *vagrant up*. However, destroy will delete it from your host.

``` bash
vagrant halt
vagrant destroy
```

## Real-World Ubuntu example: an nginx server.

The ***Vagrantfile*** and ***install.sh*** scripts below will download an OS image from the URL specified and call it **trusty64** in our local library. Once loaded, VagrantUP will call **install.sh** - which will install *nginx*!

Run it and test it with the following commands.

``` bash
vagrant up
curl http://localhost:8080
```

<script src="https://gist.github.com/jnyryan/ff71b95cac948e6895f2.js"></script>

## Real-World Windows example

Just recently the gnomes at VagrantUP added Windows support, which greatly pleased many in the online community.

Copy the file below to a local folder.

``` bash
vagrant up
vagrant rdp
```
This will bootstrap a windows VM for you and open a RDP session to it. To access it you will need a RDP client such as remote desktop.

<script src="https://gist.github.com/jnyryan/67c6ef727e495934f806.js"></script>

## What else can I do.

Well for starters you can read the API documentation.

Then try to create your own base box!

Enjoy it, it's a great tool and if you have any feedback, comments section below!
