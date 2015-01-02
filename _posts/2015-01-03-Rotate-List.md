---
layout: post
title:  LeetCode-Rotate List
description: "Rotate List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Two Pointers]
duoshuo: true
---
##题目
####Rotate List
>Given a list, rotate the list to the right by k places, where k is non-negative.

>For example:    
>Given `1->2->3->4->5->NULL` and `k = 2`,    
>return `4->5->1->2->3->NULL`.

<!-- more -->
	
##解题思路
这是一道链表操作的题目，基本思路是设置两个指针`i`,`j`,中间相差`n`,用walker-runner定位到要旋转的那个结点，然后将下一个结点设为新表头，并且把当前结点设为表尾。设置前后两个指针，然后推进前进的方法称为**尺取法**。

但是这里需要注意的是`n`超过链表长度，此时步数应该重新跑到结尾点计算，即`j`指针从新回到头结点处。

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
    public ListNode rotateRight(ListNode head, int n) {
        if(head==null || head.next==null)
        	return head;
        ListNode i=null;  //定义两个指针
        ListNode j=head;
        for(int k=0;k<n;k++)
        {
        	j=j.next;
        	if(j==null)   //n的长度超过链表，j重新回到头结点
        		j=head;
        }
        i=head;
        while(j.next!=null)
        {
        	j=j.next;
        	i=i.next;
        }
        j.next=head;  //进行旋转
        head=i.next;
        i.next=null;
        return head;
    }
}
{% endhighlight %}

