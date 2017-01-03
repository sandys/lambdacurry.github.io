---
author: admin
comments: true
date: 2013-07-24 10:57:19+00:00
layout: default
link: http://www.lambdacurry.com/2013/07/how-to-think-about-web-services-apis/
slug: how-to-think-about-web-services-apis
title: How to think about web services APIs - REST and SOAP
wordpress_id: 749
---

Over the past couple of years, I have architected or consumed web services APIs inside various web applications. And during all that time, I have never really thought about a formal approach towards API design.

A lot of what I did was subconsiously picked up from the way Rails controllers were architected, or the way that Amazon APIs were built up. However, it stands to reason to analyze the fundamental philosophy behind that design.

I typically hear arguments like this - _"REST is used for lightweight architectures, while SOAP should be used for complex architectures involving Transactions, Security, etc"_

Duh.

Amazon - perhaps the backbone of the entire web services world implements a highly secure, authenticated+authorized web services framework on top of a REST-like API. You particular vendor might claim the above, but it isnt true in general.


## Is it truly REST ?


HTTP is fundamentally two things - _discoverable _and _stateless_. You want something - you ask for it and http will either give it to you, or tell you what's wrong. REST is very much like that.

SOAP - a philosophy predominant in the .NET world - is a philosophical first cousin to HTTP (and by extension REST). It basically takes both the essential elements of HTTP/REST - viz. the URL and the Header - and packages them as a XML document to be sent over a POST request to a single endpoint. So it kind of behaves like a single page web app - you dont know where you are with a single look.

