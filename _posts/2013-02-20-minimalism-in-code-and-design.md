---
layout: post
title:  "Minimalism in code and design"
date:   2013-02-20 00:00:00
categories: better-engineering-practices 
description: 
categories: better-engineering-practices
tags: [practices, development]

---

###Minimalism. 
  
There are lots of ways to build (tools, languages) and I’ve seen many work in different companies, and I’ve seen mixed technologies work. There is one theme however to teams that deliver a lot of business value. They don’t repeat themselves. 
  
Now, I’d wager the first thing that hops into your mind with that phrase is code re-use. Or writing code to be re-used. Turns out, that’s not where you get leverage on re-use, you get it by re-using code someone, somewhere else has already written. Thinking about writing reusable code isn’t how you get leverage, reusing used code is.  
  
That’s not the real problem though. The real problem is data. If you take a big step back and look at what apps generally do is store and present data, and from time to time there is some algorithmics (search, AI suggestions, machine learned prediction models) – but most code that I’ve seen is in the business of storing data and fetching it with display to the user as a string, either as a web page or email.  
  
What we have is a substantial duplication of data concepts as a root cause for code complexity. The code is, in effect working around the lack of a singular data model. We won’t be able to fix the code until the data is fixed. 

  
###How do you get there in practice?  
Eliminate layers, which introduce copy/transform steps on data that rarely add value. Here is the challenge to each of you, particularly on the programming side. Take a look at some DTOs or containers, and the associated mappers from database or lower level on the layer stack objects. See how the data is marshaled and ask yourself – how does this add value to the data?  
Define the data once and only once, whether object, relational, document, or other make a single data model for each. 

Enhance data with metadata on a per entity/property basis, for example captions on fields – put them in the definition not all over in the code. Another example is validation, for a given entity/property there should be a singular validation command to constrain allowed values, javascript works well here as you can use it on UI and back end without recoding. Above all make it declarative.

Go incrementally, from your current place of duplication to a future place with less duplication. You don’t need to skip to perfect, we just need to get better each day. Making a ‘new solution’ only counts if it eliminates more than it adds, otherwise it becomes part of the redundancy. 
  
                                                                                                                                                        