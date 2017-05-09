---
layout: post
title: smallest multiple
description: projecteuler005
date: '2010-03-04T16:44:00.005-06:00'
author: scott
tag:
- mathematics
modified_time: '2013-02-20T11:03:09.601-06:00'
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-3132667843941436149
blogger_orig_url: http://scosant.blogspot.com/2010/03/smallest-number-that-is-evenly-disible.html
---

<span style="font-size: small;">Project Euler - Problem 005</span><br />
<br />
<b>Problem</b><br />
2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder.  What is the smallest number that is evenly divisible by all of the numbers from 1 to 20?<br />
<br />
<b>Solution</b><br />
A computer isn't necessary to solve this quickly.&nbsp; All numbers can be factored into its prime numbers.&nbsp; Since the answer we want will be divisible by all numbers between 1 to 20, the answer will be the product of the set that intersects all sets of prime numbers for each number&nbsp; The set can also be built in the following way: <br />
<ul>
<li>2 is prime so add it to the set the set {2}.</li>
<li>3 is prime so add it to the set {2, 3}.</li>
<li>4 is a product of 2 * 2 so the set now contains {2, 3, 2}.</li>
<li>5 is prime so add it to the set {2, 3, 2, 5}.</li>
<li>6 is a product of 2 * 3. the set already contains a 2 and a 3 so it doesn't change.</li>
<li>7 is prime so add it to the set {2, 3, 2, 5, 7}.</li>
<li>8 is a product of 2 * 2 * 2 so add another 2 to the set and it becomes {2, 3, 2, 5, 7}.</li>
<li>9 is a product of 3 * 3 so add an additional 3 to the set and it becomes {2, 3, 2, 5, 7, 3}.</li>
<li>10 is a product of 2 * 5 so it doesn't change.</li>
<li>11 is prime so add 11 to the set and it becomes {2, 3, 2, 5, 7, 3, 11}.</li>
<li>12 is a product of 2 * 3 * 2 so nothing needs to be added.</li>
<li>13 is prime so add it to the set and it becomes {2, 3, 2, 5, 7, 3, 11, 13}.</li>
<li>14 is a product of 7 * 2 so nothing needs to be added.</li>
<li>15 is a product of 3 * 5 so nothing needs to be added.</li>
<li>16 is a product of 2 * 2 * 2 * 2 so add two 2's {2, 3, 2, 5, 7, 3, 11, 13, 2, 2}</li>
<li>17 is prime so add it to the set {2, 3, 2, 5, 7, 3, 11, 13, 2, 2, 17}</li>
<li>18 is a product of 2 * 3 * 3 which are already included.</li>
<li>19 is prime so add it {2, 3, 2, 5, 7, 3, 11, 13, 2, 2, 17, 19}</li>
</ul>
The product of these numbers is 232792560.