---
title: "A Powershell GREP"
layout: "post"
uuid: "8370262704687799737"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-8370262704687799737"
date: "2010-02-17 18:09:00"
updated: "2010-02-18 13:50:54"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "8370262704687799737"
    comments: "0"
categories: playing-with-technology
tags: [Powershell]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---


Here’s a handy one for doing a GREP in PowerShell

Example 1

	Get-ChildItem -include .txt -recurse | Select-String “Hello”

Example 2

	Get-ChildItem -include .txt -recurse | Select-String “Hello” | Format-Table

Example 3

	Get-ChildItem -include *.txt -recurse | Select-String “Hello” | Format-Table -Property Path, LineNumber, Line -Autosize

This gets a collection of all “txt” files in the current directory and its sub directories, passes it to the “Select-String” which opens the file and look for the pattern “Hello”.

The Format-Table option allows you to display the results in a more readable format. You can also use “Format-List”

In example 3 I added the AutoSize property so the Path info wouldn’t get truncated.