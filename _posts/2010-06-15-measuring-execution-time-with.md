---
title: "Measuring Execution time with powershell"
layout: "post"
uuid: "6311353069381338898"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-6311353069381338898"
date: "2010-06-15 13:58:00"
updated: "2010-06-15 13:58:26"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "6311353069381338898"
    comments: "0"
categories: playing-with-technology
tags: [Powershell]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

This is an easy one - use measure-command CommandLet

	measure-command {
	# do your long running action in here, like loading a 	file
	@file = get-content “c:\MyFile.txt”
	}
<linebreak>
Output Looks like this:

	Days : 0
	Hours : 0
	Minutes : 0
	Seconds : 1
	Milliseconds : 638
	Ticks : 16386148
	TotalDays : 1.89654490740741E–05
	TotalHours : 0.000455170777777778
	TotalMinutes : 0.0273102466666667
	TotalSeconds : 1.6386148
	TotalMilliseconds : 1638.6148

You can also format the output by piping the output into the Filter-Table commandlet

	measure-command {
	# do your long running action in here, like loading a 	file
	@file = get-content “c:\MyFile.txt”
	} | ft -Property Hours, Minutes, Seconds, Milliseconds

Output Looks like this:

	Hours Minutes Seconds Milliseconds
	—– ——- ——- ————
	0 0 1 567
	
