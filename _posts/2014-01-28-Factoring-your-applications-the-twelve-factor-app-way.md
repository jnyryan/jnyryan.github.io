---
layout: post
title:  "Factoring your applications the Twelve Factor App way"
date:   2014-01-28 00:00:00
categories: better-engineering-practices 
description: 
categories: better-engineering-practices
tags: [practices, development, methodologies]

---
The **Twelve Factor App** is something I came across that a while ago that resonates with my thought process. It's primarily for *software-as-a-service* applications but so much of it can be abstracted to be applied to many other forms of systems.
	
What really rings through is that the version of code in source control is the live version, config is stored in the environment and logging is just a stream to standard out to be consumed as needed. Implementing these alone get a development team to a stage where an application can be deployed from git/svn/other to any environment be it production/staging or just a developers laptop with one click.

Does it work? Yes, I've been doing it for years!

###I. Codebase
One codebase per app tracked in revision control and can be deployed to many environments

###II. Dependencies
Explicitly declare and isolate dependencies. If you have binary dependencies check them in and make them part of the application. It's *Version Control* not *Source Control* 

###III. Config
Store config in the environment - don't tie your repository to a specific configuration. 

###IV. Backing Services
Treat backing services as attached resources

###V. Build, release, run
Strictly separate build and run stages

###VI. Processes
Execute the app as one or more stateless processes

###VII. Port binding
Export services via port binding

###VIII. Concurrency
Scale out via the process model - managing threads is hard. Processes are free.

###IX. Disposability
Maximize robustness with fast startup and graceful shutdown

###X. Dev/prod parity
Keep development, staging, and production as similar as possible

###XI. Logs
Treat logs as event streams - other services like *Splunk* can consume them.

###XII. Admin processes
Run admin/management tasks as one-off processes. This is just cost efficient.

The full article is available on [http://12factor.net/](http://12factor.net/) and is worth a read.