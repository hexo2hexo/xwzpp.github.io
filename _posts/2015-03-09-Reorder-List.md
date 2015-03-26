---
layout: post
title:  LeetCode-Reorder List
description: "Reorder List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List]
duoshuo: true
---
##题目
####Reorder List
>Given a singly linked list L: L0→L1→…→Ln-1→Ln,    
>reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

>You must do this in-place without altering the nodes' values.

>For example,    
>Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.
<!-- more -->
	
##解题思路
该题是对链表进行重排序，即`L1`链接`Ln`,`L2`链接`Ln-1`.但是我们可以定义两个指针`p`和`q`，`p`从前往后，`q`从后往前，那我们怎么知道`q`的前向节点呢，因此我们首先遍历一遍链表，使用`hashmap`来存储每个节点的前向节点。这样再改变链表链接的时候，就可以很方便的从后往前进行遍历。否则每次向后一个节点，都需要遍历剩余的全部节点，从而才能找到尾节点。

这里有一个需要注意的地方，就是结束条件：如果节点总数为偶数个，则结束条件为`p.next==q`.如果节点个数为奇数，则结束条件为`p==q`.

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
    public void reorderList(ListNode head) {
        if(head==null || head.next==null || head.next.next==null)
        	return;
        ListNode p=head.next;
        ListNode q=head;
        HashMap<ListNode,ListNode> map=new HashMap<ListNode,ListNode>();//存放每个节点的前一个节点
       	while(p!=null)
       	{
       		map.put(p,q);
       		p=p.next;
       		q=q.next;
       	}
       	//这里q已经到了结尾处
       	//开始遍历调序
       	p=head;
       	while(p!=q && p.next!=q)
       	{
       		ListNode tmp=p.next;
       		p.next=q;
       		q.next=tmp;
       		p=tmp;
       		q=map.get(q);
       	}
       	q.next=null;
       	return;

    }
}
{% endhighlight %}





