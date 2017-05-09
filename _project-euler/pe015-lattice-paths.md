---
layout: post
title: lattice paths
description: projecteuler015
date: '2010-04-21T04:13:00.011-05:00'
author: scott
tag:
- c++
modified_time: '2013-02-20T11:03:09.587-06:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-1629302030286368477
blogger_orig_url: http://scosant.blogspot.com/2010/04/starting-in-top-left-corner-in-20-by-20.html
---

This can be solved by applying Pascal's triangle.  One can easily determine the number of paths to the destination by working backwards.  Here is an example using a 4x4 grid (note that there is a zero column/row).  Start with an empty grid:<br />
<div style="font-family: &quot;Courier New&quot;,Courier,monospace;">
<br /></div>
<span style="font-family: 'Courier New', Courier, monospace;">&nbsp; </span><b style="font-family: &quot;Courier New&quot;,Courier,monospace;">0   1   2   3   4</b><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">0</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   0</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">1</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   0</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">2</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   0</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">3</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   0</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">4</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   0</span><br />
<br />
Along the left and bottom edges, there is only one direct path to the endpoint from any point.<br />
<br />
<span style="font-family: 'Courier New', Courier, monospace;">&nbsp; <b>0   1   2   3   4 </b></span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>0</b>   0   0   0   0   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>1</b>   0   0   0   0   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>2</b>   0   0   0   0   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>3</b>   0   0   0   0   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>4</b>   1   1   1   1   1</span><br />
<br />
At (4, 4), there are two paths leading to the end.&nbsp; One can travel right-&gt;down or down-&gt;right.&nbsp; This is the sum of the values to the right of and below the current point (in other words, the points that would lead to the endpoint without backtracking).<br />
<br />
<span style="font-family: 'Courier New', Courier, monospace;">&nbsp;     </span><b style="font-family: &quot;Courier New&quot;,Courier,monospace;">0   1   2   3   4 </b><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">0</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   1</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">1</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   1</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">2</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   0   1</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">3</b><span style="font-family: 'Courier New', Courier, monospace;">   0   0   0   2   1</span><br />
<b style="font-family: &quot;Courier New&quot;,Courier,monospace;">4</b><span style="font-family: 'Courier New', Courier, monospace;">   1   1   1   1   1</span><br />
<br />
Additionally, the path above it would have three paths to the end.&nbsp; These are (1) right-&gt;down-&gt;down, (2) down-&gt;right-&gt;down and (3) down-&gt;down-&gt;right.&nbsp; Again, this is the sum of the values below and to the right of the current point.&nbsp; This same process can be applied to all values in row 4.<br />
<br />
<span style="font-family: 'Courier New', Courier, monospace;">&nbsp;     <b>0   1   2   3   4</b></span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>0</b>   0   0   0   5   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>1</b>   0   0   0   4   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>2</b>   0   0   0   3   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>3</b>   5   4   3   2   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>4</b>   1   1   1   1   1</span><br />
<br />
This process must then be repeated by filling in rows/columns closest to the endpoint.<br />
<br />
<b><span style="font-family: 'Courier New', Courier, monospace;">&nbsp;&nbsp;       0&nbsp;    1&nbsp;    2&nbsp;   3&nbsp;   4</span></b><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>0</b>   70  35  15&nbsp;   5&nbsp;   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>1</b>   35  20  10&nbsp;   4&nbsp;   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>2</b>   15  10&nbsp;   6&nbsp; 3&nbsp;   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>3</b>&nbsp;     5&nbsp;    4&nbsp;   3&nbsp;    2&nbsp;   1</span><br />
<span style="font-family: 'Courier New', Courier, monospace;"><b>4</b>&nbsp;     1&nbsp;    1&nbsp;   1&nbsp;    1&nbsp;   1</span><br />
<br />
So for a 4x4 grid, there are 70 paths from the top-left point to the bottom-right point.&nbsp; (Note that in this example, the value at a specific point is the number of paths from that point to the endpoint (bottom-right).&nbsp; In the code, the values are reversed, and the value at a specific point is the number of paths from the beginning (top-left) to that specific point.<br />
<br />
<script src="https://gist.github.com/4317543.js"></script>