---
author: sandeep
comments: true
date: 2005-06-12 01:27:00+00:00
layout: post
link: http://www.lambdacurry.com/2005/06/constructors-vs-function-declarationsand-koenig-lookups/
slug: constructors-vs-function-declarationsand-koenig-lookups
title: Constructors vs function declarations...and Koenig lookups
wordpress_id: 51
categories:
- c++
- compiler
- software
---

A very curious incident happened with compilation today.  

"but nothing happened...."




That was the curious incident.




Consider the piece of code below:






    
    
    
    <font>#include</font> <iostream>
    <font>using</font> <font>namespace</font> std;
    <font>class</font> A{
      <font> </font><font>public</font>:
             A() {_i<font>=</font><font>5</font>;}
              ~A(){cout<<<font>"Destroying A"</font><<endl;}
           <font>int</font> _i;
    };
    <font>class</font> B: <font>public</font>  A{
     <font>public</font>:
       B() {}
       ~B(){cout<<<font>"Destroying B"</font><<endl;}
    
    };
    
    main(){
      A a( B() );
      cout<<a._i;
    }
    







Now normally, I would think that everything is all right. My expected screen output is:




"Destroying A"  

"Destroying B"  

"Destroying A" (its inherited)




However, there is no screen output.  

To further investigate, let us try to access a member variable "_i" of A.  

The compiler squeals:  

>>constructor.cpp: In function 'int main()'  

>>constructor.cpp: error: request for member '_i' in 'a', which is of non-class type 'A()(B(*)())




"non-class"?? Very strange. What's even more strange is the way that the constructor parameters to A are interpreted - as pointer to functions.




Now, we know for a fact that STL uses functors, so let's try something like this with them.






    
    
    <font>#include</font> <iostream>
    <font>#include</font> <vector>
    <font>#include</font> <algorithm>
    <font>using</font> <font>namespace</font> std;
    <font>class</font> Functor1{
    <font></font><font>public</font>:
       <font>void</font>  <font>operator</font> ()(<font>int</font> i){ }
    };
    main(){
    vector<<font>int</font>> vv;
    
    for_each(vv.begin(), vv.end(), Functor1());
    
    }
    







STL has no problem.




Actually, in the first case, C++ interprets A a() as local declaration of a function 'a' with return type A. One of a long [threads ](http://groups-beta.google.com/group/comp.lang.c++.moderated/browse_thread/thread/dd860b18e5c6cd23/493ade0efede15ca?q=c%2B%2B+constructor+%22function+declaration%22&rnum=2#493ade0efede15ca)in the "comp.lang.c++.moderated" newsgroups speaks about this dichotomy.




among one of the workarounds posted is this :






    
    
      <font>//A a=A( B() );</font>
    







Which brings us to the motivations behind programmers declaring functions in local scope. One of the possible reason is to hide an overloaded function declaration. For example, in the following example, the local function declaration overrides the global function declaration:






    
    
    <font>#include</font> <iostream> 
    
    <font>void</font> f(<font>int</font> i) { std::cout << <font>"int="</font> << i << <font>'n'</font>; }
    <font>void</font> f(<font>short</font> s) { std::cout << <font>"short="</font> << s << <font>'n'</font>;}
    
    <font>int</font> main()
    {
        f(<font>1</font>); <font>// calls f(int)</font>
        <font>void</font> f(<font>short</font>);
        f(<font>1</font>); <font>// fooled you!</font>
    
    }
    







However this can be taken care of, by using Koenig lookup - which works only if there are namespaces or classes to be resolved (I dont think it works for primitive types).






    
    
    <font>#include</font> <iostream> 
    
    <font>class</font> X{};
    <font>void</font> f(X x, <font>int</font> i) { std::cout << <font>"int="</font> << i << <font>'n'</font>; }
    <font>void</font> f(X x, <font>short</font> s) { std::cout << <font>"short="</font> << s << <font>'n'</font>;}
    <font>int</font> main()
    {
        X x1;
    
        f(x1,<font>1</font>); <font>// calls f(int)</font>
        <font>void</font> f(X x, <font>short</font>);
        f(x1,<font>1</font>); <font>// fooled you!</font>
    
    }
    







Thaks to PK for this !!!




del.icio.us Tags: [software](http://del.icio.us/sss8ue/software) [c++](http://del.icio.us/sss8ue/c++) [g++](http://del.icio.us/sss8ue/g++) [compiler](http://del.icio.us/sss8ue/compiler)



