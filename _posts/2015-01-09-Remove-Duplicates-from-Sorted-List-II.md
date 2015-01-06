---
layout: post
title:  LeetCode-Remove Duplicates from Sorted List II
description: "Remove Duplicates from Sorted List II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Remove Duplicates from Sorted List II
>Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

>For example,     
>Given `1->2->3->3->4->4->5`, return `1->2->5`.       
>Given `1->1->1->2->3`, return `2->3`.     

<!-- more -->
	
##解题思路
该题与[Remove Duplicates from Sorted List][1]非常类似，同样是去除链表中的重复元素，但是这里不保留重复的元素，还是链表操作，这里定义三个指针`k`,`i`,`j`往后推进。指针`i`，`j`之间是重复的元素(包含`i`,但不包含`j`)，`k`是`i`的前一位指针，然后通过`k.next=j`来进行跳过所有的重复元素，同时`i=j`,`j=j.next`.依次下去，直到`j=null`为止。由于只要遍历链表一遍，所以时间复杂度为`O(n)`。

这里有个注意点，为了初始化`k`指针，这里重创了一个新的头结点`newhead`,然后将这个节点的`next`指向`head`节点.

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
        ListNode newhead=new ListNode(-1);
        newhead.next=head;
        ListNode i=head;
        ListNode j=head.next;
        ListNode k=newhead;
        while(j!=null)
        {
        	while(j!=null && i.val==j.val)
        	{
        		j=j.next;
        	}
        	if(j!=null)
        	{
        	    if(i.next!=j)
            	{
            		k.next=j;
    	        	i=j;
    	        	j=j.next;
            	}else{
            		j=j.next;
            		i=i.next;
            		k=k.next;
            	}	
        	}else{
        	    k.next=j;
        	}
        	
        }
        return newhead.next;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Remove-Duplicates-from-Sorted-List.html