Why is this even important ? There is a great [presentation](http://mollyrocket.com/883.pdf) from MollyRocket, that leads you to the answer - _reuse of components_. Effectively, reuse is a function of time - a single endpoint with a complex set of instructions sent to each effectively nullifies the way you can architect for reuse.

Let's understand what that means from an example of Object Oriented programming:


## Transferring state vs transferring objects


In classic OO design philosophy - objects have state and function.

When you work with REST apis, you are just playing around with state - the functions are pre-defined: GET, POST, PUT, DELETE. Let's say you have an object in your database - User. You now need someway to combine two users, so what do you do ? You define a resource _/combineusers _and possibly call POST with id=1 and id=2. Thinking in OO parlance, what you have just done is set the state of the _CombineUsers_ class to id=1&id=2. This class, in turn, could have simply inherited/extended from the _Users_ class. In fact, at this point, you can completely do away with traditional inheritance paradigms and instead bring in stuff like monkey patching to achieve the same result (IMHO - one of the reason, functional languages like Ruby work beautifully here).

How would you have done the same thing with SOAP ? Well you would have composed an XML like the following :

    
    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
     <soap:Body>
      <gs:CombineUsers xmlns:gs="urn:C<em>ombineUsers</em>">
       <id1>1</id1>
       <id2>2</id2>
      </gs:CombineUsers>
     </soap:Body>
    </soap:Envelope>


But that is NOT idiomatic SOAP. What you really need to do (as per the "true way") is request the entire Object on your client side and call seemingly native functions on both (which transparently call remote calls). Effectively, you would have done this:

    
    <code>$client = new SoapClient(null, array('location' => "http://localhost/soap.php",'uri'      => "http://test-uri/"));
    $client->SomeFunction($a, $b, $c);
    <code>//or
    $client->__soapCall("SomeFunction", array($a, $b, $c));</code>
    </code>


On the surface, it doesnt look too different. Now, think about how you would implement that on your remote side - every call to request an object has to send along with it (at a minimum), all applicable method calls. This becomes an even bigger clusterfuck, when you have to deduce "applicable method calls" on the basis of authorization and ACLs.

Suddenly, not only does your class become invariant, but also every one of your methods - because the whole world has access to them. How on earth are you supposed to refactor ?

I havent worked very deeply with SOAP server architectures, but I dont even think you can inherit classes here - you are always afraid of what methods you might inadvertently expose. So you have to start engineering in terms of _interfaces_ , etc.


### A list is an object.


With REST, you simply throw away the concept of working with objects and instead think in terms of _**state.**_** **The big advantage that comes here is that on the client side, you can model this state as a list.. or a map... or as a string. As long as you model the state correctly and transfer it to the server, nobody cares what the underlying object model is. Which is why REST based clients are easy to implement in the most quirkiest of programming languages.


## The mystical compiler and interface definitions


One of the most popular arguments in favor of SOAP is type-checking and automatic datastructure creations by SOAP. Unlike most of the REST fanatics, I do agree on this part. In large enterprise-y infrastructures, this can be a godsend.

So is REST dead in the water in large teams ?

Not really. If you think about it, effectively what you want is what I like to call _serialization compatibility_.

Enter [Thrift](http://thrift.apache.org/).

Thrift is a binary serialization protocol that is agnostic of the kind of web technologies you are using and the kind of underlying protocol that you are leveraging. It natively understands a few different basic [types ](http://thrift.apache.org/docs/types/)and generates interface wrappers for them (in a variety of languages - Ruby, Python, .NET, etc.).

Using Thrift over REST effectively nullifies the advantage that SOAP had, but gives you the advantage of type-checking. What's more, REST allows you to specify the wire-format - so you can start off with JSON and move to Thrift once you are comfortable with your client.

The best part - Thrift is 600% [faster](http://code.google.com/p/thrift-protobuf-compare/wiki/BenchmarkingV2) than native XML/JSON.


## Art of documentation


If you are part of an enterprise that is implementing a web-services rearchitecture, then the best way to answer "documentation???" questions is by two things - **_dogfooding_** and _**testcases**._

_Testcases: _One of the problems with SOAP is discoverability. This is the endemic problem of .NET based architectures which are caught in a cycle of SDK based toolkits - loosely based on SOAP. If you want to use them, you need to write code in a supported SDK and instantiate the objects (remember what I wrote above ? you are getting the entire "object").

Compare that to REST, where you can "GET" the state from your commandline

    
    curl -XGET http://ifconfig.me/ip


What this effectively buys you is that you can get away very effectively by just documenting the list of end-points ("_resources_"). Your testcases should be able to give a hint of what is the expected output.

If you are using a interface language like Thrift, then the IDLs for the APIs could be useful, but they are effectively transparent to the client (since they only impact the wire).

_Dogfooding_: It effectively means eating your own food before feeding the dog. One of the best examples of enterprise rearchitecture and dogfooding was set by[ Jeff Bezos](https://raw.github.com/gist/933cc4f7df97d553ed89/24386c6a79bb4b31fb818b70b34c5eab7f12e1ff/gistfile1.txt), who effectively threw a fit:

    
    <span style="font-size: small;">So one day Jeff Bezos issued a mandate. He's doing that all the time, of course, and people scramble like ants being pounded with a rubber mallet whenever it happens. But on one occasion -- back around 2002 I think, plus or minus a year -- he issued a mandate that was so out there, so huge and eye-bulgingly ponderous, that it made all of his other mandates look like unsolicited peer bonuses.
    
    His Big Mandate went something along these lines:
    
    1) All teams will henceforth expose their data and functionality through service interfaces.
    
    2) Teams must communicate with each other through these interfaces.
    
    3) There will be no other form of interprocess communication allowed: no direct linking, no direct reads of another team's data store, no shared-memory model, no back-doors whatsoever. The only communication allowed is via service interface calls over the network.
    
    4) It doesn't matter what technology they use. HTTP, Corba, Pubsub, custom protocols -- doesn't matter. Bezos doesn't care.
    
    5) All service interfaces, without exception, must be designed from the ground up to be externalizable. That is to say, the team must plan and design to be able to expose the interface to developers in the outside world. No exceptions.
    
    6) Anyone who doesn't do this will be fired.
    
    7) Thank you; have a nice day!
    <strong><span style="font-size: large;">- from a now deleted blog post by Steve Yegge
    
    </span></strong></span>


if you eat your own dogfood, I dont see why there will ever be a documentation problem (there still will be :twisted: , but much less than otherwise)


## Is this perfect ?


No, it is not. But I would say that a perfect solution is marketing sell from an enterprise vendor. What you should be looking for is understanding the problems and defining your organization to work with it, instead of shooting for the stars and having it fall on top of your head.
