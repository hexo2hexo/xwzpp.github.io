---
layout: post
title:  LeetCode-Intersection of Two Linked Lists
description: "Intersection of Two Linked Lists"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Intersection of Two Linked Lists
>Write a program to find the node at which the intersection of two singly linked lists begins.


>For example, the following two linked lists:
>
	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗            
	B:     b1 → b2 → b3

>begin to intersect at node c1.


>####Notes:
>
+ If the two linked lists have no intersection at all, return null.
+ The linked lists must retain their original structure after the function returns.
+ You may assume there are no cycles anywhere in the entire linked structure.
+ Your code should preferably run in O(n) time and use only O(1) memory.

>####Credits:
>Special thanks to @stellari for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这道题是找到两个链表的共同的第一个节点。方法比较简单，首先对两个链表分别遍历一次，分别得到两个链表的长度为`m`,`n`,且`m<n`.然后定义两个指针`p`,`q`.`p`指向长度为`m`的链表，`q`指向长度为`n`的链表，然后首先让`q`先向前遍历`n-m`个位置，然后`p`和`q`同时一起前进，当`q==p`时，此时的节点即为两个链表第一个公共节点。

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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null)
        	return null;
        //获取两个链表的长度
        ListNode p=headA;
        int headAlen=0;
        int headBlen=0;
        while(p!=null)
        {
        	headAlen++;
        	p=p.next;
        }
        p=headB;
        while(p!=null)
        {
        	headBlen++;
        	p=p.next;
        }
        ListNode longP;
        ListNode shortP;
        if(headAlen<headBlen)
        {
        	longP=headB;
        	shortP=headA;
        }else
        {
        	longP=headA;
        	shortP=headB;
        }

        //longP向前历|headAlen-headBlen|
        int m=Math.abs(headAlen-headBlen);
        while(m!=0)
        {
        	longP=longP.next;
        	m--;
        }
        while(longP!=shortP)
        {
        	longP=longP.next;
        	shortP=shortP.next;
        }
        return longP;
    }
}
{% endhighlight %}





