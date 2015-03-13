---
layout: post
title:  LeetCode-Populating Next Right Pointers in Each Node II
description: "Populating Next Right Pointers in Each Node II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Populating Next Right Pointers in Each Node II
>Follow up for problem "Populating Next Right Pointers in Each Node".

>What if the given tree could be any binary tree? Would your previous solution still work?

>####Note:

>* You may only use constant extra space.

>For example,
>Given the following binary tree,
>
         1
       /  \
      2    3
     / \    \
    4   5    7

>After calling your function, the tree should look like:
>
        1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL

<!-- more -->
	
##解题思路
该题是[Populating Next Right Pointers in Each Node][1]的延伸。该树可能不是一个完美二叉树，而是一个任意的二叉树。但是，上题中的方法并没有对树是否是完美二叉树有要求。所以，上题的求解方法在此处依旧适用。

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

[1]: http://pisxw.com/algorithm/Populating-Next-Right-Pointers-in-Each-Node.html







