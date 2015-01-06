---
layout: post
title:  LeetCode-Remove Duplicates from Sorted List
description: "Remove Duplicates from Sorted List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Remove Duplicates from Sorted List
>Given a sorted linked list, delete all duplicates such that each element appear only once.

>For example,   
>Given `1->1->2`, return `1->2`.   
>Given `1->1->2->3->3`, return `1->2->3`.      

<!-- more -->
	
##解题思路
该题是去除链表中的重复元素，且重复元素只保存一个，主要是链表操作，这里定义两个指针`i`,`j`往后推进。指针`i`，`j`之间是重复的元素(包含`i`,但不包含`j`)，然后通过`i.next=j`来进行跳过多余的重复元素，同时`i=j`,`j=j.next`.依次下去，直到`j==null`为止。由于只要遍历链表一遍，所以时间复杂度为`O(n)`。

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
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null)
        	return head;
        ListNode i=head;
        ListNode j=head.next;
        while(j!=null)
        {
        	while(j!=null && i.val==j.val)
        	{
        		j=j.next;
        	}
        	if(j!=null)
        	{
        		i.next=j;
        		i=j;
        		j=j.next;
        	}else{
        		i.next=j;
        	}
        }
        return head;
    }
}
{% endhighlight %}


