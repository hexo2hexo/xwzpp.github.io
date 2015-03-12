---
layout: post
title:  LeetCode-Flatten Binary Tree to Linked List
description: "Flatten Binary Tree to Linked List"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search]
duoshuo: true
---
##题目
####Flatten Binary Tree to Linked List
>Given a binary tree, flatten it to a linked list in-place.

>For example,
>Given
>
         1
        / \
       2   5
      / \   \
     3   4   6

>The flattened tree should look like:
>
	   1
	    \
	     2
	      \
	       3
	        \
	         4
	          \
	           5
	            \
	             6

>click to show hints.

>####Hints:
>If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.

<!-- more -->
	
##解题思路
该题要求把一颗二叉树按照先序遍历顺序展成一个链表，不过这个链表还是用树的结果，即就地解决问题，就是一直往右走（没有左孩子）来模拟链表。老套路还是用递归来解决，维护先序遍历的前一个结点pre，然后每次把pre的左结点置空，右结点设为当前结点。这里需要注意的一个问题就是我们要先把右子结点保存一下，以便等会可以进行递归，否则有可能当前结点的右结点会被覆盖，后面就取不到了。算法的复杂度时间上还是一次遍历，O(n)。空间上是栈的大小，O(logn)。

树的题目主要考虑递归，要考虑好递归条件和结束条件。
##算法代码
代码采用JAVA实现： 
{% highlight java %}
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void flatten(TreeNode root) {
    	//定义前序节点的存放
    	ArrayList<TreeNode> pre=new ArrayList<TreeNode>();
    	pre.add(null);
        helper(root,pre);
    }

    public void helper(TreeNode root,ArrayList<TreeNode> pre)
    {
    	if(root==null)
    		return;
    	//因为root右节点在递归中会有变化，所以需要保存右节点
    	TreeNode tmp=root.right;
    	if(pre.get(0)!=null)
    	{
    		pre.get(0).left=null;
    		pre.get(0).right=root;
    	}
    	pre.set(0,root);
    	helper(root.left,pre);
    	helper(tmp,pre);
    }
}
{% endhighlight %}








