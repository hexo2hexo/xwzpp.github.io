---
layout: post
title:  LeetCode-Sum Root to Leaf Numbers
description: "Sum Root to Leaf Numbers"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Sum Root to Leaf Numbers
>Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

>An example is the root-to-leaf path `1->2->3` which represents the number `123`.

>Find the total sum of all root-to-leaf numbers.

>For example,
>
	    1
	   / \
	  2   3

>The root-to-leaf path `1->2` represents the number `12`.      
>The root-to-leaf path `1->3` represents the number `13`.     

>Return the `sum = 12 + 13 = 25`.

<!-- more -->
	
##解题思路 
这是一道树的题目，一般使用递归来做，主要就是考虑递归条件和结束条件。这道题思路还是比较明确的，目标是把从根到叶子节点的所有路径得到的整数都累加起来，递归条件即是把当前的sum乘以10并且加上当前节点传入下一函数，进行递归，最终把左右子树的总和相加。结束条件的话就是如果一个节点是叶子，那么我们应该累加到结果总和中，如果节点到了空节点，则不是叶子节点，不需要加入到结果中，直接返回0即可

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
    public int sumNumbers(TreeNode root) {
    	return helper(root,0);
	}
	private int helper(TreeNode root, int sum)
	{
	    if(root == null)
	        return 0;
	    if(root.left==null && root.right==null)
	        return sum*10+root.val;
	    return helper(root.left,sum*10+root.val)+helper(root.right,sum*10+root.val); //加上左右子树中所有路径的长度
	}
}
{% endhighlight %}









