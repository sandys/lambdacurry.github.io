---
author: admin
comments: true
date: 2015-09-28 09:03:01+00:00
layout: post
link: http://www.lambdacurry.com/2015/09/the-power-of-digital-india-and-the-futility-of-our-government/
slug: the-power-of-digital-india-and-the-futility-of-our-government
title: The power of Digital India and the futility of our government
wordpress_id: 924
---

There's been a few reddit threads started about how the #DigitalIndia campaign is a stupid exercise and our funds and efforts should be better utilized on building basic infrastructure for farmers. It is a classic comment that gets repeated again and again. It is fairly similar to an argument in a hospital - should you do the surgery yourself or spend a lot of extra time+effort+money training a new intern on how to perform surgery. Do note that it will take many years for the intern to qualify to do a surgery.

In 2002, when I graduated from IIT Bombay, I was part of a small project called a[AquA](https://en.wikipedia.org/wiki/Aaqua) headed by Prof Krithi Ramamritham. I will have to confess that I did no work, and was more interested in getting drunk - but aAquA turned into something very powerful. It still lives on today at https://aaqua.persistent.co.in/aaqua/forum/index and is run by Persistent Systems.

aAquA stood for Almost All Questions Answered. Think of it as Quora + Wikipedia for farmers.  The interesting point was that this effort predates the mobile phone revolution in India or even the internet revolution. It predates Flipkart or any ecommerce in India. Even more flabbergasting is that aAquA was contemporary with television based content for farmers (e.g. Krishi Darshan), yet was being used by farmers who walked all the way to telephone booth to access the internet. What did help a lot was that it was multi-lingual from the start (e.g. [here](https://aaqua.persistent.co.in/aaqua/forum/viewthread?thread=24242)) which was very important to reach out to that particular demographic.

Imagine what you could do with a mobile aAquA !

DigitalIndia is a fair goal, but unfortunately the goal is badly planned and is doomed to failure. Let's take a simple example - just to get millions of farmers connected to the internet, presumably through their mobile devices, needs IPV6. In case people havent noticed, we have[ run out of IPV4 addresses](http://www.theinquirer.net/inquirer/news/2427696/as-the-us-runs-out-of-ipv4-addresses-bt-confirms-uk-rollout-of-ipv6). Yes, there are ways to get around it.. but it makes zero sense in a country of our population. We need IPV6 yesterday to enable mobile connectivity, yet we have no comprehensive strategic plan around IPV6.

The only other country with a crippling dependence on IPV6 is China, but it started a large scale push to IPV6 in 2008 (using the Olympics as an [excuse](http://ipv6.com/articles/general/IPv6-Olympics-2008.htm)).

Also remember that we are the ones who need a large number of fonts and language support for our users to use the internet. That effort has not been standardized yet - in fact the only place I can find comprehensive Indic fonts is at the [Google Noto](https://www.google.com/get/noto/) project. However, font rendering for the lesser known languages needs compex technologies like [SIL Graphite](http://scripts.sil.org/cms/scripts/page.php?site_id=projects&item_id=graphite_aboutOT) which is not an important criteria for the rest of the world. Even if we solve it, we have no content on the internet that serves these languages. Take for instance the **[Traditional Knowledge Digital Library](https://en.wikipedia.org/wiki/Traditional_Knowledge_Digital_Library) - **the content inside is locked up in unreadable images and english language PDF. It cannot even be translated effectively.

And while these are important aspects to be taken under consideration, our government is keen on focusing on censorship and banning porn sites.

Digital India is a fair goal. I have zero confidence that this government can actually execute it.


## Indian fonts and the Digital Divide


EDIT: so I got a question from Kiran on what's so difficult about supporting Indian languages. After all most computers have Indian languages, right ?

Wrong.

There is NO operating system in existence that supports Indian languages in all its complexity. This is called the "ligature" problem - what we know in hindi as "maatras". Historically, Microsoft has been the most compatible of all operating systems for Indian languages. Take for example this page on [Oriya language support](http://www.microsoft.com/typography/OpenTypeDev/oriya/intro.htm) on Microsoft's official site. The complexity of supporting Oriya is laid bare.

Look at the same language on [Noto](https://www.google.com/get/noto/#sans-orya).

Even more interestingly, Noto screws up on Urdu - it assumes the Arabic Nashq script for Urdu. However, Urdu is an Indian language - it uses a derivative of the Persian Nastaliq fonts (a brilliant write up by Ali Eteraz [here](https://medium.com/@eteraz/the-death-of-the-urdu-script-9ce935435d90)) .

This is why I filed a bug on [Google](https://github.com/googlei18n/noto-fonts/issues/39) ;)

So what happens in Android currently ? Android re-uses the same fonts as Linux - that is the [Lohit Indic](https://en.wikipedia.org/wiki/Lohit_fonts) fonts. However, Noto has undergone several improvements in rendering (as can be seen in this [bug](https://github.com/googlei18n/noto-fonts/issues/474)). Hindi/Devanagari specific efforts in this direction have been [SIL Annapurna](http://software.sil.org/annapurna/) and Microsoft's [Utsaah](https://www.microsoft.com/typography/fonts/font.aspx?FMID=1811) / [Nirmala](https://en.wikipedia.org/wiki/Nirmala_UI) .. but no such love exists for most of the other Indian languages (especially south Indian).

Now, SIL Graphite rendering technology is far superior to Harfbuzz/Pango (which is what is used by default on Linux/android) **for minority and Indic languages**. But for obvious reasons, it is not a priority for the core Android project. Additionally, how do you input text on mobile phones in Oriya ? You have to hunt through hundreds of keyboard apps to find one that works. this is NOT how you do DigitalIndia.

Apparently, our govt is spending a lot of money on a customized version of Linux called BOSS. And what is so special about this great OS ? [this](http://wiki.bosslinux.in/wiki/index.php/Security). As most people would know, this takes a system administrator all of 2 hours to configure.

You want to bridge the digital divide ? let's first understand the problem - language accessibility and infrastructure/IPV6 problems. Let's talk about Facebook later.
