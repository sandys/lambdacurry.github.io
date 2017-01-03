---
author: sandeep
comments: true
date: 2011-10-14 19:30:47+00:00
layout: default
link: http://www.lambdacurry.com/2011/10/monitoring-hardware-raid-at-a-dedicated-hosting-provider-hivelocity/
slug: monitoring-hardware-raid-at-a-dedicated-hosting-provider-hivelocity
title: Monitoring hardware RAID at a dedicated hosting provider (Hivelocity??) ...
  and avoiding nasty surprises
wordpress_id: 561
---

Hivelocity has been quite a good host for us for a coupla years now - but today a friend of mine, who owned a 500$ Hivelocity RAID 1+0 server permanently lost his data completely, I had to really try and figure out what happened.

I suddenly figured that I had no scripts to really monitor my hardware raid. After a lot of googling, I came upon a couple of tidbits, that could help others.

**Figuring out what controller you have**

I took a lot of help from this script [here](http://www.watters.ws/scripts/checkraid.sh) to figure out which RAID card I have. In general it could be



	
  1. 3Ware SATA RAID -  lsmod|grep 3w-xxxx __or lsmod|grep 3w_xxxx

	
  2. LSI Megaraid - lsmod|grep -w megaraid

	
  3. LSI Megaraid SAS - lsmod | grep megaraid_sas


Since, I have a LSI Megaraid card on my server, I will be writing about Megaraid ... and its tools - Megacli

**Installing MegaCli**

(This step took me a while to locate) Add the following lines to your _/etc/apt/sources.list _


<blockquote>deb http://hwraid.le-vert.net/ubuntu lucid main</blockquote>


run _sudo apt-get update && sudo apt-get install megacli_

MegaCli is now installed. The command I use to get the fastest piece of info is


<blockquote>sudo megacli -AdpAllInfo -aAll -NoLog | grep -A 6 "Virtual Drives"</blockquote>


You get the following pieces of information


<blockquote>

>     
>     Virtual Drives    : 1
>       Degraded        : 0
>       Offline         : 0
>     Physical Devices  : 3
>       Disks           : 2
>       Critical Disks  : 0
>       Failed Disks    : 0
> 
> 
</blockquote>


Thats good enough for a quick monitor - add that into your crontab and you're good to go. A good readymade script is [here](http://www.watters.ws/scripts/sascheck.sh).

**RAID battery issues**

As I read in this blog [post](http://agiletesting.blogspot.com/2011/09/slow-database-check-raid-battery.html), there are issues with LSI Megaraid controllers (usually in Dell servers), where the RAID battery state is using its heuristics to learn about RAID behavior .. especially after a reboot.

Generate an _event-log-since-last-reboot _using _megacli -AdpEventLog -GetSinceReboot -f events.log -aALL_

Grep for the keyword _changing. _The reason why this flags is an issue because RAID controllers try to autolearn the battery charge. Double check your autolearn mode by _megacli -AdpBbuCmd -GetBbuStatus -a0_


<blockquote># echo "autoLearnMode=1" > tmp.txt
# megacli -AdpBbuCmd -SetBbuProperties -f tmp.txt -a0</blockquote>


Please run the autolearn cycle manually by _megacli -AdpBbuCmd -BbuLearn -a0_


