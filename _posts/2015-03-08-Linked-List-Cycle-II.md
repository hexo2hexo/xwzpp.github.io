---
layout: post
title:  LeetCode-Linked List Cycle II
description: "Linked List Cycle II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Linked List,Two Pointer]
duoshuo: true
---
##题目
####Linked List Cycle II
>Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

>Follow up:   
>Can you solve it without using extra space?
<!-- more -->
	
##解题思路
该题与[Linked List Cycle][1]解法相同，同样定义两个指针，因为这两个指针即可以用来判断是否是一个环`（A==B）`，也可以得到最终他们的相遇点。

假设两个指针walker和runner，walker一倍速移动，runner两倍速移动。有一个链表，假设他在cycle开始前有a个结点，cycle长度是c，而我们相遇的点在cycle开始后b个结点。那么想要两个指针相遇，意味着要满足以下条件：(1) a+b+mc=s; (2) a+b+nc=2s; 其中s是指针走过的步数，m和n是两个常数。这里面还有一个隐含的条件，就是s必须大于等于a，否则还没走到cycle里面，两个指针不可能相遇。假设k是最小的整数使得a<=kc，也就是说(3) a<=kc<=a+c。接下来我们取m=0, n=k，用(2)-(1)可以得到s=kc以及a+b=kc。由此我们可以知道，只要取b=kc-a(由(3)可以知道b不会超过c)，那么(1)和(2)便可以同时满足，使得两个指针相遇在离cycle起始点b的结点上。
因为s=kc<=a+c=n，其中n是链表的长度，所以走过的步数小于等于n，时间复杂度是O(n)。

从head开始到环的起点和从想遇点到环的起点距离是一样的。

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
    public ListNode detectCycle(ListNode head) {
        if(head==null)
        	return null;
        ListNode A=head;
        ListNode B=head;
        while(B!=null && B.next!=null)
        {
        	A=A.next;
        	B=B.next.next;
        	if(A==B)
        	{
        		//此时从head开始到环的起点和从想遇点到环的起点距离是一样的。
        		ListNode C=head;
        		while(C!=A)
        		{
        			C=C.next;
        			A=A.next;
        		}
        		return C;
        	}
        }
        return null;
    }
}
{% endhighlight %}





