---
author: sandeep
comments: true
date: 2011-06-17 06:39:03+00:00
layout: post
link: http://www.lambdacurry.com/2011/06/does-your-sudo-hang-on-centosfedorarhel-mine-does-too/
slug: does-your-sudo-hang-on-centosfedorarhel-mine-does-too
title: Does your "sudo " hang on Centos/Fedora/RHEL/Debian ? mine does too
wordpress_id: 541
---

Warning: this is for google to index this and help out other poor hapless souls.

If your sudo adduser/passwd/vim , etc. are hanging on any of the Redhat distro variants - its because of [this](https://bugzilla.redhat.com/show_bug.cgi?id=479464) not-a-bug. Apparently, Redhat does a DNS lookup whenever you do a sudo.

This usually happens when you change the hostname incorrectly. The way to fix it is to fix  your _**/etc/sysconfig/network**_

The correct version looks like this


<blockquote>

>     
>     NETWORKING=yes
>     NETWORKING_IPV6=yes
>     HOSTNAME=myname
> 
> 
</blockquote>
