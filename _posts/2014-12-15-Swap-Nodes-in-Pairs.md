---
layout: post
title:  LeetCode-Swap Nodes in Pairs
description: "Swap Nodes in Pairs"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Swap Nodes in Pairs
>Given a linked list, swap every two adjacent nodes and return its head.

>For example,
>Given `1->2->3->4`, you should return the list as `2->1->4->3`.

>Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.

<!-- more -->

##解题思路
该题是对链表中的两个相邻的节点进行交换。这里可以使用**递归**的思想来求解该问题。因为对整个链表进行交换，也包含对子链表的交换。由于题目中不允许开辟新的空间，只能通过对节点间的链接关系进行调整，因此需要仔细考虑链接的问题。

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
	//采用递归求解
    public ListNode swapPairs(ListNode head) {
        if(head==null) return null;
        if(head.next==null) return head;
        ListNode newhead=head.next; //新的头结点
        ListNode node=head.next.next; //下次递归的头结点
        newhead.next=head;
        head.next=swapPairs(node); //递归调用
        return newhead;
    }
}
{% endhighlight %}
