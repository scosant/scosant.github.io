---
layout: post
category: blog
title: fixing suspend and enabling wol on ubuntu jaunty
description: ubuntu jaunty power issue
date: '2009-04-26T18:28:00.002-05:00'
author: scott
tag:
- linux-troubleshooting
image: https://unsplash.it/560/120?random
headerImage: true
comments: false
modified_time: '2010-03-05T03:09:52.944-06:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-8330345587057660038
blogger_orig_url: http://scosant.blogspot.com/2009/04/fixing-suspend-and-enabling-wol-on.html
---

I had some issues with suspend/resume on previous versions of Ubuntu, but it seems that most of them have been fixed in Jaunty.  With a brand new installation of Jaunty, the system will suspend but will immediately resume.   This bug was highlighted [here](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/291300).

I used the fix by Geoff Goehle and created the file `etc/pm/config.d/usb_suspend_workaround` with the line:

    SUSPEND_MODULES="ehci_hcd uhci_hcd ohci_hcd usbcore"

After adding this file, resume/suspend should work correctly (my system has an evga 750i FTW motherboard).

Enabling WakeOnLan takes a few more steps.  First, make sure you enable it in your BIOS.  To check if your network card supports it, do

    sudo ethtool eth0

in your terminal.  if WOL is supported, you will see the lines

    Supports Wake-on: g Wake-on: g

If there is a 'd' by Wake-on, then you need to enable WOL.  Do this by executing

    sudo ethtool -s eth0 wol g

This will turn on WakeOnLan but only for your current session.

To automatically enable WOL when your system starts, create the file: `/etc/init.d/wakeonlanconfig` with the lines:

``` bash
    #!/bin/bash
    ethtool -s eth0 wol g exit
```

and execute

    chmod a+x wakeonlanconfig

to give everyone execute permissions. To make the script automatically run, execute

    update-rc.d -f wakeonlanconfig defaults

If you want to remove these startup scripts, replace "defaults" with "remove".  These steps were referenced <a href="http://ubuntuforums.org/showthread?t=234588">here</a>.  EDIT:  I seem to have additional problems with a blank screen after resuming.  I think it might be <a href="https://bugs.launchpad.net/ubuntu/+source/linux/+bug/229806">this bug</a>.