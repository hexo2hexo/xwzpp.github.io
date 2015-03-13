---
layout: post
title:  LeetCode-Populating Next Right Pointers in Each Node
description: "Populating Next Right Pointers in Each Node"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Populating Next Right Pointers in Each Node
>Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }

>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

>Initially, all next pointers are set to `NULL`.

>####Note:

	1. You may only use constant extra space.     
	2. You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

>For example,      
>Given the following perfect binary tree,
>
         1
       /  \
      2    3
     / \  / \
    4  5  6  7

>After calling your function, the tree should look like:
>
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL

<!-- more -->
	
##解题思路
该题是对树中的每一层建立链表。这与层次遍历非常相似。但是，这里需要常量的空间，因此不可以使用队列进行存储。由于是链表，因此我们可以通过上一层的链表操作从而进行层次遍历，当当前行遍历结束后，下一行的链表关系其实已经建立好了。因此可以通过获取下一行的头结点，从而遍历到下一层。这样依次遍历，就可以得到最终的结果。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root==null)
        	return;
        TreeLinkNode lastnode=root;//每一行的头结点
        TreeLinkNode curhead=null;//定义当前行的头结点
        TreeLinkNode prenode=null;//定义当前行向后遍历的节点
        while(lastnode!=null)
        {
        	TreeLinkNode nextnode=lastnode; //定义当前行的遍历节点
        	while(nextnode!=null)
        	{
        		if(nextnode.left!=null)  //说明有左孩子节点
	        	{
	        		//判断当前有没有头结点，即该节点是不是下一行第一个节点
	        		if(curhead==null) //没有头结点
	        		{
	        			curhead=nextnode.left;
	        			prenode=curhead;
	        		}else{ //有头结点,prenode向后前进
	        			prenode.next=nextnode.left;
	        			prenode=prenode.next;
	        		}
	        	}

	        	if(nextnode.right!=null) //说明有右孩子节点
	        	{
	        		//同样需要判断当前有没有头结点
	        		if(curhead==null) //没有头结点
	        		{
	        			curhead=nextnode.right;
	        			prenode=curhead;
	        		}else{ //有头结点,prenode向后前进
	        			prenode.next=nextnode.right;
	        			prenode=prenode.next;
	        		}
	        	}
	        	nextnode=nextnode.next;
	        }
	        //当前行结束,进入下一行
	        lastnode=curhead;
	        curhead=null;   //需要置为null，因为是新的一层需要建立 	
        }
    }
}
{% endhighlight %}








