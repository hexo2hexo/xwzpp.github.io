---
layout: post
title:  LeetCode-Copy List with Random Pointer 
description: "Copy List with Random Pointer"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Linked List]
duoshuo: true
---
##题目
####Copy List with Random Pointer
>A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

>Return a deep copy of the list.

<!-- more -->
	
##解题思路 
该题首先想到的是可以通过两次遍历得到结果，第一次是复制`next`节点，第二次是链接`random`节点,为了通过旧节点能过迅速的找到对应的新节点，我们这里采用`hashmap`进行存储，其中键为旧节点，值为新节点，但是这里需要额外的存储空间。

这里可以不是用额外空间进行求解，但是这里需要三次扫描链表。第一次遍历链表，得到新节点，并将新节点插入到旧节点之后，即原来的链表变成新旧节点交替出现的情况。第二次是链接新节点的random,即old.next.random=old.random.next.第三次是将该链表进行分割，分别得到两个链表，就是对相互间隔的节点进行切割。

##算法代码
代码采用JAVA实现： 
一般方法：
{% highlight java %}
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head==null)
        	return null;
        RandomListNode headbefore=new RandomListNode(0);
        headbefore.next=head;
        RandomListNode newheadbefore=new RandomListNode(0);
        HashMap<RandomListNode,RandomListNode> map=new HashMap<RandomListNode,RandomListNode>();
        RandomListNode cur=head;
        RandomListNode last=newheadbefore;
        while(cur!=null)
        {
        	RandomListNode newnode=new RandomListNode(cur.label);
        	map.put(cur,newnode);
        	last.next=newnode;
        	last=last.next;
        	cur=cur.next;
        }
        cur=head;
        while(cur!=null)
        {
        	RandomListNode newnode=map.get(cur);
        	newnode.random=map.get(cur.random);
        	cur=cur.next;
        }

        return newheadbefore.next;
    }
}
{% endhighlight %}

不适用额外空间：
{% highlight java %}
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head==null)
        	return null;
       	RandomListNode p=head;
       	//第一次遍历
       	while(p!=null)
       	{
       		RandomListNode newnode=new RandomListNode(p.label);
       		RandomListNode temp=p.next;
       		newnode.next=p.next;
       		p.next=newnode;
       		p=temp;
       	}

       	//第二次遍历
       	p=head;
       	while(p!=null)
       	{
       		if(p.random!=null)
       			p.next.random=p.random.next;
       		p=p.next.next;

       	}

       	//第三次遍历
       	p=head;
       	RandomListNode newhead=p.next;
       	while(p!=null)
       	{
       		RandomListNode temp=p.next;
       		if(p.next!=null)
       		{
       			p.next=p.next.next;
       		}else{
       			p.next=null;
       		}
       		p=temp;
       	}

       	return newhead;
    }
}
{% endhighlight %}



