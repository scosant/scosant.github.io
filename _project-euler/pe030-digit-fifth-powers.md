---
layout: post
title: digit fifth powers
description: projecteuler030
date: '2012-12-22T00:28:00.000-06:00'
author: scott
tag:
- python
- mathematics
modified_time: '2013-02-20T11:03:09.589-06:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-1748125396264246729
blogger_orig_url: http://scosant.blogspot.com/2012/12/projecteuler030.html
---

The logic is straight-forward.  The main thing that needs to be considered is the max number to check.  We can determine this by inspection.  For each additional digit, the number grows by an order of magnitude.  The maximum value of the fifth power of a digit is<br />
\[\begin{aligned}<br />
9^5 &amp;= 59049<br />
\end{aligned}\]<br />
and for each additional digit, it will grow linearly.  Eventually, the number itself will far exceed the sum of the fifth powers of its digits:<br />
\[\begin{aligned}<br />
9 &amp; &lt; 59049 \\ 99 &amp; &lt; 118098\ (or\ 2*59049) \\ 999 &amp; &lt; 177147\ (or\ 3*59049) \\ 9999 &amp; &lt; 295245\ (or\ 4*59049) \\ 99999 &amp; &gt; 354294\ (or\ 5*59049)<br />
\end{aligned}\]<br />
We can see that the maximum possible value for this number will be a 5-digit number.<br />
<br />
<br />
<script src="https://gist.github.com/4357777.js"></script>