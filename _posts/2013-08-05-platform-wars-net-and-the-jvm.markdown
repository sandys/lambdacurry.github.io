---
author: admin
comments: true
date: 2013-08-05 07:09:38+00:00
layout: post
link: http://www.lambdacurry.com/2013/08/platform-wars-net-and-the-jvm/
slug: platform-wars-net-and-the-jvm
title: 'Platform wars: .NET and the JVM'
wordpress_id: 774
categories:
- technology
tags:
- .net
- frameworks
- jvm
---

A chance conversation with a friend got me to think about two of the most dominant platforms out there - .NET and JVM


**note**: I dont say Java or C#, because these platforms have given birth to more languages than the two most popular ones. Clojure, Scala, F#,etc. are some of them.


In particular, I want to think about whether there is a crippling effect to the overall strategic engineering roadmap if you choose the obvious devil - the .NET stack.

**JSP vs Silverlight**

JSP vs Silverlight is a case-study in the business of risk of adopting technologies that have a single point of failure in parent companies.

JSPs were invented by Sun in [1995-2000](https://weblogs.java.net/blog/driscoll/archive/2005/12/servlet_history.html). It's not the best technology today by any stretch of imagination, but it has been kept alive by users who choose to use/learn/teach them. Development of the JSP codebase has progressed over the past two decades as the Java platform evolved.

On the other hand [Silverlight](http://en.wikipedia.org/wiki/Microsoft_Silverlight#cite_note-10) was originally released by Microsoft in 2007. It got its big win with the Beijing Olympics in 2008 (which used Silverlight for streaming).

Microsoft abandoned it in [2012](http://visualstudiomagazine.com/articles/2012/07/13/silverlight-transitions-continue-for-developers-and-microsoft.aspx) and took with it millions of dollars of technology investments by companies all over the world. It is a fundamental case study in the business continuity rewards of betting on true open source.

**License costs**

Here is a nice [article](http://www.brentozar.com/archive/2013/07/sql-server-2014-standard-edition-sucks-and-its-all-your-fault/) by Microsoft SQL Server guru Brent Ozar on the various licensing cost issues that begin to hit you as soon as you graduate out of the Microsoft Accelerator program or start to handle any decent amount of computation/traffic.

Now, dont get me wrong - I do not mean to disparage SQL Server which is a seriously marvelous piece of technology (unrivaled by Mysql or Postgres till now). However the 98% of use cases that dont need the secret sauce of SQL Server, will be seriously crippled by the exponential license growth.

_Why is this important ?_ Frequently, companies have a sunk investment into expensive technologies like SQL Server, and therefore the question begs to be asked - so what ? The problem is that as you refactor/rearchitect your system to a split service-based architecture, you will need independent self-contained teams/systems. Now, the volume licenses of a single enterprise SQL Server license is no longer relevant. I wouldnt want my teams productivity being crippled by sales negotiations into 3 new licenses.

And I dont even know the impact of these licenses on test and pre-production setups.

Rob Conery was a member of the ASP.NET team at Microsoft. When he started his company - Tekpub - he moved away to using Ruby on Rails and MongoDB. This is what [he had to say](http://www.infoq.com/articles/architecting-tekpub).


_**RB:** So what does the TekPub platform look like today? _




**RC: **We moved to Rails 2.3.5 using MongoMapper against [MongoDB](http://www.mongodb.org/). We have a reporting setup that uses [MySQL](http://www.mysql.com/?bydis_dis_index=1) to track stuff we need to report on which uses [DataMapper](http://datamapper.org/). We also plugged in [New Relic RPM](http://www.newrelic.com/) to keep track of our site and it's health - all of this is less than 1% of what it would have cost us, on average, with BizSpark.




**JA:** This solved all of our issues around licensing, we pay about $80/month for a large Ubuntu instance on [Amazon EC2](http://aws.amazon.com/ec2/), after the reserved instance fee. It’s a technology that both Rob and I really enjoy working with, we have great testing with [Cucumber](http://cukes.info/), and deployments with [Capistrano](http://www.capify.org/index.php/Capistrano) are simple and easy.




**JA:** All the problems we had (licensing, testing, deployments) could have been overcome. We could have used workarounds, written our own deployment framework, etc. What is comes down to is that we both really enjoy working with Rails and we enjoy the Rails community and the tools and libraries available. One of the best parts about running the show is that we get to do what makes us happy.




_**RB:** How hard is it to do testing on a Microsoft stack and why?_




**RC:** The language and the tools. If Microsoft thought more about it, it would be a bit easier to test the stuff. You can't do RSpec with any language other than Ruby really - it just makes it easy. Microsoft could capitalize on that with the DLR... but they don't. It's not in their ".NET Story" and that's OK - it's their business decision. It was ours to move away from t


NOTE - I'll be talking about Capistrano in the point about _Impact on Service Oriented Architecture/Distributed Systems_

**Legal impact of licenses and patent coverage**

Mono/Xamarin is basically an open source fork of the .NET runtime - Microsoft has actually seen it fit to encourage this development. However, there are certain aspects of the runtime that are not available on Mono (for legal or technical reasons).

Until the [Oracle vs Google lawsuit](http://en.wikipedia.org/wiki/Oracle_v._Google) is done with completely, the legal implications of both .Net/Mono and JVM platforms are a little doubtful. To a very large extent, this will not impact server-side applications, because the license talks chiefly about "redistributable" code - i.e. if you are shipping devices with these pieces of software on them (like Android was doing).

In general, server side applications are exempt from patents (from Oracle or Microsoft) being used to disable core functionality.

**Superiority of technology**

I would say it is an even match here. The .NET runtime and C# is quite well designed (by one of the greatest language designers on the planet - Anders Hejlsberg). They undoubtedly learned from some of the mistakes that Java did. The biggest con is obviously the fact that is tied down to the Windows platform (and its cost implications). In fact, C# (along with the Xamarin stack) is now one of the most effective ways to build apps for mobile devices across all platforms (iOS, Android and Windows Mobile)

On the other hand, the JVM is one of the most performant runtimes ever - very few things can come close to it in terms of performance. The Java language however is not the best designed language (when you compare it to C#). However, the rapid rate of language development on the JVM platform has given rise to some of the most advanced programming languages ever - Clojure, Scala, JRuby, etc.

Now, while F# is another language built on top of the .NET runtime, but it is not as production tested as some of the newer JVM languages - for e.g. Twitter (Scala), Twitter-Backtype (clojure), Factual (clojure).. and my very own Tradus (Jruby - atleast circa 2012).

**NOTE**: I later realized that, the [core of LINQ](http://codebetter.com/matthewpodwysocki/2008/10/13/functional-c-linq-as-a-monad/) essentially the same as the core of F# : two operators Return(x) and Bind(m,f). The name of Return is datatype dependent in LINQ, but its purpose is to create a container with a single thing inside. 

This does not sound like a problem, but it is - because some of the most exciting technology platform of recent times is being built on these newer languages and .NET is simply not able to keep up, regardless of how superior the platform is - e.g. [Storm](https://github.com/nathanmarz/storm) (in clojure).

One of the big *rumors* against .NET - lack of systems for building web services is simply not true. For example, [ServiceStack ](http://www.servicestack.net/)is an amazing piece of architecture with one of the fastest JSON parsing engines around (used by Stackoverflow, among other companies). There are many more than I would like to list, but many startups default to using ASP.NET MVC to build web services ... which doesnt make sense.

**Modern Hardware**

Both the .NET framework and the JVM are equipped to deal with multicore on modern day hardware. However, there are certain technology fabrics (like [Azul](http://www.azulsystems.com/products/zing/whatisit)) which extend the power of JVM on grids and bring together really advanced tech pieces like Software Transactional Memory.

(more on this in the next section)

**Community**

"Productivity", as is meant in modern day programming practice, is a function of leveraging existing building blocks. These are pieces of fundamental technology built and maintained by the community - which could be both the parent company, or by an open source community worldwide.

The "officially" sanctioned community repository for the .NET platform is [Codeplex](http://www.codeplex.com/).

The JVM is absolutely unparalleled in this regard.

To dig deeper into this, I took a look at what is probably the current poster boy for .NET development - StackOverflow. Jeff Atwood (a highly experienced .NET programmer for a long time) made the decision to go with ASP.NET and has [blogged ](http://www.codinghorror.com/blog)about his justifications. One of the big things that .NET made is possible for them in the early days was performance, since it ran much faster than Python or Java.

However, as they needed to go deeper into horizontal scalability and performance, they realized that some of the most important pieces of web scalability - load balancers, messaging queues, etc are all based on top of Linux (for example, they use HAProxy for load balancing and Redis for queuing). As a result they [built](http://blog.stackoverflow.com/2012/02/stack-exchange-open-source-projects/) a lot of tools in-house to be able to interoperate with these sytems.

This is what Jeff [has to say](http://www.codinghorror.com/blog/2013/03/why-ruby.html) about sharing software in the .NET world.


You can certainly build open source software in .NET. And many do. But it never feels natural. It never feels right. Nobody accepts your patch to a core .NET class library no matter how hard you try. It always feels like you're swimming upstream




I no longer live in the Microsoft universe any more. Right, wrong, good, evil, that's just how it turned out for the project we wanted to build.




However, I'd also be lying if I didn't mention that I truly believe the sort of project we are building in Discourse does represent most future software. If you squint your eyes a little, I think you can see a future not too far in the distance where .NET is a specialized niche outside the mainstream


**Talent Trends**

[![jobgraph2](/wp-content/uploads/2013/08/jobgraph2.png)](/wp-content/uploads/2013/08/jobgraph2.png)The graph from Indeed.com job search trends gives an indication of talent availability along PHP, C# and Java.. along with .NET and JVM languages like Scala and F#.

It is therefore a question of how you would acquire, retain and motivate your talent over the lifecycle of your engineering roadmap.

**Homogeneity vs Interoperability
**

The main issue is not one of building the entire stack in Java (as opposed to Ruby or any of the hundreds of languages out there). The main issue is interoperability - because of the platform tie down of .NET, there are several hoops that need to be jumped to get an effective stack.

For example, one will invariably use HAProxy, Varnish, Memcached or Redis - all of them run on Linux and will add to the complexity of managing your overall stack (which started off primarily around Windows)

**Impact on Service Oriented Architecture/Distributed Systems
**



	
  * _Deployment & Management Systems - _One of the biggest sources of complexity in a distributed systems framework is service orchestration. This is a problem both at production as well as during development (how do you setup a stack combining tens of services on a developer's laptop). The Linux world has a plethora of systems which solve this problem with space age sophistication - Puppet, Chef, Ansible, etc. are all some of those. There are not many such tools in the Microsoft world.

	
  * _Cloud Compatibility - _ Except for Microsoft Azure (which is looking to be suffering from the same Silverlight risk mentioned above), all the other cloud platforms support stacks which are difficult to interoperate with .NET systems. For example, it is tricky to use Amazon RDS (even though it is currently built on SQL Server 2008 R2) from an ASP.NET deploy on EC2.

	
  * _Self contained systems _- License costs begin to impact as you begin to build a distributed system with self contained databases.




People have their opinions - especially when it comes to editors (Vim rules!) and platforms. There are some who are overly [dogmatic](http://blog.expensify.com/2011/03/25/ceo-friday-why-we-dont-hire-net-programmers/) about it . Yet, objectively thinking, I think I make a strong case to rearchitect away from .NET frameworks in a way that is easily justifiable.
