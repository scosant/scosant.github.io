---
layout: post
title: number spiral diagonals
description: projecteuler028
date: '2011-05-16T17:09:00.002-05:00'
author: scott
tag:
- python
- mathematics
modified_time: '2013-02-20T11:03:09.594-06:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-2609897591170931321
blogger_orig_url: http://scosant.blogspot.com/2011/05/project-euler-problem-028-what-is-sum.html
---

This is easily solved by walking the spiral:<br />
<br />
<script src="https://gist.github.com/4317480.js"></script>
<br />
It can also be solved mathematically.  The top-right corner values clearly represent the area of the rectangle for a given depth (length from center to corner).  The top-left corner value can be found by subtracting the length_of_the_side from the area and adding one to account for the single corner.  The bottom-left corner can be found by subtracting two * length_of_the_side and adding two to account for the two corners.  The value at the bottom-right corner can be found in a similar way.  Therefore, we have the following equations:<br />
<br />
\[\begin{aligned}<br />
f_{topright}(y) &amp; = y^2 \\<br />
f_{topleft}(y) &amp; = y^2 - y + 1 \\<br />
f_{bottomleft}(y) &amp; = y^2 - 2y + 2 \\<br />
f_{bottomright}(y) &amp; = y^2 - 3y + 3<br />
\end{aligned} \]<br />
<br />
where y = length of the side for a given rectangle.  We can then find the sum of these four corner values:<br />
<br />
\[\begin{aligned}<br />
g(y) &amp; = f_{topright} + f_{topleft} + f_{bottomleft} + f_{bottomright} \\<br />
g(y) &amp; = y^2 + y^2 - y + 1 + y^2 - 2y + 2 + y^2 - 3y + 3 \\<br />
g(y) &amp; = 4y^2 - 6y + 6 \\<br />
\end{aligned} \]<br />
<br />
and modify it so that it is a function of the depth rather then the length of the side.<br />
<br />
\[\begin{aligned}<br />
let\ y(x) &amp; = 2x + 1,\ then \\<br />
g(x) &amp; = 4(2x+1)^2 - 6(2x + 1) + 6 \\<br />
g(x) &amp; = 16x^2 + 4x + 4<br />
\end{aligned} \]<br />
<br />
Finally, we can find the sum of all corners up to a certain depth using a Riemann sum:<br />
<br />
\[\begin{aligned}<br />
h(x) &amp; = \sum_{x=1}^m 16x^2 + 4x + 4 \\<br />
h(x) &amp; = \sum_{x=1}^m 16x^2  + \sum_{x=1}^m 4x + \sum_{x=1}^m 4 \\<br />
h(x) &amp; = 16\sum_{x=1}^m x^2  + 4\sum_{x=1}^m x + 4\sum_{x=1}^m 1 \\<br />
h(m) &amp; = 16\frac{m(m+1)(2m+1)}{6} + 4\frac{m(m+1)}{2} + 4m \\<br />
h(m) &amp; = \frac{16}{3}m^3 + 10m^2 + \frac{26}{3}m \\<br />
h(500) &amp; = 669171000<br />
\end{aligned} \]<br />
<br />
then add one to account for the center value.<br />
<br />
\[\begin{aligned}<br />
h(500) + 1 &amp; = 669171001<br />
\end{aligned} \]