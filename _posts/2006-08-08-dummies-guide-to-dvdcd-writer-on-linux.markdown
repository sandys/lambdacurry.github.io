---
author: sandeep
comments: true
date: 2006-08-08 06:15:09+00:00
layout: post
link: http://www.lambdacurry.com/2006/08/dummies-guide-to-dvdcd-writer-on-linux/
slug: dummies-guide-to-dvdcd-writer-on-linux
title: Dummies Guide to DVD/CD writer on Linux
wordpress_id: 109
categories:
- dvd
- linux
---

After reading countless docs and tutorials, I have been able to get my DVD and CD writer working on an ancient Linux version - Redhat 7.2

Here's the story of my travails:

So basically, to use any CD/DVD writer on Linux, you need to turn on SCSI emulation. This is because the **standard **application - _cdrecord _- works with SCSI drivers **ONLY.**

To get around this problem, you need a wrapper driver called _**ide-scsi **_loaded up and you need to tell your linux kernel to start your CD device in SCSI emulation mode.

First you need to find out which directory in your "/dev" maps to the CD device. Grep for CD, DVD, ATAPI in your /var/log/messages
You should see a line like this


<blockquote>hda: HL-DT-ST DVD+/-RW GWA4164B, ATAPI CD/DVD-ROM drive</blockquote>


So, in your grub.conf append the lines


<blockquote>kernel /bzImage-2.4.32 ro root=/dev/sda7 hdc=ide-scsi hda=ide-scsi</blockquote>


And in your /etc/modules.conf add the lines


<blockquote>alias scsi_hostadapter ide-scsi</blockquote>


It means that the /dev/hda DVD device should now be emulated as scsi (in my case I had another device as SCSI too, ergo the hdc=ide-scsi)
Now reboot.
if you now do a ls -l on your /dev/cdrom, you should be able to see something like


<blockquote>lrwxrwxrwx    1 root     root            9 Jul 26 12:44 /dev/cdrom -> /dev/scd0</blockquote>


Your new SCSI emulated drive is /dev/scd0. Also remember to change appropriate entries in your /etc/fstab (if any).

In addition, you need to have the **_sr.o _**and **_sg.o _**modules loaded - these are to tell the SCSI device to behave as a block device (to write to it).
Try locating _**sr.o **_and **_sg.o _**. If you cannot find it, you may need to build it from your linux source (in /usr/src/linux-2.4 ). Do a **_make menuconfig _** in your linux source and go to **_SCSI support _**. Check **SCSI disk support**<*>, **SCSI tape support** <M>, **SCSI CDROM support**<M>, **SCSI generic support** <M>.  Then do **_make modules _**. The sr.o and sg.o modules should be built.

Add the following lines to your /etc/modules.conf


<blockquote>alias character_scsi sg
alias driver_scsi sr</blockquote>


**NOTE: **sometimes the order of these lines added to /etc/modules.conf is important, if on your next reboot, things dont work then make sure to do modprobe by hand

Now, we need to see if your DVD drive is accessible. Run **_cdrecord -scanbus _**.
You should see something like


<blockquote>Linux sg driver version: 3.1.25
Using libscg version 'schily-0.7'
cdrecord: Warning: using inofficial libscg transport code version (schily - Red Hat-scsi-linux-sg.c-1.75-RH '@(#)scsi-linux-sg.c        1.75 02/10/21 Copyright 1997 J. Schilling').
scsibus0:
0,0,0     0) '' '' '' Disk
0,1,0     1) '' '' '' Disk
0,2,0     2) *
0,3,0     3) *
0,4,0     4) *
0,5,0     5) *
0,6,0     6) *
0,7,0     7) *</blockquote>


This means your CD drive is working fine. Note that you might have to be root to run **_cdrecord _**at this time, we will change that shortly.

Now, as far as CD writing goes, you are good to go - there are a million docs on that (my favorite is at [Yolinux](http://yolinux.com/TUTORIALS/LinuxTutorialCDBurn.html))
I first create an ISO using **_mkisofs _**and then I usually do


<blockquote>cdrecord -v -speed=2  RedHat-7.0-i386-powertools.iso</blockquote>


About DVD writers - now there is a commercial version of cdrecord called **_cdrecord-prodvd _**which has a lot of funky licenses and is not opensource. It also has a lot of features. But the thing I use and has worked for burning a lot of DVD's is **_growisofs_**. This is opensource and developed by [Andy Polyakov of Chalmers.](http://fy.chalmers.se/~appro/linux/DVD+RW/) I compiled and built it on my machine.
I usually do


<blockquote>growisofs -dvd-compat -speed=2 -Z /dev/<name_of_dvd_device> -R -J -pad /dir-path/file1</blockquote>


Now, it so happens that the DVD device on my machine used to be unwritable(by anyone except root) as soon as a DVD was put in it - the culprit was the file **_/etc/security/console.perms_**. This changed the permissions to read-only as soon as something was put in.
I changed a line


<blockquote><console>  0600 <cdrom>      0660 root.disk</blockquote>


And everything was fine.

Whew.. hope that helps.

del.icio.us Tags: [linux](http://del.icio.us/sss8ue/linux) [dvd](http://del.icio.us/sss8ue/dvd)
