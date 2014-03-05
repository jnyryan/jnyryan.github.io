---
layout: post
title:  "Analysing a network with google enumeration"
date:   2014-01-16 00:00:00
categories: better-engineering-practices forensics-and-security playing-with-technology
description: 
tags: [practices, development]

---

Google searches alone can reveal a huge amount of information on networks and the data contained on them. These are just a few of the quick searches that will reveal information that could otherwise be considered to be unavailable to the public.

***I think a  disclaimer here is appropriate. I am publishing these for educational purposes only. Just because a front door is open it doesn't mean that you can just walk in. These searched are legal in this sence as the information is public, but use any resources found responsibily.***

1. Find all sites with directory browsing enabled

	intitle: index.of "parent directory" site: .dcu.ie

2. Locate any Excel files on a network

This is a very easy search to see if any spreadsheets are available publicly.

	Filedype:xls site:.dcu.ie

3. Finding password files

