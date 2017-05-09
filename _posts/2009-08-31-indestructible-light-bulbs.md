---
layout: post
category: blog
title: indestructible light bulbs
description: how high can you drop a light bulb
date: '2009-08-31T22:22:00.007-05:00'
author: scott
tag:
- puzzles
modified_time: '2010-11-02T12:01:34.440-05:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-8753112210906803930
blogger_orig_url: http://scosant.blogspot.com/2009/08/indestructible-light-bulbs.html
---

#### Problem

You have 2 supposedly unbreakable light bulbs and a 100-floor building. Using fewest possible drops, determine how much of an impact this type of light bulb can withstand. (i.e. it can withstand a drop from 17th floor, but breaks from the 18th).&nbsp; Note that the ever-popular binary search will give you a worst case of 50 drops. You should be able to do it with under 20. (<a href="http://maxnoy.com/interviews.html">Source</a>)

#### Solution

##### Naive Approach

The naive approach for this problem would be to simply start at the bottom floor and continually dropping it at higher floors until it breaks. This would require only one indestructible light bulb and have a worst case of 100 drops. The binary search has a worst case of 50 drops because if you drop it at 50, you still have the other 50 to check. If the light bulb breaks, you only have one light bulb left and must start from the lowest remaining floor and move up.

##### Increments of 20

Now, suppose we drop it in increments of 20. The worst case word occur if it broke at floor 80. We would only have one bulb left and must drop it starting at floor 61 all the way to floor 79. This would have a worse case of 4+18=22 drops.

One might think the worst case occurs if the bulb does not break at 80, but remember, you still have two light bulbs left. You can now test in increments of 5 (85,90,95) and have a worst case of 4+3+5=12 drops.

##### Increments of 10

What about increments of 10? The worst case would occur if highest floor at which the bulb breaks is 89. The first bulb would break at 90, at which you must now test floors 81-89 in order. This would have a worst case of 9+9=18 drops.

Now, suppose the bulb survives the drop at floor 90. You still have two bulbs left and can do a binary search. In the worst case, the bulb breaks at floor 95, and you must now test floors 91-94 in order. This results in a worst case of 9+1+4=14 drops. However, this is still a more ideal case than the previous.

##### Increments of 15

Again, in the worst case, it breaks at floor 90 and you must now test floors 76-89 in order. This results in a worst case of 6+13=19 drops, slightly worse than increments of 10. Also notice that if it does not break at floor 90, you have the same scenario as with dropping in increments of 10.<br />

##### The Best Worst-Case

Because of this, it is likely that dropping it in increments of 10 will yield the best worst-case.