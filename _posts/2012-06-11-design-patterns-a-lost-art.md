---
title: "Design Patterns - A lost art?"
layout: "post"
uuid: "2413489383813035000"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-2413489383813035000"
date: "2012-06-11 10:52:00"
updated: "2012-06-11 10:52:39"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "2413489383813035000"
    comments: "0"
categories: better-engineering-practices
tags: [practices, development]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"

---

A few months ago i was standing around the work coffee machine with a colleague when he blurted out “do you ever study design patterns in university?”. Now rather than take this as a personal affront to my coding style - I cast my mind back about 20 years and had to answer “no” - and this made me think.
<linebreak>
His question stemmed from the round of interviews we were conducting for an open senior developer. Very few of the interviewees could answer the simplest design pattern questions like “describe the factory pattern or singleton pattern”- or even “What’s your favourite pattern or one you find yourself using the most often”. Now it wasn’t just a case of them forgetting, which i have no problem with, there are lots of different names for patterns and coders just use them without thinking - or so i thought. It seems that something that i take for granted now is not

That got me thinking, how much do i really know about design patterns and how much do i practice.

So this is my quick recap on those patterns, their categories and when to use them(their Intent).   

What are design patterns
Simply put, design patterns are existing solutions to common software problems. In much the same way a carpenter has particular methods of joining wood together such as a ‘tongue and groove’ or a ‘lap joint’, in software may very smart people have spent a lot of time developing methods that have proven to be best in class for particular everyday code problems. The most famous of these are a group of people known as the Gang Of Four or GOF. They spent a lot of time categorizing and formalizing design patterns into a scheme that is easy to follow and remember.

|Pattern|Categories|
|---|---|
|Construction|	Builder, Factory , Abstract Factory, Prototype, Memento|
|Interface|	Adapter, Bridge, Composite, Facade|
|Operation|	Template, State, Strategy, Command, Interpreter|
|Responsibility|	Singleton, Observer, Mediator, Proxy, Chain of Responsibility, Flyweight|
|Extension|	Decorator, Iterator, Visitor|


###Patterns Intent
The following describes when to use each pattern. So browse through the scenarios below and next time you come across one of the times to use the pattern, why not give it a go there are plenty of examples on the web for all manor of languages - you can even look at my library of design pattern examples

|Construction|When to use|
|---|---|
|Abstract Factory|Creates an instance of several families of classes|
|Builder |                    Separates object construction from its representation|
| Factory|                    Creates an instance of several derived classes|
| Memento|                 Capture and restore an object’s internal state|
| Prototype|                 A fully initialized instance to be copied or cloned|

|Interface                   |When To Use|
|---|---|
|Adapter   |                 Match interfaces of different classes
|Bridge |                     Separates an object’s interface from its implementation|
|Composite |               A tree structure of simple and composite objects|
|Facade|                     A single class that represents an entire subsystem|

|Operation|         When To Use|
|---|---|
|Command |                Encapsulate a command request as an object|
|Interpreter |                A way to include language elements in a program|
|Observer |                  A way of notifying change to a number of classes|
|State|                         Alter an object’s behavior when its state changes|
|Template Method|      Defer the exact steps of an algorithm to a subclass|

|Responsibility |         When To Use|
|---|---|
|Chain of Resp. |        A way of passing a request between a chain of objects|
| Flyweight  |               A fine-grained instance used for efficient sharing|
| Mediator |                 Defines simplified communication between classes|
| Observer |                A way of notifying change to a number of classes|
| Singleton |                 A class of which only a single instance can exist|


|Extension|         When To Use|
|---|---|
|Decorator|                Add responsibilities to objects dynamically
|Iterator|                    Sequentially access the elements of a collection|
|Visitor|                      Defines a new operation to a class without change|
