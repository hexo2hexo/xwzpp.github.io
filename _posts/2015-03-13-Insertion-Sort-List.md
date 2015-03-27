---
layout: post
title:  LeetCode-Insertion Sort List 
description: "Insertion Sort List "
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Sort]
duoshuo: true
---
##题目
####Insertion Sort List 
>Sort a linked list using insertion sort.
>
<!-- more -->
	
##解题思路
该题是采用插入排序对链表进行排序，主要是需要了解插入排序的原理，以及链表的插入操作。这里通过重新设定一个空的头结点`newhead`来统一节点在头结点处插入和中间插入的步骤。可以简化程序的设计。

需要注意的是，其中链表之间的链接操作和跳转需要比较小心的处理。

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
    public ListNode insertionSortList(ListNode head) {
        if(head==null || head.next==null)
        	return head;
        ListNode newhead=new ListNode(0);
        newhead.next=head;
        ListNode prep=newhead; //p的前向节点
        ListNode p=head; //定义遍历节点
        while(p!=null)
        {
        	ListNode pnext=p.next;
        	ListNode a=newhead;
        	ListNode b=a.next;
        	while(b!=p)
        	{
        		if(b.val<=p.val)
        		{
        			a=a.next;
        			b=b.next;
        		}else{
        			a.next=p;
        			p.next=b;
        			prep.next=pnext;
        			p=pnext;
        			break;
        		}

        	}
        	if(b==p)
        	{
        		prep=p;
        		p=pnext;
        	}
        }
        return newhead.next;
    }
}
{% endhighlight %}





