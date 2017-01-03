---
author: sandeep
comments: true
date: 2011-03-24 09:43:17+00:00
layout: default
link: http://www.lambdacurry.com/2011/03/maven-jaxb-plugin-problems-in-your-maven-pom-xml/
slug: maven-jaxb-plugin-problems-in-your-maven-pom-xml
title: maven-jaxb-plugin problems in your maven pom.xml
wordpress_id: 525
---

[put up here to be crawled and help the next hapless soul]

taken from http://blog.dawouds.com/2009/11/sun-moved-maven-repository-breaking.html

Just put in


<blockquote>

> 
> `<``pluginRepositories``>`
> 
> 

> 
> ` ``<``pluginRepository``>`
> 
> 

> 
> ` ``<``id``>java.net-plugin-1</``id``>`
> 
> 

> 
> ` ``<``name``>java.net Maven Repository</``name``>`
> 
> 

> 
> ` ``<``url``>[http://download.java.net/maven/1](http://download.java.net/maven/1)</``url``>`
> 
> 

> 
> ` ``<``layout``>legacy</``layout``> `
> 
> 

> 
> ` ``</``pluginRepository``> `
> 
> 

> 
> ` ``<``pluginRepository``>`
> 
> 

> 
> ` ``<``id``>java.net-plugin-2</``id``>`
> 
> 

> 
> ` ``<``name``>java.net Maven Repository</``name``>`
> 
> 

> 
> ` ``<``url``>[http://download.java.net/maven/2](http://download.java.net/maven/2)</``url``>`
> 
> 

> 
> ` ``</``pluginRepository``>`
> 
> 

> 
> ` ``</``pluginRepositories``>`
> 
> </blockquote>


in your pom.xml
