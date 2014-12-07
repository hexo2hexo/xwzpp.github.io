---
layout: post
title:  LeetCode-Add Two Numbers
description: "Add Two Numbers"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Math]
duoshuo: true
---
##题目
####Add Two Numbers

>You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

>Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)   
>Output: 7 -> 0 -> 8

<!-- more -->
##解题思路
该方法是用链表来表示两个整数间的求和，由于采用逆序排列，因此在做加法时只需要遍历两个链表即可，其中需要保存每一位相加后产生的进位。   
需要注意的是最后一位相加是否产生新的进位。整体的时间复杂度为`O(n)`。
	
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode l3=new ListNode(0);
        ListNode result=l3;
        ListNode prel3=l3;
        if(l1==null)
            return l2;
        if(l2==null)
            return l1;
        while(l1!=null&&l2!=null)
        {
            int s=l1.val+l2.val+l3.val;
            l3.val=s%10;
            l3.next=new ListNode(s/10);
            l1=l1.next;
            l2=l2.next;
            prel3=l3;
            l3=l3.next;
        }
        ListNode rest;
        if(l1==null)
            rest=l2;
        else
            rest=l1;
        while(rest!=null)
        {
            int s=rest.val+l3.val;
            l3.val=s%10;
            l3.next=new ListNode(s/10);
            rest=rest.next;
            prel3=l3;
            l3=l3.next;
        }
        if(l3.val==0)
            prel3.next=null;
        else
            l3.next=null;
        return result;       
    }
}
{% endhighlight %}

