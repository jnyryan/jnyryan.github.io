---
layout: post
title:  "Source Control Management"
date:   2013-07-09 00:00:00
categories: better-engineering-practices
tags: [practices, development]

---

Source Control Management (SCM) also called a Version Control System (VSC) is the cornerstone of enterprise software development. Simply put, it provides an easy means for developers to manage their source code in terms of sharing, tracking and security – giving teams (and individual coders) the flexibility that they need to produce high quality reliable code with the safety that they know all changes to code can be retrieved/monitored and undone if necessary. The alternative is to keep the source code in a folder somewhere on a network, but then think how hard it would be to do the following:

- Keep a history of changes to files
- Allow multiple developers to work on a file at once
- View the differences between files
- Allow for multiple different features to be developed simultaneously
- Allow for whole code streams to be merged together easily
- Create snapshots the state of the source at a point in time (so you know what’s deployed)
- Track who made what changes and when (useful for determining when a bug was introduced)
lots lots more…..
- So what exactly is a SCM tool

It’s a tool that you download and install on a server (internal to a household or company) or a cloud based service that you connect to – that is a secure database of all your code (called a repository). The administrator sets up users on the system and provides the users with a URL to connect to. The end-users then simply download the client tool onto their PC and pull the code code they want to work on onto their machine. When they have made a change they’re happy with they push it back to the repository. Other users then can get your changes when they update their local repository. The beauty is the system helps manage changes like if another user also edited the same file either resolving them automatically or allowing the user to choose the differences to use. You’ll find my personal repository on Github.

Each SCM system has it’s own guidelines on how to layout your branches and tree structures so it’s always a good idea to read the best practices on the system you use (e.g. Subversion Best Practices).

Tip: Try a few services for yourself on your own code to decide on which you prefer before bringing one option into work.

### Terminology

|Term|Description|
|-----------------------|--------------|
|Repository| the database containing the source code|
|Trunk/Master|the main stream of code, usually defined what is currently in production. When a new feature is to be added, the developer will create a branch from this Trunk/Master and when it is ready to be released -merge it back into trunk/master|
|Branching|the process of copying the code into two separate areas so that new features can be worked on independently, thus if one is finished before the other – they can be tested and released separately.|
|Merging|the process where two branched codebases are merged together into a parent stream.|
|Forking|forking is similar to branching but usually refers to creating a branch that may never rejoin the master – as in forking the open source repository of Linux to make your own version.|
|Tagging|this is a way of recording the state of your repository so that you can always get to a certain point in the code if needed.|
|Check-out / Clone|when a developer pulls the latest code from the repository to their machine|
|Check-in / Commit / Push|when a developer wants the code they worked on to be save back to a central repository|

### Types of Source Control Management

|Type|Description|
|-----------------------|--------------|
|Centralized|This is the most common type of system used by large companies. It’s basically a central server (with proxies for scalability) that holds all your code in a database with a management system on top of it that allows your code to be edited/forked/branched/merged/tagged. Users download the client software onto their development machines and connect to the central server. All code required is the downloaded onto the clients machine and the developer works on the code as needed. Merging facilities are provided by the SCM system allowing several developers to working on the same codebase simultaneously.|
|Distributed|These are becoming more popular these days as they provide a way for developers to work off line. Essentially, every developer has their own code repository locally and can link to remote repositories pulling in other peoples changes or requesting their own to be added into a main stream. Take for example if a developer wanted to work on an Open Source project that was available on an online distributed repository. The developer would fork the main repository and make changes to that codebase. If the the developer decided that their changes were ready for the main product they would make a request to the main branch owner for their branch to be merged into the main stream.|

### Popular SCM Tools

There are dozens of free and paid for solutions available with the most popular these days being Subversion and Git – here are a few:

|Tool|Description|
|-----------------------|--------------|
|Subversion (svn)|This seems to be the most popular centralized SCM at the moment with a lot of support and tools. I like it a lot. There are many free cloud based versions of this that provide free single user experience|
|Git|This is my current SCM of choice and is a popular decentralized system. It’s used a lot in open source development due to it’s ease of forking and remerging. This has a steep learning curve if your coming from the likes of SVN, but is worth it.|
|Github|This is a centralized version of above, I use it a lot and there are free versions available.|
|Accurev|A graphical management system that allows features to be added and removed via a drag and drop UI. Have not used this but heard only good reviews.|
|Mercurial (hg)|A lot of big systems use this and it seems very popular. I’ve only ever pulled code from it to build locally|
|Perforce|I used this years ago and was very happy with it. Provides many features and very scalable.
|Visual Sourcesafe|Microsoft’s SCM that is now part of Team System. A very good system with excellent reporting and plugins for SCRUM systems.|
|CVS|The old school that people are moving from. Never used it directly.|

###Online Source Control

Whether your a professional or novice coder having your library of apps and scripts in one place is a fantastic advantage - there's no shortage of free online solutions either. You can sign up to any of these and they'll give you a few hundred MB of space to get started with. 

|Tool|Description|
-----------------------|--------------
|BitBucket|[www.bitbucket.com](www.bitbucket.com)|
|github|[www.github.com](www.github.com)|
|Unfuddle|[www.unfuddle.com](www.unfuddle.com)|
	 