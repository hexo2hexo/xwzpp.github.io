---
layout: post
title:  LeetCode-Remove Nth Node From End of List
description: "Remove Nth Node From End of List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Two Pointers]
duoshuo: true
---
##题目
####Remove Nth Node From End of List
>Given a linked list, remove the nth node from the end of list and return its head.

>For example,
>
	Given linked list: 1->2->3->4->5, and n = 2.
>
	After removing the second node from the end, the linked list becomes 1->2->3->5

####Note:
>Given n will always be valid.  
>Try to do this in one pass.
<!-- more -->

##解题思路
该题是删除链表从尾部开始数第n个节点的问题，思路就是先用一个`runner`指针走n步，然后再来一个`walker`从头开始和`runner`同时向后走，当`runner`走到链表末尾的时候，`walker`指针即为倒数第n个结点。算法的时间复杂度是O(链表的长度)，空间复杂度是`O(1)`

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
	//思路就是先用一个runner指针走n步，然后再来一个walker从头开始和runner同时向后走，当runner走到链表末尾的时候，walker指针即为倒数第n个结点。算法的时间复杂度是O(链表的长度)，空间复杂度是O(1)
   public ListNode removeNthFromEnd(ListNode head, int n) {  
        if(head == null)  
            return null;  
        int i=0;  
        ListNode runner = head;  
        while(runner!=null && i<n)  
        {  
            runner = runner.next;  
            i++;  
        }  
        if(i<n)  
            return head;  
        if(runner == null)  
            return head.next;  
        ListNode walker = head;  
        while(runner.next!=null)  
        {  
            walker = walker.next;  
            runner = runner.next;  
        }  
        walker.next = walker.next.next;  
        return head;  
    }  
}
{% endhighlight %}l
