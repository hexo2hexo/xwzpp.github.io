---
layout: post
title:  LeetCode-Symmetric Tree
description: "Symmetric Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Symmetric Tree
>Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

>For example, this binary tree is symmetric:
>
	    1
	   / \
	  2   2
	 / \ / \
	3  4 4  3

>But the following is not:
>
	    1
	   / \
	  2   2
	   \   \
	   3    3

>####Note:
>Bonus points if you could solve it both recursively and iteratively.

>confused what `"{1,#,2,3}"` means? > read more on how binary tree is serialized on OJ.


>####OJ's Binary Tree Serialization:
>The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.

>Here's an example:
>
	   1
	  / \
	 2   3
	    /
	   4
	    \
	     5

>The above binary tree is serialized as `"{1,2,3,#,#,4,#,#,5}"`.

<!-- more -->
	
##解题思路
该题是判定一个二叉树是否是中心对称的。我们可以通过对二叉树进行遍历而进行判定，是一个递归的过程，一颗树对称其实就是看左右子树是否对称，一句话就是左同右，右同左，结点是对称的相等。我们主要说说结束条件，假设到了某一结点，不对称的条件有以下三个：（1）左边为空而右边不为空；（2）左边不为空而右边为空；（3）左边值不等于右边值。根据这几个条件在遍历时进行判断即可。

这里可以使用栈来达到非递归的目的，不过里面的判断条件就比较多了。

##算法代码
代码采用JAVA实现： 
算法的递归实现：   
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
    public boolean isSymmetric(TreeNode root) {
    	//判断左右子树是否对称
    	if(root==null)
    		return true;
        return helper(root.left,root.right);
    }

    public boolean helper(TreeNode left,TreeNode right)
    {
    	//结束条件
    	if(left==null && right!=null)
    		return false;
    	if(left!=null && right==null)
    		return false;
    	if(left==null && right==null)
    		return true;
    	return left.val==right.val && helper(left.left,right.right) && helper(left.right,right.left);
    }
}

{% endhighlight %}

算法的非递归实现：   
{% highlight java %}
//非递归实现
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
    public boolean isSymmetric(TreeNode root) {
    	if(root==null)
    		return true;
    	if(root.left==null && root.right==null)
    		return true;
    	if(root.left==null && root.right!=null)
    		return false;
    	if(root.left!=null && root.right==null)
    		return false;
    	//使用两个栈来实现非递归
    	LinkedList<TreeNode> stack1=new LinkedList<TreeNode>();
    	LinkedList<TreeNode> stack2=new LinkedList<TreeNode>();
    	stack1.add(root.left);
    	stack2.add(root.right);
    	while(!stack1.isEmpty() && !stack2.isEmpty())
    	{
    		TreeNode tn1=stack1.poll();
    		TreeNode tn2=stack2.poll();
    		if(tn1.val!=tn2.val)
    			return false;
    		if(tn1.left==null && tn2.right!=null)
    			return false;
    		if(tn1.left!=null && tn2.right==null)
    			return false;
    		if(tn1.right==null && tn2.left!=null)
    			return false;
    		if(tn1.right!=null && tn2.left==null)
    			return false;
    		if(tn1.left!=null && tn2.right!=null)
    		{
    			stack1.add(tn1.left);
    			stack2.add(tn2.right);
    		}
    		if(tn1.right!=null && tn2.left!=null)
    		{
    			stack1.add(tn1.right);
    			stack2.add(tn2.left);
    		}
    	}
    	return true;
    }
}
{% endhighlight %}



