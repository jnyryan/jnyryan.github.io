---
layout: post
title:  "Building a Software Engineering Framework that works for you"
date:   2013-05-13 00:00:00
categories: better-engineering-practices

---

This article and it’s posts are about about figuring out what engineering fundamental’s are missing as a delivery team and how putting them in place will not only ensure a better product delivery rate, but also less stressed teams and a overall better working environment. You won’t find a solution to your problem here but you will find ideas that will help you solve it yourself.


Every company, every delivery team, probably each product has it’s own style that requires a delicate touch that requires it’s own it’s own customizations. All to often, organizations attempt to create one all encompassing strategy to handle its builds, configurations, deployments and project management. With the growth of the Cloud, we can’t assume any longer that the majority of our applications will be 3-tier, internally hosted mammoth systems. These days, I spend my time writing distributed systems, internal message queue connected out to Salesforce CRM, syncing to Amazon Web Services with external front ends hosted on Heroku and internal sites running on our Internal Private Cloud. The good old days of having the whole system sitting on my laptop and hacking away end-to-end features while on a plane are well and truly gone.

It’s no surprise that as professional developers working in an enterprise environment we have all come across the same issues that slow down the whole process of delivering the product. I’ve lost count of the amount of times my team and I have moaned about awkward deployment processes, adding and removing features from releases, new features breaking existing one. Those are just the ones we can control, there’s also the ever changing requirements, release dates that only move closer and of course the uninterested Product Owners who on release day decided that you’ve delivered something totally different that what they wanted.

There is no golden solution for these problems. The truth is that each company is different and has different needs, wants and goals. However, the basics are still there. We want to architect good solutions, have good quality code, not be working late to catch up on unrealistic deadlines. We want to be able to focus on our job – be it coding, designing, documenting, architecting, testing or managing. We can’t do this if we are bogged down in consistently in tracking down production issues, supporting the operations team on deployments.

The powers-that-be in companies like to throw processes like SCRUM on top of them and walk away smiling saying “that’ll fix it”, but really all that does is bury the existing problems deeper and introduce a whole new set of issues. What they don’t realize is that in order to get the management processes running, the basics have to be in place.

#Where do you start?

There is a basic minimum that every team needs. You’ll find tens of methods of over engineering your environments, but the KISS method is always the best.. Keep It Simple Stupid. First, identify the pain points. Where is the majority of the teams day spent?

I divide these up into 3 basic areas

- Configuration Management
- Code and Quality Management
- Delivery Management

Each of these areas have systems and processes that can help a team achieve certain goals.

#Configuration Management

This covers identifying a teams most basic requirements for creating and managing changes in software. This is primarily to do with all the automated tasks. Everything from backing up your code to getting it into the public eye.

- Source Control
- Continuous Build
- Continuous Deployment
- Defect and Task Management
- Environment Management
- Change Control
- Work Item Tracking
- Packaging 


#Code and Quality Management

This covers techniques to make code better and more sharable. Allowing teams to easily share and hand-off work to each other. Reduce the “blocker” that is single developers having knowledge or ownership of code. Simple techniques exist to help manages these, a few examples…

- Code Reviews
- Coding Standards
- Code Introspection
- Unit Testing
- Quality metrics
- Defect Injection Management
- Managing technical Debt
- Pair Programming


#Delivery Management

Finally this topic covers those factors outside the teams control, or at least those that seem to be outside control – like managing delivery dates and scope of work to be done.

Feature and Backlog Management
Requirement Reviews
Scope Definition and Data Gathering
Project Estimation
Project Tracking
Release Planning and the Release Train
That seems like a lot to do…

If that’s what you think, then you’d be very right. To get teams to implement all the items above is a full time job that might not involve delivering any product. Instead the idea is to start at the beginning. Pick a single item to include in your day-to-day process. Give it a few weeks an if it works then keep it and add another. If not, it’s a lesson learned, throw it away and try something else.

REMEMBER. The idea of adding these is to increase productivity through reducing wastage. If all you’re doing is adding work for you staff… then it’s not for you. Iterative improvement is just that. Iterative.