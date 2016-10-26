---
author: admin
comments: true
date: 2015-01-06 12:34:32+00:00
layout: post
link: http://www.lambdacurry.com/2015/01/creating-fedora-21-liveusb-ubuntu-14-04/
slug: creating-fedora-21-liveusb-ubuntu-14-04
title: Creating  a Fedora 21 LiveUSB in Ubuntu 14.04
wordpress_id: 917
---

Sadly, Ubuntu's startup disk creator does not allow you to create fedora images.

The **officially **sanctioned way to create a fedora liveusb in ubuntu is the following:


<blockquote>`sudo aptitude install isomd5sum python-parted python-pyisomd5sum python-urlgrabber extlinux python-qt4 python-qt4-dbus tar udisks libudisks2-dev`

`git clone https://github.com/lmacken/liveusb-creator.git`

`sudo ./liveusb-creator`</blockquote>
