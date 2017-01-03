---
author: admin
comments: true
date: 2014-10-19 20:09:54+00:00
layout: default
link: http://www.lambdacurry.com/systemd-nice-dont-afraid/
slug: systemd-nice-dont-afraid
title: systemd is nice. Dont be afraid.
wordpress_id: 889
---

# The "WMD" argument


Most of the arguments against systemd are up-in-the-air, monsters-under-the-bed variety. Sound familiar ?

When a noisy minority takes the help of social media and makes a lot of noise of "how Linux is being destroyed by Lennart", it sounds all too familiar.


# What is the Unix way ?


What is the Unix way ? Is Mac OSX the Unix way ? _launchd _- the init system for OSX behaves very similarly to systemd.

Some people say that the unix way is to not have too many functionality in one binary. In fact a popular statment that I have heard is "_To Lennart - In Unix, each program should implement only a very small, managable set of feature, whereas your projects are usually bloated with functionality_". If you build systemd with all configuration options enabled you will build 69 individual binaries. So is it still non-unixy ? Where is it bloated ?

![http://www.linux.com/images/stories/41373/Systemd-components.png](http://www.linux.com/images/stories/41373/Systemd-components.png)

Or is the unix way about choice - That one should be able to use whichever init system they want ? That is a fair statement and I completely empathize with it - but the question is really, who is really paying the price for this choice ?

The answer is not : _you - the user_. It is:_ they - package maintainers and developers_. For example, the guy who maintains Plex on Debian will now have to maintain compatibility on multiple init systems or else... his software will not be available on Debian's default package repository.


# Shell scripts are unixy - systemd .service files are not


systemd defines [.service](http://www.freedesktop.org/software/systemd/man/systemd.service.html) files to be used to define services (start, stop, dependencies, etc.). A service file is a declarative way to define a service. Previously, this used to be achieved by shell scripts - most of which were copied from someone who made it previously. For example, [this](https://github.com/gitlabhq/gitlab-recipes/blob/master/init/sysvinit/debian/gitlab-puma) is the sysvinit startup file for gitlab. And [this](https://github.com/gitlabhq/gitlab-recipes/blob/master/init/systemd/gitlab-unicorn.service) + [this](https://github.com/gitlabhq/gitlab-recipes/blob/master/init/systemd/gitlab.target) is the same startup file implemented as a systemd service.

Are shell scripts unixy ? Frankly, after [ShellShock](http://en.wikipedia.org/wiki/Shellshock_%28software_bug%29), I really dont care for millions of shell scripts (as part of init systems) written and maintained by hundreds of people.  I would much rather prefer a config file parsed by a single program, which can be audited far, far better.

There are people who are far more qualified as sysadmins than I will ever be, who have the following [opinion](http://debianfork.org/):


<blockquote>We like controlling the startup of the system with shell scripts that are readable, because readability grants a certain level of power and consciousness for those among us who are literate</blockquote>


I respect the emotion, but cannot empathize with the result. Your freedom to possess power and consciousness ends where my productivity, security and usability begins.


# systemd caused the Linux community to fragment


Atleast Upstart and SysvInit existed before systemd. There were also many others - like _initng _(for Berry Linux, etc.)

Oh, and lets not forget the big one - Android and it's init system "_binder_".


# The Binary log file problem


Simply put - systemd is trying to pull a [Splunk](http://www.splunk.com/) on your local machine. It is trying to build an indexed binary format for your log files on your machine, so you can do ... well [this](http://www.splunk.com/view/product-tour/SP-CAAAAGV). I think Lennart envisions an ecosystem of products that can easily aggregate and mine log files, much much more simply than what Splunk or Loggly's collectors do today.

Now, this is the second of the most contentious design decisions that systemd has taken and arguably has led to a huge amount of polarisation. There have been the inevitable comparisons with Windows event viewer and how binary logs have broken every known legacy tool ever.

This is true - I really, really dont know how good or bad this will be. I honestly cant see that far into the future - but I can respect the thought.

Secondly, getting a text log (via `ForwardToSyslog` journal-to-syslog forwarding) is bloody simple.


# The "boot without /usr " FUD


A popular conception is that systemd killed the possibility to have a separate /usr volume. systemd itself is actually completely fine with /usr on a separate file system that is not pre-mounted at boot time - however, many other components of Linux break because of this. [systemd is just the messenger.](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken/)

In fact, systemd developers are trying really hard to build [stateless](http://0pointer.net/blog/projects/stateless.html) and [minimally bootable](https://plus.google.com/u/3/+KaySievers/posts/UJ1Hj7DE4ZS) systems.


# Socket Activation FUD


Here's a comment by Russ Alberry of the Debian CTTE

https://lists.debian.org/debian-ctte/2013/12/msg00234.html


<blockquote>Socket activation, by which I don't mean lazy start of daemons, although it enables that, but init management of socket setup so that daemons can start in parallel.

This has been discussed elsewhere on the thread, but I want to note here that systemd's approach is bold and innovative. We've had multiple discussions in Debian lists in the past where people have felt somewhat depressed or discouraged about Debian's lack of innovation or unwillingness to tackle sweeping improvements. After having studied and
implemented socket activation, I think this is one of those opportunities, and we should not pass it by.

There are a variety of advantages to socket activation that have been discussed elsewhere, and I'm not going to repeat them all here. But one
I want to call out is the advantage for an enterprise systems administration environment. Right now, in order to configure bind addresses or IPv6 behavior for my services, I have to dig into the individual configuration syntax or command-line flags of each separate daemon, and often there's no easy way to set these parameters without making intrusive changes to daemon startup. Socket activation lets me manage all of this through a simple configuration override that I drop into /etc via (for example) Puppet, and the syntax is the same for every
service that uses it. It would obviously take quite some time to get there, but that's a really nice vision of the future, and one that would make a real difference for Debian use cases I care about.</blockquote>


The interesting part is that the Ubuntu competitor to Systemd -  Upstart -  also supports socket activation. Everyone is in agreement that socket activation is a particularly good idea... Just that systemd implements it [particularly well](https://lists.debian.org/debian-ctte/2013/12/msg00177.html).


# Everyone hates systemd


For an innocent bystander, systemd looks to be truly evil. Everyone seems to be hating it and only Lennart seems to be the evil mastermind promoting it.

Nothing could be further from the truth. Even before systemd became the default, Spotify [came out](https://lists.debian.org/debian-ctte/2014/01/msg00287.html) in support for it


<blockquote>

> 
> Spotify, an online streaming music service, is a significant user of Debian GNU/Linux. We have some 5000 physical servers and well over a thousand virtual servers using both public and private clouds running Debian GNU/Linux serving millions of songs to our users every day.
> 
> 

> 
> 

> 
> We would like to take this opportunity to endorse systemd as our preferred init system and we would like to see it as default on Debian GNU/Linux moving forward.
> 
> 

> 
> </blockquote>




# systemd is meaningless on the server


One of the most exciting engineering efforts in modern times - CoreOS and fleet are based on systemd. Both these Docker-based technologies are powering Google-like infrastructure for smaller startups.

In addition, as I pointed out above - startups like Spotify decided to bet on systemd, even when it was not standardized.

Also, as Russ Alberry quoted above, "_... one_
_ I want to call out is the advantage for an enterprise systems administration environment._" The sophisticated socket activation and [resource management abilities](http://0pointer.de/blog/projects/resources.html) of systemd are a godsend for building and managing large services on the cloud.


# Desktop Linux is dead - why fight for it ?


This has been the most ... frustrating thing that I hear from people. I have heard a million variants of "I dont care about desktop linux - just dont touch the server because of this".

This is the sad truth - in the USA and Europe, OSX has won. Every developer in every startup may deploy on Linux, but codes on the Mac.

But desktop linux is being transformative in Asia. In fact, India is becoming one of the fastest growing markets for Linux. Desktop linux is critical for everything here.

A good argument is _**mobile **_linux is becoming more relevant here - by which you essentially mean Android. But again, that is an argument made by people who work primarily on Macbooks and look at Linux/Android as auxiliary.

This is not the case in India.


# Gnome and KDE hard dependency theories - conspiracy ?


another big conspiracy theory is that Gnome and KDE are building hard dependencies on systemd. What need does a GUI desktop environment have of an init system ? Is this not definitive proof that systemd is trying to take over everything.

Well, actually Gnome and KDE dont depend on systemd, but rather logind - which is incidentally powering a lot of long-waited changes in desktop security and interaction. For example, it is [powering](http://fedoraproject.org/wiki/Changes/XorgWithoutRootRights) XWindows-without-root, something that is pretty cool for desktop security. Some of the other cool things it enables on the desktop are:



	
  * [http://dvdhrm.wordpress.com/2013/08/24/session-management-on...](http://dvdhrm.wordpress.com/2013/08/24/session-management-on-linux/)

	
  * [http://dvdhrm.wordpress.com/2013/08/24/how-vt-switching-work...](http://dvdhrm.wordpress.com/2013/08/24/how-vt-switching-works/)

	
  * [http://dvdhrm.wordpress.com/2013/08/25/sane-session-switchin...](http://dvdhrm.wordpress.com/2013/08/25/sane-session-switching/)


Oh, but logind seems to be pretty useless on the server. Isnt this a problem of prioritizing desktop features vs a server ? Well, logind also powers featuresets like [inhibitor locks](http://www.freedesktop.org/wiki/Software/systemd/inhibit/) (_A package manager wants to ensure that the system is not turned off while a package upgrade is in progress_).


# the cgroup arbiter issue


One of the other reasons that Gnome and KDE are building hard dependencies to logind is because of the cgroup arbiter issue. The Linux _kernel group _(and not systemd) is [mandating](http://www.linuxfoundation.org/news-media/blogs/browse/2013/08/all-about-linux-kernel-cgroup%E2%80%99s-redesign) that cgroups be written by a single writer in userspace.

systemd [implements](http://www.freedesktop.org/wiki/Software/systemd/ControlGroupInterface/) this single writer API and therefore seems to become "all powerful". Here's the kicker - every init system will need to do this eventually. systemd is just being the first one to do it.


# hard dependency on systemd libraries - libsystemd


[libsystemd-daemon](https://github.com/linuxmint/systemd/blob/master/src/libsystemd-daemon/sd-daemon.c) is a packaging of sd_notify - a fairly well documented _protocol _ to communicate with systemd. This is not so much a dependency as much as a convenience. For illustration, here's the same thing reimplemented in [python](https://github.com/kirelagin/pysystemd-daemon/blob/master/sddaemon/__init__.py) and [erlang](https://github.com/lemenkov/erlang-sd_notify).


# systemd has trashed cron


[systemd timers](https://wiki.archlinux.org/index.php/Systemd/Timers) are widely considered to be the answer to cron - that is true...but in no way does it trash cron.

systemd timers have the ability to specify dependencies, are automatically logged and run jobs with resource limits (using cgroups). That in itself makes it far superior to cron.


# udev is unusable without systemd (cue Lennart hate)


udev is dependent on kdbus - the high performance IPC mechanism, implemented in the kernel rather than userspace. kdbus is dependent on systemd for initialization.

udev will soon drop the netlink-based transport mechanism and therefore a hard dependency on systemd will arise. Again, this is something that you can replace if you can build the initialization code.

Secondly, udev is being maintained by Kay Sievers - not Lennart. This decision was a collaborative result of two core maintainers, rather than a global conspiracy. Here's what Kay has to [say](https://lwn.net/Articles/490413/) about udev:


<blockquote>

>     
>     Today, ‘Init’ needs to be fully hotplug-capable; udev device management and knowledge about device lifecycles is an integral part of systemd and not an isolated logic. Due to this, and to minimize our
>     administrative workload, as well as to minimize duplication of code, and to resolve cyclic build dependencies in the core OS, we have decided to merge the two projects.
> 
> 
</blockquote>




#  All of the above have been possible on *nix for decades


Which for me summarizes what systemd is versus what people _think_ it is. More than ideas, systemd is innovation in implementation. There have been a hundred million "recipes" floating around on how to build stateless systems, or what is the "[best](http://dev.mysql.com/doc/refman/5.0/en/mysql-server.html)" startup script for a particular service.

systemd standardizes on all of that - it builds consistency where there was none. It makes it possible for someone like me to start building Google-ish clouds - by reducing the complexity by orders of magnitude. How could you not want that ?


# Joey Hess did not leave because of systemd


Here's his [blog post](http://joeyh.name/blog/entry/a_programmable_alarm_clock_using_systemd/) building a cool little hack on his laptop using systemd.


<blockquote>I don't think this would be anywhere near as easy to do without systemd, logind, etc. Especially the handling of waking the system at the right time, and the behavior around lid sleep inhibiting.</blockquote>




# Tweet  #systemdisnice



