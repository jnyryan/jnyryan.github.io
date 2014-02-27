---
title: "PowerShell and Large Files"
layout: "post"
permalink: "/2010/06/powershell-and-large-files.html"
uuid: "1411452767162325156"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-1411452767162325156"
date: "2010-06-15 13:36:00"
updated: "2010-06-15 13:37:14"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "1411452767162325156"
    comments: "0"
categories: playing-with-technology
tags: [Powershell]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

I recently needed to write a script to get some data from a XML file, in this case all IDs of Topic Elements. Decided to use Powershell but quickly ran into an issue due to the size of the uncompressed file... 127MB. Here's my initial script:

{% highlight powershell%}
# Get the ids
$File = .\myFile.xml
[xml]$topic = get-content $File
$arrayTopicIds = $topic.TopicResults.Topic | %{$_.Authors.Author} | %{$_.Id}
{% endhighlight %}

Needless to say, it consumed all my memory and froze my machine.

Undeterred, I turned to the -FilterScript. Rather than use an XML object, I used the get-content commandlet to load the file into an array of end-line-delimited strings. And since i knew the pattern i was looking for i was able to use the -FilterScript command to filter the processed lines. At the same time also formatted the string to how i wanted it:

{% highlight powershell%}
# Get the ids
#$topic = get-content $File | Where-Object -FilterScript { $_ -ilike “*Author id=*” } | %{ $_ - replace "" } | %{ $_.Trim() }
{% endhighlight %}

Simple and ended up running in under 4 minutes. Which was nice.