---
layout: post
title:  LeetCode-Partition List
description: "Partition List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Two Pointers]
duoshuo: true
---
##题目
####Partition List 
>Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

>You should preserve the original relative order of the nodes in each of the two partitions.

>For example,    
>Given `1->4->3->2->5->2` and `x = 3`,    
>return `1->2->2->4->3->5`.

<!-- more -->
	
##解题思路
本题主要是链表操作，这里为了实现指针的变化，维护两个指针`i`,`j`使得`i.next==j`，让这两个指针一起推进，并用指针`k`始终指向比`x`小的元素序中的最后一个元素位置。如果`j`指的元素比`x`小，则该元素应该放到`k`后面。这里只要进行指针指向的变换操作。如果`j`指的元素比`x`大，则将`i`,`j`往前推进。依次处理直到`j==null`。

这里有个细节需要判定，当`j`指的元素比`x`小时，如果`k==i`，说明`j`就是下一个比`x`小的元素，则不用变换指针操作，直接`i=i.next`,`j=j.next`,`k=k.next`即可。 

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
    public ListNode partition(ListNode head, int x) {
        if(head==null || head.next==null)
        	return head;
        ListNode newhead=new ListNode(0);
        newhead.next=head;
        ListNode k=newhead;
        ListNode i=newhead;
        ListNode j=head;
        while(j!=null)
        {
        	if(j.val>=x)
        	{
        		j=j.next;
        		i=i.next;
        	}else{  
        		if(k==i){  //说明j就是下一个比X小的元素
	        		i=i.next;
	        		j=j.next;
	        		k=k.next;
	        	}else{    //将j移到k的后面
	        		ListNode tmp=j;
	        		i.next=j.next;
	        		j=j.next;
	        		tmp.next=k.next;
	        		k.next=tmp;
	        		k=k.next;
        		}
       		}
        }
        return newhead.next;
    }
}
{% endhighlight %}



