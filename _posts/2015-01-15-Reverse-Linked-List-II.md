---
layout: post
title:  LeetCode-Reverse Linked List II
description: "Reverse Linked List II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Reverse Linked List II
>Reverse a linked list from position m to n. Do it in-place and in one-pass.

>For example:  
>Given `1->2->3->4->5->NULL`, m = 2 and n = 4,

>return `1->4->3->2->5->NULL`.

>####Note:
>Given m, n satisfy the following condition:   
>1 ≤ m ≤ n ≤ length of list.

<!-- more -->
	
##解题思路
该题是基本的链表操作，主要是对m节点到n节点之间的节点进行转置，首先需要找到m节点和其前节点preMnode，然后每次读到下一个节点后，将其插入到preMnode后面即可，然后继续读下一个节点，直到n节点完成。总共只需要一次扫描，所以时间是O(n)，只需要几个辅助指针，空间是O(1)。

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if(head == null)
        	return head;
        ListNode newHead = new ListNode(0);
        newHead.next=head;
        ListNode preMnode=newHead;
        int i=1;
        //找到m节点的前一个节点preMnode
        while(preMnode!=null && i<m)
        {
        	preMnode = preMnode.next;
        	i++;
        }
        if(i<m) 
        	return head;
        ListNode Mnode=preMnode.next;
        //对m节点到n节点之间的节点进行转置，每次读取一个节点就放在preMnode节点的后面
        ListNode curNode=Mnode.next;
        while(curNode!=null && i<n)
        {
        	ListNode next=curNode.next;
        	curNode.next=preMnode.next;
        	preMnode.next=curNode;
        	Mnode.next=next;
        	curNode=next;
        	i++;    	
        }
        return newHead.next;
    }
}
{% endhighlight %}





