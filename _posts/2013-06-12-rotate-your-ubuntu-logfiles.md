---
title: "Rotate your Ubuntu Logfiles"
layout: "post"
uuid: "2231292098669152309"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-2231292098669152309"
date: "2013-06-12 12:48:00"
updated: "2013-06-12 12:48:50"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "2231292098669152309"
    comments: "0"
categories: "playing-with-technology"
tags: [ubuntu, bash]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

Running out of diskspace coz you over-log?

Well first, there are never too many logs!

Managing your logs is the trick. In ubuntu there’s a service/daemon that manages this for you called rsyslog, that will ensure your logs are kept in order. The service will delete logs that go stale according to the settings in the config file. Below the process “syslog” is rotated daily, that is every day a new file is created and a index number appended onto the end of the file. The rotate value is set to 2, which means only hold 2 rotated logs and delete the rest. The other services in the config file are set to weekly rotation and to be rotated every 4 weeks.

### Edit the config file

{% highlight bash %}

sudo vi /etc/logrotate.d/rsyslog

/var/log/syslog
{
        rotate 2
        daily
        missingok
        notifempty
        delaycompress
        compress
        postrotate
                reload rsyslog >/dev/null 2>&1 || true
        endscript
}

/var/log/mail.info
/var/log/mail.warn
/var/log/mail.err
/var/log/mail.log
/var/log/daemon.log
/var/log/kern.log
/var/log/auth.log
/var/log/user.log
/var/log/lpr.log
/var/log/cron.log
/var/log/debug
/var/log/messages
{
        rotate 4
        weekly
        missingok
        notifempty
        compress
        delaycompress
        sharedscripts
        postrotate
                reload rsyslog >/dev/null 2>&1 || true
        endscript
}
{% endhighlight %}

### Restart the service

{% highlight bash %}
sudo service rsyslog restart
{% endhighlight %}
