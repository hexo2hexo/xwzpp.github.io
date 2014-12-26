---
layout: post
title:  LeetCode-Merge Two Sorted Lists 
description: "Merge Two Sorted Lists"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Merge Two Sorted Lists
>Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

<!-- more -->
	
##解题思路
该题是将两个有序链表进行合并，方法很简单，只要对每个链表维持一个指针，然后比较大小，进行链表的链接操作就行了，该题是[Merge k Sorted Lists][1]这题的子过程。

##算法代码
代码采用JAVA实现：
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1==null)
        	return l2;
        if(l2==null)
        	return l1;
        ListNode l3=new ListNode(0);
        ListNode p=l1;
        ListNode q=l2;
        ListNode k=l3;
        while(p!=null && q!=null)
        {
        	if(p.val<=q.val)
        	{
        		k.next=p;
        		p=p.next;
        		k=k.next;
        	}else{
        		k.next=q;
        		q=q.next;
        		k=k.next;
        	}
        }
        if(p!=null)
        	k.next=p;
        if(q!=null)
        	k.next=q;
        return l3.next;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Merge-k-Sorted-Lists.html