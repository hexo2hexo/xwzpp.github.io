---
layout: post
title:  LeetCode-Linked List Cycle
description: "Linked List Cycle"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Two Pointer]
duoshuo: true
---
##题目
####Linked List Cycle
>Given a linked list, determine if it has a cycle in it.

>Follow up:  
>Can you solve it without using extra space?
<!-- more -->
	
##解题思路
该题是判断一个链表是否存在一个环，这里我们可以将其联想到现实生活中，我们找两个指针`A,B`，`A`每次以1步为单位前进，而`B`每次以2步为单位前行，最终我们会发现，如果链表中有环，肯定是在末尾，而且`A`最终肯定能与`B`相遇。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null || head.next==null)
        	return false;
        ListNode A=head;//定义A指针，每次以1步为单位前进
        ListNode B=head;//定义B指针，每次以2步为单位前进
        while(B!=null && B.next!=null)
        {
        	A=A.next;
        	B=B.next.next;
        	if(A==B)
        		return true;
        }
        return false;
    }
}
{% endhighlight %}





