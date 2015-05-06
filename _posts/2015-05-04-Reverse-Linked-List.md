---
layout: post
title:  LeetCode-Reverse Linked List
description: "Reverse Linked List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Reverse Linked List
>Reverse a singly linked list.

>click to show more hints.

>####Hint:
>A linked list can be reversed either iteratively or recursively. Could you implement both?
<!-- more -->
	
##解题思路
该题是对一个单链表进行转置，其实很简单，与遍历链表的操作类似，我们可以通过两个指针一前一后向后遍历，然后只需要改变指针的指向即可。

##算法代码
代码采用JAVA实现：
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode reverseList(ListNode head) {
    	if(head==null || head.next==null)
    		return head;
    	ListNode p=head.next;
    	ListNode q=head;
    	while(p!=null)
    	{
    		ListNode tmp=p.next;
    		p.next=q;
    		q=p;
    		p=tmp;
    	}
    	//这条语句非常重要，由于是转置，因此head的next应该最后为null,否则则会出现超时的情况
    	head.next=null;
    	return q;
        
    }
}
{% endhighlight %}










