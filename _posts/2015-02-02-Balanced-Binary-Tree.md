---
layout: post
title:  LeetCode-Balanced Binary Tree
description: "Balanced Binary Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search]
duoshuo: true
---
##题目
####Balanced Binary Tree
>Given a binary tree, determine if it is height-balanced.

>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

<!-- more -->
	
##解题思路
该题是判断一个二叉树是否是平衡二叉树，平衡二叉树满足对树中的每一个节点，其左右子树的高度差都不大于1。因此，这里可以使用**递归**的方法进行判断。

一个二叉树是否是一个平衡二叉树的判断条件是：

	1. 左子树为平衡二叉树
	2. 右子树为平衡二叉树
	3. 左右子树的高度只差不大于1

这里面需要一个子方法求取每个树的高度，然而这个方法也可以使用递归方法求解。

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
    public boolean isBalanced(TreeNode root) {
        return helper(root);
    }

    //递归判断是否为平衡二叉树
    public boolean helper(TreeNode root)
    {
    	if(root==null)
    		return true;
    	int leftheight=getHeight(root.left);
    	int rightheight=getHeight(root.right);
    	/*平衡二叉树需要满足三个条件：
		*1.左子树为平衡二叉树
		*2.右子树为平衡二叉树
		*3.左右子树的高度只差不大于1
		*/
    	return helper(root.left)&&helper(root.right)&&Math.abs(leftheight-rightheight)<=1;
    }

    //获取二叉树的高度
    public int getHeight(TreeNode root)
    {
    	if(root==null)
    		return 0;
    	return Math.max(getHeight(root.left),getHeight(root.right))+1;
    }
}
{% endhighlight %}




