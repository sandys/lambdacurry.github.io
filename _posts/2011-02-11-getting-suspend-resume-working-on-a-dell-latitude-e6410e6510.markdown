---
author: sandeep
comments: true
date: 2011-02-11 07:40:29+00:00
layout: post
link: http://www.lambdacurry.com/2011/02/getting-suspend-resume-working-on-a-dell-latitude-e6410e6510/
slug: getting-suspend-resume-working-on-a-dell-latitude-e6410e6510
title: Getting suspend-resume working on a Dell Latitude E6410/E6510 with Ubuntu
wordpress_id: 514
tags:
- arrandale
- suspend
- ubuntu
---

This has been my BIGGEST problem with the newer kernels. There has been a [bug](https://bugs.freedesktop.org//show_bug.cgi?id=28739) with the Intel Arrandale chipsets, which are causing suspend/resume to break. The problems include blank screen on resume, computer not booting up, etc.  I have a Core I7 Latitude E6410 and I was simply being screwed because of the suspend issue.

There is a temporary [workaround](https://bugs.freedesktop.org//show_bug.cgi?id=28739#c55) posted by Paulo Silva - you need to first install the 2.6.38-rc3 (or rc1/rc2 but NOT rc4) kernel on your machine from [here](http://kernel.ubuntu.com/~kernel-ppa/mainline/v2.6.38-rc3-natty/).


<blockquote>sudo dpkg -i [linux-headers-2.6.38-020638rc3_2.6.38-020638rc3.201102010912_all.deb](http://kernel.ubuntu.com/~kernel-ppa/mainline/v2.6.38-rc3-natty/linux-headers-2.6.38-020638rc3_2.6.38-020638rc3.201102010912_all.deb)

sudo dpkg -i
<table >
<tbody >
<tr >

> <td >[linux-headers-2.6.38-020638rc3-generic_2.6.38-020638rc3.201102010912_amd64.deb](http://kernel.ubuntu.com/~kernel-ppa/mainline/v2.6.38-rc3-natty/linux-headers-2.6.38-020638rc3-generic_2.6.38-020638rc3.201102010912_amd64.deb)
> </td>
</tr>
</tbody>
</table>
sudo dpkg -i [linux-image-2.6.38-020638rc3-generic_2.6.38-020638rc3.201102010912_amd64.deb](http://kernel.ubuntu.com/~kernel-ppa/mainline/v2.6.38-rc3-natty/linux-image-2.6.38-020638rc3-generic_2.6.38-020638rc3.201102010912_amd64.deb)</blockquote>


Reboot.

When you suspend and resume, your screen would be dim - this is because the LCD backlighting is still switched off (unresolved issue). To turn it back on, press Fn+Left-Arrow.

Whew...

**NOTE: **An additional clarification - after resume, if you try to use VLC, the machine crashes with GPU errors. This is easily solved by turning off GPU acceleration in VLC.
