---
author: sandeep
comments: true
date: 2010-11-18 06:19:33+00:00
layout: default
link: http://www.lambdacurry.com/2010/11/third-party-libs-management-with-leiningen-in-clojure/
slug: third-party-libs-management-with-leiningen-in-clojure
title: third party libs management with leiningen in clojure
wordpress_id: 477
---

in a particular project, I had to use a 3'rd party jar given to me. I didnt want to go through the whole business of uploading the JAR to clojars and trying to manage it.

An alternative was to install it in my maven local directory using _**mvn install:install-file **_. But I wanted something simpler.

The problem is that if you copy a JAR file into your lib directory and check it into revision control, the moment someone clones the repository and runs _lein deps_, it will destroy-recreate the _lib _directory causing the 3'rd party jars to be lost.

The way I figured to make it work was to use the _:disable-implicit-clean true _variable, which will prevent delete-recreate of the lib directory.

A hack.. but it works.
