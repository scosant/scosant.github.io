---
layout: post
category: blog
title: reverse words in a string
description: most popular programming interview question
date: '2009-08-31T06:02:00.011-05:00'
author: scott
tag:
- c
image: https://unsplash.it/560/120?random
headerImage: true
comments: false
modified_time: '2012-12-17T06:33:54.146-06:00'
thumbnail: http://1.bp.blogspot.com/_4yzBNmd0Mow/SpuswSkGqxI/AAAAAAAABkQ/8GTlzLy_PkU/s72-c/reverse+words+in+a+string+state+machine.png
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-2495358262353513147
blogger_orig_url: http://scosant.blogspot.com/2009/08/reverse-words-in-string.html
---

# Problem

Reverse words in a string (words are separated by one or more spaces). Now do it in-place. By far the most popular string [question](http://maxnoy.com/interviews.html)!

# Solution

This is an in-place solution in C.  It works by first reversing the entire string, and then reverses each word.  To detect the beginning and end of each word, it uses the following state machine:

<p align="center" markdown="1">
    ![reverse words in a string state machine](/assets/images/posts/reverse-words-in-a-string-state-machine.png)
</p>

Once it detects its first character, it marks this as the beginning of the word. It then traverses the string until it reaches a "." (period) or " " (space) and marks the previous character as the end of the word. It then reverses this word. If a "\0" (null terminator) is reached and is still within a word, it reverses this final word and exits. Otherwise, it simply exits.

<script src="https://gist.github.com/4317969.js"></script>