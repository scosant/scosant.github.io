---
layout: post
category: blog
title: why do home routers suck?
description: six routers and counting
date: '2010-03-06T22:01:00.001-06:00'
author: scott
tag:
- networking
image: https://unsplash.it/560/120?random
headerImage: true
comments: false
modified_time: '2010-03-07T00:25:20.551-06:00'
thumbnail: http://2.bp.blogspot.com/_4yzBNmd0Mow/S5McpCt00FI/AAAAAAAACss/_a5NxI1jYt0/s72-c/Netgear-RangeMax-WNR3500L-Wireless-N-Router-with-USB.jpg
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-3544658642828486375
blogger_orig_url: http://scosant.blogspot.com/2010/03/why-do-home-routers-suck.html
---

Of all the computer equipment I have ever purchased, none has been replaced more often than the wireless router. During my undergraduate years, my roommates and I replaced our router at least once per year. We went through multiple D-Link, Netgear and Linksys 802.11b/g models, always thinking that "this time, we won't have any issues." In college, I distinctly remember having to reboot the router at least once per week.

Approximately two years ago, I purchased a Linksys WRT310N for fast wireless-n and gigabit connections. Today, it can make connections with all devices EXCEPT FOR THE CABLE MODEM. Reviews indicate that this particular Linksys model has <a href="http://lmgtfy.com/?q=wrt310n+overheating">overheating issues</a>. This is unacceptable. Do they expect people to hack a fan onto it? Three months ago, my girlfriend purchased a brand new Linksys WRT54G2, because her previous Netgear router had connection issues. The new router continues to have connection issues that require the good old "unplug it/plug it back in" solution.

This baffles me because a "hard reboot" of any other computer device is generally considered a last resort. Yet, when a router stops working, it's the first solution that many people will try. The administration page can't be checked because there is no connection. Troubleshooting is often limited to checking the blinking lights on the router, and, well, resetting it.

Eventually, I became so frustrated with my router that I decided to load up the <a href="http://www.dd-wrt.com/site/index">DD-WRT</a> custom firmware. It is well-known for improving reliability and performance and adding features that can "turn a $30 router into a $500 router". Admittedly, many of these features are overkill for a home networking environment. However, there are a few things that I found extremely useful:

1. local name lookups for DHCP clients using DNSMasq
2. SSH server (primarily for waking up PCs behind the router)
3. DDNS
4. VPN
5. Port-Forwarding
6. QoS (with choice of two packet schedulers: HTB and HFSC)
7. ability to use router USB port for NAS or printer
8. and most useful, the ability to use the router as an access point, client, client-bridge, ad-hoc, repeater or repeater-bridge.

That last thing is especially clutch since I stream a lot of media to a Playstation3. Since the wireless adapter built into the PS3 sucks, it causes constant stuttering when streaming large movie files from a desktop PC. Plugging the PS3 into an old router via Ethernet and configuring the router as a client-bridge results in stutter free media streaming. DD-WRT allowed me to salvage old routers as client and repeater-bridges.

For anyone else who has issues with their router, I suggest looking into DD-WRT. If your router is problem-free, then consider yourself lucky and enjoy it while it lasts. If you are looking for a new router, I would suggest the <a href="http://www.newegg.com/Product/Product.aspx?Item=N82E16833122334&amp;Tpk=wnr-3500l">Netgear WNR3500L</a>, my most recent router-of-choice. Not only does it have the wireless-n and gigabit ports that I have come to enjoy, but it is open source and specifically designed to accept custom firmware like DD-WRT. In fact, there is <a href="http://www.myopenrouter.com/">DD-WRT-based custom firmware specifically designed for this Netgear model</a>. I've only had it for a week, but this time, I won't have any issues.