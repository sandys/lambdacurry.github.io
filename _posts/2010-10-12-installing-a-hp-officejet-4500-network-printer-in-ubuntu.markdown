---
author: sandeep
comments: true
date: 2010-10-12 09:12:14+00:00
layout: post
link: http://www.lambdacurry.com/2010/10/installing-a-hp-officejet-4500-network-printer-in-ubuntu/
slug: installing-a-hp-officejet-4500-network-printer-in-ubuntu
title: Installing a HP Officejet 4500 Network Printer in Ubuntu
wordpress_id: 436
tags:
- '4500'
- hp
- hplip
- officejet
- ubuntu
---

Download the latest version of HPLIP from [http://sourceforge.net/projects/hplip/files/](http://sourceforge.net/projects/hplip/files/) (forget the ubuntu standard repository)

Preferably set the printer to a static IP (using the small display and some tiresome typing)

Install the following packages:


<blockquote>python-qt4 python-qt4-dbus libsnmp-dev libsane-dev libcups2-dev libusb-dev python-dev</blockquote>


Run the _hplip-x.xx.xx.run _from the commandline. Choose the automatic install option.

When the installation is complete and the automatic configuration window pops up, set it to pick up the ip address of the printer (I think you have to click the "_advanced_" button for that). Click "_next_" till you are done.

The system administration "Printing" option is junk for installing a HP printer, even if you give it the IP address or whatever. I think it is due to the difference in "Device URI" which in my case ought to be "_**hp:/net/Officejet_4500_G510g-m?ip=192.168.1.219**_"
