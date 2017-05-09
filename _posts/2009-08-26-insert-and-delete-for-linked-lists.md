---
layout: post
category: blog
title: insert and delete for linked lists
description: basic data structures
date: '2009-08-26T23:04:00.008-05:00'
author: scott
tag:
- c
- data-structures
image: https://unsplash.it/560/120?random
headerImage: true
comments: false
modified_time: '2012-12-17T06:42:28.051-06:00'
thumbnail: http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo9wTVdFiI/AAAAAAAABiw/gNd8bp3-Hqo/s72-c/singly-linked+original.png
blogger_id: tag:blogger.com,1999:blog-8714319922389040689.post-678208148173055298
blogger_orig_url: http://scosant.blogspot.com/2009/08/insert-and-delete-for-linked-lists.html
---

Here, I am going to solve and discuss a relatively simple problem involving linked lists.  If there is something wrong or missing, <b>please comment</b>! All code compiles and runs without error or warnings.  There are a small number of test cases for each.<br />
<br />
<span style="font-size: x-large;">Problem</span><br />
<br />
Implement <code>insert</code> and <code>delete</code> for (1) singly-linked linked list, (2) sorted linked list, (3), circular linked list. (<a href="http://maxnoy.com/interviews.html">Source</a>)<br />
<pre class="c" name="code">int Insert(node** head, int data);
int Delete(node** head, int deleteMe);
</pre><br />
<span style="font-size: x-large;">Solution</span><br />
<br />
From the method signatures, it is evident that C will be used.  We see that <code>insert</code> and <code>delete</code> will accept a "pointer to the head pointer" and an int.  We can pass <code>head</code> by reference which will allow it to be modified.  Also, notice that <code>data</code> is passed-by-value.  There is no definition for <code>node</code>, but it is reasonable to assume that it has this structure:<br />
<br />
<pre class="c" name="code">typedef struct node {
   struct node* previous // for doubly-linked nodes
   struct node* next;
   int data;
} node;</pre><br />
<br />
Also, we can assume that <code>int data</code> in <code>Insert</code> refers to the data value to be inserted and <code>int deleteMe</code> in <code>Delete</code> refers to the value to be deleted.  However, there are still a few questions.  <code>Insert</code> does not specify where the value will be inserted.  The most likely behavior is that the data will be appended to the list, and we will assume this here.  Now, what should this function return?  Two possible options are to return the inserted value or to return a status code.  Since the inserted value is already known, and it is possible for the <code>insert</code> to fail (i.e. memory cannot be allocated for the new node), the function will return a status code; "1" if successful and "0" otherwise.<br />
<br />
There are some things to consider for <code>delete</code> as well.  For example, what happens if the value to be deleted does not exist?  Here, we define this as a failed operation, and thus, the function will return a "failed" status code.  If it succeeds , it will return a "success".  Now, what happens if there are duplicate values (note that <code>insert</code> allows duplicates)?  Here, we choose to delete only the first encountered occurrence (which is likely to be the most recently added value).  This would provide the most consistent behavior with <code>insert</code>.<br />
<br />
<span style="font-size: large;">Singly-Linked: Insert and Delete</span><br />
<br />
<a href="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo9wTVdFiI/AAAAAAAABiw/gNd8bp3-Hqo/s1600-h/singly-linked+original.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375677005253383714" src="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo9wTVdFiI/AAAAAAAABiw/gNd8bp3-Hqo/s400/singly-linked+original.png" style="cursor: pointer; display: block; height: 39px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
For a singly-linked linked list, <code>insert</code> is simple.  A node <code>newnode</code> is created with the data to be inserted.  The <code>*head</code> pointer is set to this new node, and <code>next</code> of the new head is set to the previous head node.&nbsp; This will have a running time of <i>O(1)</i>.<br />
<br />
<a href="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo9txK5L_I/AAAAAAAABio/TahBpjk0I1U/s1600-h/singly-linked+insert+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375676961722544114" src="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo9txK5L_I/AAAAAAAABio/TahBpjk0I1U/s400/singly-linked+insert+4.png" style="cursor: pointer; display: block; height: 39px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
Delete is only slightly more complex since it involves two special cases.  If the head node contains the value to be deleted, the <code>*head</code> pointer must be updated to point to the following node.<br />
<br />
<a href="http://4.bp.blogspot.com/_4yzBNmd0Mow/Spo9rHWT-kI/AAAAAAAABig/d6xbQFRiKXE/s1600-h/singly-linked+delete+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375676916136409666" src="http://4.bp.blogspot.com/_4yzBNmd0Mow/Spo9rHWT-kI/AAAAAAAABig/d6xbQFRiKXE/s400/singly-linked+delete+4.png" style="cursor: pointer; display: block; height: 52px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
Otherwise, the <code>next</code> pointer of the previous node is set to the <code>next</code> of the node to be deleted.  This also works if the last node contains the data to be removed.  The previous node will simply point to <code>NULL</code>.&nbsp; Deletions will have a running time of <i>O(n)</i>.<br />
<br />
<a href="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo9oKlOzXI/AAAAAAAABiY/zrd6Omf6f4E/s1600-h/singly-linked+delete+2.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375676865464683890" src="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo9oKlOzXI/AAAAAAAABiY/zrd6Omf6f4E/s400/singly-linked+delete+2.png" style="cursor: pointer; display: block; height: 70px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
<script src="https://gist.github.com/4317988.js"></script><br />
<br />
<br />
<span style="font-size: 130%;">Doubly-Linked:  Insert and Delete</span><br />
<br />
<a href="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-TGZ5CII/AAAAAAAABjQ/Qme7YPA7Dbs/s1600-h/doubly-linked+original.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375677603077752962" src="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-TGZ5CII/AAAAAAAABjQ/Qme7YPA7Dbs/s400/doubly-linked+original.png" style="cursor: pointer; display: block; height: 49px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
For a doubly-linked linked list, <code>insert</code> is also very easy.  A new node is created with the data to be inserted, <code>next</code> is pointed to the old head and <code>previous</code> is pointed to <code>NULL</code>.  If the list already contained at least one other element, the <code>previous</code> pointer of the old head must now point to the new head. Then, the <code>*head</code> pointer is updated.&nbsp; Insertions for a doubly-linked linked list will have a running time of <i>O(1)</i>.<br />
<br />
<a href="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-QCEFJaI/AAAAAAAABjI/s5Y_0znierY/s1600-h/doubly-linked+insert+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375677550372922786" src="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-QCEFJaI/AAAAAAAABjI/s5Y_0znierY/s400/doubly-linked+insert+4.png" style="cursor: pointer; display: block; height: 46px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
Deleting, on the other hand, has a few special cases.  If the first node is to be deleted, the <code>*head</code> simply needs to point to the next node.  If the last node is to be deleted, then the <code>next</code> pointer of the previous node must point to <code>null</code>.<br />
<br />
<a href="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo-NSBp3UI/AAAAAAAABjA/qPV-agPuELo/s1600-h/doubly-linked+delete+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375677503118105922" src="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo-NSBp3UI/AAAAAAAABjA/qPV-agPuELo/s400/doubly-linked+delete+4.png" style="cursor: pointer; display: block; height: 59px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
For nodes deleted from within the list, the <code>next</code> and <code>previous</code> pointers must be updated for the previous and next node, respectively.&nbsp; Just as with a singly-linked linked list, deletions in a doubly-linked linked list will also run in linear time, <i>O(n)</i>.<br />
<br />
<a href="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo-K7Kl6UI/AAAAAAAABi4/3xZOQSMO-Lw/s1600-h/doubly-linked+delete+2.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375677462621841730" src="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo-K7Kl6UI/AAAAAAAABi4/3xZOQSMO-Lw/s400/doubly-linked+delete+2.png" style="cursor: pointer; display: block; height: 83px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
<script src="https://gist.github.com/4317992.js"></script><br />
<br />
<br />
<span style="font-size: 130%;">Circular:  Insert and Delete</span><br />
<br />
For inserting new nodes into a circular linked list, there are a few options.  We could use a singly-linked linked list and simply point the last node to the head node.  This would make inserts have a running time of <span style="font-style: italic;">O(n)</span>.  If we used a doubly-linked linked list, we could use the node pointed to by the head node's <code>previous</code> pointer and make insertions in constant time, <span style="font-style: italic;">O(1)</span>.  Deletions will be similar to deletions in a doubly-linked linked list and run in <span style="font-style: italic;">O(n)</span>.  Since insertions are faster using doubly-linked nodes, we choose this for the implementation.<br />
<br />
<a href="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo_ZPH0qdI/AAAAAAAABj8/9cwJ7MzkITg/s1600-h/circular+original.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375678808008731090" src="http://1.bp.blogspot.com/_4yzBNmd0Mow/Spo_ZPH0qdI/AAAAAAAABj8/9cwJ7MzkITg/s400/circular+original.png" style="cursor: pointer; display: block; height: 65px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
For <code>insert</code>, there are two cases.  If the list is empty, the <code>head</code> node is created and its <code>next</code> and <code>previous</code> members are pointed to itself.  Otherwise, the <code>previous</code> node of the head node is saved, <code>next</code> of the new node points to the old <code>head</code> and the <code>next</code> and <code>previous</code> members are updated accordingly.<br />
<br />
<a href="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-0lyPM9I/AAAAAAAABjo/F9jikBKcuqY/s1600-h/circular+insert+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375678178437051346" src="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-0lyPM9I/AAAAAAAABjo/F9jikBKcuqY/s400/circular+insert+4.png" style="cursor: pointer; display: block; height: 67px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
For <code>delete</code>, the list is first checked if it is empty.  If it is not, It first checks if the <code>*head</code> node contains the value to be deleted.  If not, it then goes through a loop searching for the value until it traverses the list and returns back to the <code>*head</code> node.  The first node requires a special check because the iterator starts at the node after the <code>head</code> node.  This is so the <code>while</code> loop does not exit immediately.<br />
<br />
<a href="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo-yQjJHbI/AAAAAAAABjg/pgQLq0o5gmY/s1600-h/circular+delete+4.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375678138376854962" src="http://3.bp.blogspot.com/_4yzBNmd0Mow/Spo-yQjJHbI/AAAAAAAABjg/pgQLq0o5gmY/s400/circular+delete+4.png" style="cursor: pointer; display: block; height: 62px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><br />
<br />
As you can see, deleting a node in the middle is similar to deleting the <code>*head</code> node.<br />
<br />
<a href="http://2.bp.blogspot.com/_4yzBNmd0Mow/SppANvO7zII/AAAAAAAABkI/d99J7T0mZaE/s1600-h/circular+delete+2.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img alt="" border="0" id="BLOGGER_PHOTO_ID_5375679709981691010" src="http://2.bp.blogspot.com/_4yzBNmd0Mow/SppANvO7zII/AAAAAAAABkI/d99J7T0mZaE/s400/circular+delete+2.png" style="cursor: pointer; display: block; height: 109px; margin: 0px auto 10px; text-align: center; width: 400px;" /></a><a href="http://2.bp.blogspot.com/_4yzBNmd0Mow/Spo-vxT-3II/AAAAAAAABjY/PYAFMsMazUU/s1600-h/circular+delete+2.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"></a><br />
<br />
<script src="https://gist.github.com/4317996.js"></script>