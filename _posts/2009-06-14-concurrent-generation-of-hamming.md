---
layout: post
category: blog
title: concurrent generation of hamming numbers
description: fun programming homework
date: '2009-06-14T05:56:00.030-05:00'
author: scott
tag:
- state-machine
- java
image: https://unsplash.it/560/120?random
headerImage: true
comments: false
modified_time: '2012-12-17T06:45:02.459-06:00'
thumbnail: http://3.bp.blogspot.com/_4yzBNmd0Mow/SlAjJMjUlLI/AAAAAAAABLQ/3d30U7XwL_I/s72-c/diagram.png
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-1430157865796583378
blogger_orig_url: http://scosant.blogspot.com/2009/06/concurrent-generation-of-hamming.html
---

This was a fun little program I had to do for a concurrent programming course. It generates Hamming numbers, which are numbers of the form (2^k)(3^m)(5^n), where k, m and n are non-negative integers.

It has the following design:
<a href="http://3.bp.blogspot.com/_4yzBNmd0Mow/SlAjJMjUlLI/AAAAAAAABLQ/3d30U7XwL_I/s1600-h/diagram.png" ><img alt="" border="0" id="BLOGGER_PHOTO_ID_5354818597838689458" src="http://3.bp.blogspot.com/_4yzBNmd0Mow/SlAjJMjUlLI/AAAAAAAABLQ/3d30U7XwL_I/s400/diagram.png" style="cursor: pointer; display: block; height: 212px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a>

Each dotted line represents a blocking queue and each box represents an individual thread. The "Multiply" boxes take an input and multiply it by it's respective constant.  These are then fed into the "3-In Ordered Merge" thread which takes the minimum value and sends it to the "4-Out Copy" thread.  This thread then sends it to the "print" thread while also sending it to the "Multiply" threads. This is an elegant example of transforming a serial program into a concurrent one.

<script src="https://gist.github.com/4318020.js"></script>