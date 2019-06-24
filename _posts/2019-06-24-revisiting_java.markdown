---
layout: post
title:      "Revisiting Java"
date:       2019-06-24 17:07:53 +0000
permalink:  revisiting_java
---


In my continuous quest to make myself employable, I recently revisited Java. This was the language used in my data structures class. My knowledge of linked lists, trees, hash tables etc. are intimately related with Java. Also, a lot of job listings have suggested at least a familiarity with it to be the ideal candidate. For all these reasons, I solved some HackerRank problems with it and also wrote a basic linked list class. Since my most proficient language is JavaScript, I thought it would be interesting to compare the two. 

When I considered the two languages side by side the most immediate difference is how both handle data types. A "loosely typed" language is one where you don't have to define the data type when you declare a variable. A "strongly typed" language is the opposite. JavaScipt is loosely typed whereas Java is strongly typed. 

Everything in Java must be explicitly defined as a certain type. Once a variable is defined, it can only operate with other variables of that type. The only language I had learned when I started with Java was Python, so I was not familiar with defining classes. Not only did it make me a better developer by forcing me to learn data types, but I felt that the rigidity saved me some headaches when debugging. 

All methods and functions in Java must be defined with their return value. I found this to be extremely helpful in complex classes. I was always certain that the method was returning what I was expecting it to, so there was one less thing to worry about when debugging. 

A developer moving from a language like Java to JavaScript should certainly expect some bugs in their near future. Not only does JS not worry about the type when declared, it is also dynamically typed. When two data types are attempted to be added together, compared, or some other operation, JavaScript automatically attempts to coerce them. For example:
```
12 + '1'
     -> '121'
		 
false == 0
     -> true
```
These are either beautiful or hideous, depending on how long you have been debugging. 
