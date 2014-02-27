---
title: "Accessing Remote Servers with other active users"
layout: "post"
uuid: "7514659054126749825"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-7514659054126749825"
date: "2011-11-16 10:30:00"
updated: "2012-11-23 13:29:46"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "7514659054126749825"
    comments: "0"
categories: playing-with-technology
tags: [Windows]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

If you ever have tried to remote to a server and the max number of connections are already estabilsted, here’s how to view the sessions remotely and terminate them:
<linebreak>

###QWINSTA 

View active connections on are remote server

```
C:\Users\jryan>qwinsta /?
Display information about Remote Desktop Sessions.

QUERY SESSION [sessionname | username | sessionid]
              [/SERVER:servername][/MODE] [/FLOW][/CONNECT] [/COUNTER][/VM]
```
|Option|Description|
|---|---|
|  sessionname          |Identifies the session named sessionname.|
|  username              |Identifies the session with user username.|
|  sessionid               |Identifies the session with ID sessionid.|
|  /SERVER:servername  |The server to be queried (default is current).|
|  /MODE                |Display current line settings.|
|  /FLOW                |Display current flow control settings.|
|  /CONNECT        |Display current connect settings.|
|  /COUNTER         |Display current Remote |Desktop Services counters information.|
|  /VM                     |Display information about sessions within virtual machines.|

``` bash
Example:
qwinsta /server: pc1.domain.com
```

###RWINSTA

Remove the active connections on a remote server 

```
C:\Users\ebyrne>rwinsta /?
Reset the session subsytem hardware and software to known initial values.

RESET SESSION {sessionname | sessionid} [/SERVER:servername][/V]
```
|Option|Description|
|---|---|
| sessionname | Identifies the session with name sessionname|
|sessionid | Identifies the session with ID sessionid.|
|  /SERVER:servername   |The server containing the session (default is current).|
|  /V                                  |Display additional information.|

Example:

``` bash
rwinsta 2 /server:pc1.domain.com
```

###MSTSC

Another method for stealing control of a server is to use Microsofts Terminal Services Console

``` bash
mstsc -v:192.168.1.2 /admin
```