---
layout: post
title:  LeetCode-Binary Tree Maximum Path Sum
description: "Binary Tree Maximum Path Sum"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Binary Tree Maximum Path Sum
>Given a binary tree, find the maximum path sum.

>The path may start and end at any node in the tree.

>For example:   
>Given the below binary tree,   
>
       1
      / \
     2   3

>Return `6`.

<!-- more -->
	
##解题思路
这道题是求树的路径和的题目，不过和平常不同的是这里的路径不仅可以从根到某一个结点，而且路径可以从左子树某一个结点，然后到达右子树的结点，就像题目中所说的可以起始和终结于任何结点。在这里树没有被看成有向图，而是被当成无向图来寻找路径。因为这个路径的灵活性，我们需要对递归返回值进行一些调整，而不是通常的返回要求的结果。在这里，函数的返回值定义为以自己为根的一条从根到子结点的最长路径（这里路径就不是当成无向图了，必须往单方向走）。这个返回值是为了提供给它的父结点计算自身的最长路径用，而结点自身的最长路径（也就是可以从左到右那种）则只需计算然后更新即可。这样一来，一个结点自身的最长路径就是它的左子树返回值（如果大于0的话），加上右子树的返回值（如果大于0的话），再加上自己的值。而返回值则是自己的值加上左子树返回值，右子树返回值或者0（注意这里是“或者”，而不是“加上”，因为返回值只取一支的路径和）。在过程中求得当前最长路径时比较一下是不是目前最长的，如果是则更新

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
    public int maxPathSum(TreeNode root) {
        if(root==null)
        	return 0;
        //由于java是值传递，但是我们需要在递归中保存最大的路径长度，因此定义个ArryList便于修改,其中保存最大的长度。
        ArrayList<Integer> res=new ArrayList<Integer>();
        res.add(Integer.MIN_VALUE);
        helper(root,res);
        return res.get(0);
    }
    //这里需要一个返回值，返回以root节点为根的从root节点出发的最长路径长度
    public int helper(TreeNode root,ArrayList<Integer> res)
    {
    	if(root==null)
    		return 0;
    	int left=helper(root.left,res); //返回左子树的最长路径长度
    	int right=helper(root.right,res);//返回右子树的最长路径长度
    	int cur=(left>0?left:0)+(right>0?right:0)+root.val; //从左子树到右子树的路径长度
    	if(cur>res.get(0))
    		res.set(0,cur);
    	return root.val+Math.max(Math.max(left,0),Math.max(right,0));
    }
}
{% endhighlight %}









