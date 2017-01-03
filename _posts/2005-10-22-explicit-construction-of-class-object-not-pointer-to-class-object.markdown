---
author: sandeep
comments: true
date: 2005-10-22 17:48:00+00:00
layout: default
link: http://www.lambdacurry.com/2005/10/explicit-construction-of-class-object-not-pointer-to-class-object/
slug: explicit-construction-of-class-object-not-pointer-to-class-object
title: Explicit construction of class object (not pointer to class object)
wordpress_id: 77
categories:
- c++
- software
---

Consider the following piece of code:





    
    <font>#include</font> <stdio.h> 
    
    <font>#include</font> <stdlib.h>
    <font>using</font> <font>namespace</font> std;
    
    <font>class</font> SSS{
       <font> </font><font>public</font>:
           SSS(){
            printf(<font>"Calling constructorn"</font>);
           }
    };
    
    <font>typedef</font> <font>struct</font> test{
    SSS s1;
    }test;
    
    <font>int</font> main(){
        test *t1;
        t1<font>=</font>(test*)malloc( <font>sizeof</font>(test)*<font>1</font>);
        <font>return</font> <font>0</font>;
    }


Does the constructor of the class get called?
Nope.

Then how do you do it. The problem is, how do you explicitly call the constructor of a class object that is defined but not constructed. Usually, class objects are constructed as soon as they are declared. For e.g.


<blockquote>SSS s1;</blockquote>


The above will immediately call the constructor of SSS. However, this is a case where  objects are declared, but not constructed. And there is no easy way to construct it now.

First of all, this is bad design. If there is ever a necessity to explicitly declare a class object but construct it only later, then a pointer to a class should be used.
However, this is comes from another problem that I encountered.
Legacy code.
Ah yes. the bane of any code writers existence. While code can almost be thought of a s poetry, this, ladies and gentlemen, is nothing short of blasphemy.

In any case, the solution is not very difficult - placement new operator.
Take a look at the modified code:





    
    <font>#include</font> <stdio.h> 
    
    <font>#include</font> <stdlib.h>
    <font>using</font> <font>namespace</font> std;
    
    <font>class</font> SSS{
       <font> </font><font>public</font>:
           SSS(){
            printf(<font>"Calling constructorn"</font>);
           }
           <font>void</font>* <font>operator</font> <font>new</font>(size_t size, SSS* s2){ <font>//<-- need to overload</font>
    
    printf(<font>"Calling operator newn"</font>);
            <font>return</font> (malloc(<font>sizeof</font>(SSS)*<font>1</font>));
           }
          <font> </font><font>private</font>:
            <font>int</font> n;
    };
    
    <font>typedef</font> <font>struct</font> test{
    SSS s1;
    }test;
    
    <font>int</font> main(){
        test *t1;
        t1<font>=</font>(test*)malloc( <font>sizeof</font>(test)*<font>1</font>);
        <font>new</font>(&t1<font>-</font>>s1)SSS;  <font>//<---- how cool is that</font>
    
    <font>return</font> <font>0</font>;
    }


The key is overloading the new operator and calling the placement new operator in a weird way:


<blockquote>new(&t1->s1)SSS</blockquote>


Again... bad design.


del.icio.us Tags: [software](http://del.icio.us/sss8ue/software)
