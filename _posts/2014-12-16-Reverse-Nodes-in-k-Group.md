---
layout: post
title:  LeetCode-Reverse Nodes in k-Group
description: "Reverse Nodes in k-Group"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Reverse Nodes in k-Group
>Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

>If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

>You may not alter the values in the nodes, only nodes itself may be changed.

>Only constant memory is allowed.

>For example,
>Given this linked list: `1->2->3->4->5`

>For k = 2, you should return: `2->1->4->3->5`

>For k = 3, you should return: `3->2->1->4->5`

<!-- more -->

##解题思路
该题是将链表中的元素按照K个一组进行翻转。这题是[Swap Nodes in Pairs][1]的变形。首先我们需要找到K个元素，然后对这K个元素进行翻转；接着再向后找下一组K个元素并对其进行翻转，依次下去，直到找到链表结束为止。

其中对K个元素进行翻转，需要仔细考虑链表的指向问题，尤其是最终头结点的指针。

在该题中，本文假设存在一个**虚拟头结点**链接原始的链表,这样对后面的链表翻转有一定的帮助简化作用。通过设定翻转链表的起始点`Start`和结束点`End`,来对`Start+1`到`End-1`这些元素进行翻转。

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
	//每K个逆转一次
    public ListNode reverseKGroup(ListNode head, int k) {
    	if(head==null||head.next==null) return head;
    	int count=0;
    	ListNode newhead=new ListNode(0);
    	newhead.next=head;
    	ListNode p=head;
    	ListNode pre=newhead;
    	while(p!=null)
    	{
    		count++;
    		ListNode next=p.next;
    		if(count==k)
    		{
    			pre=reverseList(pre,next);
    			count=0;
    		}
    		p=next;
    			
    	}
    	return newhead.next;

    }

    //逆转pre和end之间的链表元素
    public ListNode reverseList(ListNode pre,ListNode end)
    {
    	if(pre==null||pre.next==null) return pre;
    	ListNode head=pre.next;
    	ListNode cur=pre.next.next;
    	while(cur!=end){
    		ListNode curnext=cur.next;
    		cur.next=pre.next;
    		pre.next=cur;
    		cur=curnext;
    	}
    	head.next=end;
    	return head;  //返回的是逆转后的最后一个结点
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Swap-Nodes-in-Pairs.html