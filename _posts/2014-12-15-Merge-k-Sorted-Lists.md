---
layout: post
title:  LeetCode-Merge k Sorted Lists
description: "Merge k Sorted Lists"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Linked List,Heap]
duoshuo: true
---
##题目
####Merge k Sorted Lists
>Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

<!-- more -->

##解题思路
该题是对多个已经排好序的链表进行合并，从而生成最后一个有序的链表。我们知道，对两个链表进行合并是非常简单的，时间复杂度为`O(m+n)`,`m`和`n`分别为两个链表的长度。但是，这里却是对多个链表进行合并，因此我们可以采用**分治算法**进行求解。

	分治算法主要分为以下三步：
	* 分解（这里可以采用二分）
	* 求解（这里无需求解，因为每个链表已经有序）
	* 合并（这里为对两个有序链表进行合并）

时间复杂度分析：假设总共有k个list，每个list的最大长度是n，那么运行时间满足递推式T(k) = 2T(k/2)+O(n*k)。根据主定理，可以算出算法的总复杂度是O(nklogk)。

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
    //采用分治法求解
    public ListNode mergeKLists(List<ListNode> lists) {
        int k=lists.size();
        if(k==0) return null;
       	return mergeLists(lists,0,k-1);
    }

    public ListNode mergeLists(List<ListNode> lists,int start,int end)
    {
    	if(start==end)
    		return lists.get(start);
    	else{
    		int middle=(end+start)/2; //分解操作
	    	ListNode left=mergeLists(lists,start,middle);
	        ListNode right=mergeLists(lists,middle+1,end);
	        return merge(left,right); //合并操作
    	}
    	
    }

    public ListNode merge(ListNode head1,ListNode head2)
    {
    	if(head1==null)
    		return head2;
    	if(head2==null)
    		return head1;
    	ListNode head3=new ListNode(0);
    	int i=0;
    	ListNode p=head1;
    	ListNode q=head2;
    	ListNode r=head3;
    	if(p.val<=q.val){
    		head3.val=p.val;
    		p=p.next;		
    	}else{
    		head3.val=q.val;
    		q=q.next;	
    	}
    	while(p!=null&&q!=null){
    		if(p.val<=q.val){
	    		ListNode m=new ListNode(p.val);
	    		r.next=m;
	    		r=m;
	    		p=p.next;		
	    	}else{
	    		ListNode m=new ListNode(q.val);
	    		r.next=m;
	    		r=m;
	    		q=q.next;	
	    	}
    	}
    	if(p!=null)
    		r.next=p;
    	else
    		r.next=q;
    	return head3;
    }
}
{% endhighlight %}
