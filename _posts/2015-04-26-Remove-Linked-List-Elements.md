---
layout: post
title:  LeetCode-Remove Linked List Elements
description: "Remove Linked List Elements"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Remove Linked List Elements
>Remove all elements from a linked list of integers that have value val.

>**Example**   
>**Given**: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6      
>**Return**: 1 --> 2 --> 3 --> 4 --> 5

>**Credits**:       
>Special thanks to @mithmatt for adding this problem and creating all test cases.
<!-- more -->
	
##解题思路
该题是对链表中的节点进行删除，因此可以维护两个指针，删除的时候只需要指针的变动即可，此外，由于头结点的删除是一种特殊情况，因此我们可以通过重新设定一个新的头结点，将其next指向head,这样头结点与其他节点的删除操作就可以统一化处理。


##算法代码
代码采用JAVA实现：
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head==null)
        	return null;
        ListNode newhead=new ListNode();
        newhead.next=head;
        ListNode p=head;
        ListNode q=newhead;
        while(p!=null)
        {
        	if(p.val==val)
        	{
        		q.next=p.next;
        		p=p.next;
        	}else{
        		q=p;
        		p=p.next;
        	}
        }
        return newhead.next;

    }
}
{% endhighlight %}










