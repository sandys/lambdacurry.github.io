---
author: sandeep
comments: true
date: 2009-05-14 09:02:49+00:00
layout: post
link: http://www.lambdacurry.com/2009/05/ati-ixp-ad1981b-thinkpad-r51e-sound-on-jaunty/
slug: ati-ixp-ad1981b-thinkpad-r51e-sound-on-jaunty
title: ATI IXP AD1981B (Thinkpad R51e) sound on Jaunty
wordpress_id: 242
categories:
- linux
- personal
- ubuntu
tags:
- thinkpad
---

This was tough.. so here's a quick list:



	
  * Your sound preferences should look like this:


[caption id="attachment_243" align="alignright" width="150" caption="R51e sound preferences"][![R51e sound preferences](/wp-content/uploads/2009/05/screenshot-sound-preferences.png?w=150)](/wp-content/uploads/2009/05/screenshot-sound-preferences.png)[/caption]



	
  * Your alsamixer should look like this


[caption id="attachment_244" align="alignleft" width="150" caption="R51e alsa preferences"][![R51e alsa preferences](/wp-content/uploads/2009/05/screenshot-alsa.png?w=150)](/wp-content/uploads/2009/05/screenshot-alsa.png)[/caption]
	  
	  
	  
	  
	  
	  
	  
	  




	
  * Install the following




<blockquote>sudo apt-get install asoundconf-gtk gstreamer0.10-alsa libasound2-plugins libesd-alsa0</blockquote>




<blockquote>sudo apt-get install gnome-alsamixer</blockquote>




<blockquote>sudo apt-get install bum</blockquote>





	
  * Your boot-up-manager should look like this (notice the unchecked PulseAudio) die.. pulse.. die!!


[caption id="attachment_245" align="alignright" width="150" caption="R51e boot up manager preferences"][![R51e boot up manager preferences](/wp-content/uploads/2009/05/screenshot-boot-up-manager.png?w=150)](/wp-content/uploads/2009/05/screenshot-boot-up-manager.png)[/caption]

Reboot and enjoy
