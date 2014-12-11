---
layout: post
title:  "WiFi-Sniffing-on-OSX-using-airport"
date:   2014-07-29 00:00:00
categories: forensics-and-security
description:
tags: [practices, development, security]

---

``` bash
sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/bin/airport
```


Many Mac OS X users lament the lack of sophisticated network analysis tools, often prevalent and seemingly prolific on Linux systems. What many don’t know is that Mac OS X comes with a built-in command-line tool to do all sorts of nifty things with Wi-Fi networks, from packet capture (traffic sniffing) to scanning nearby networks’ signal to noise ratios.

Mac OS X ships with a command-line tool called airport that can do all sorts of nifty things with Wi-Fi networks. Unfortunately, it’s so squirreled away that most people don’t seem to know about it. The utility is part of the Apple80211 Private Framework used to power your Mac’s Airport menubar icon.

Invoking the utility without arguments prints a useful (if incomplete) usage message. At a Terminal command prompt, type:

/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport
The tool let’s you do a number of interesting things, so it’s worth playing around with. While you’re playing, you may as well create a symlink (a shortcut) to the utility so you don’t have to type that long path name all the time:

sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/bin/airport
Among the easiest things you can do is print a list of the Wi-Fi networks within range of your computer, but unlike the Airport menubar item, this report shows you a bunch of extra, precise data, such as which encryption protocol (if any) is being used on the network:

$ airport en1 scan
                            SSID BSSID             RSSI CHANNEL HT CC SECURITY (auth/unicast/group)
                       moscohome 00:22:6b:8b:86:51 -61  10      N  -- WPA2(PSK/AES/AES)
                     PUBLIC-455H 00:15:6d:60:95:d1 -82  1       N  -- NONE
                    Alex Network 00:1e:e5:24:c4:4f -86  1       Y  TW WPA(PSK/TKIP,AES/TKIP) WPA2(PSK/TKIP,AES/TKIP)
                   linksysELNIDO 00:21:29:a3:fd:99 -90  6       N  -- WPA(PSK/AES,TKIP/TKIP) WPA2(PSK/AES,TKIP/TKIP)
                        2WIRE024 00:18:3f:02:2f:49 -88  6       N  US WEP
                        2WIRE940 00:12:88:d9:85:41 -93  6       N  US WEP
If I wanted to see which of my neighbors still haven’t upgraded from WEP, I could just filter using grep:

airport en1 scan | grep WEP
More awesome, perhaps, is the tool’s ability to actually perform traffic sniffing and capture packets. Tell airport to sniff, and optionally provide a channel (which you now know thanks to your ability to scan). You need to be an administrator (i.e., you need sudo privileges) to do this:

sudo airport en1 sniff 6
This creates a file called airportSniffXXXXXX.cap in the /tmp directory, where XXXXXX is a string for uniqueness. You can then feed this file into your favorite network analyzer such as Wireshark to examine the traffic offline.


airport -I
