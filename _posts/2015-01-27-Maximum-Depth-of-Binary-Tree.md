---
layout: post
title:  LeetCode-Maximum Depth of Binary Tree
description: "Maximum Depth of Binary Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Maximum Depth of Binary Tree
>Given a binary tree, find its maximum depth.

>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

<!-- more -->
	
##解题思路
该题是树中求解最大深度的问题，该题可以采用深度优先遍历，然后使用递归求解比较方便，因为整个树的最大深度为左子树和右子树中最大深度中较大的一个+1.因此可以很容易的写出递归代码。

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
    public int maxDepth(TreeNode root) {
        if(root == null)
        	return 0;
        return 1+Math.max(maxDepth(root.left),maxDepth(root.right));
    }
}
{% endhighlight %}



