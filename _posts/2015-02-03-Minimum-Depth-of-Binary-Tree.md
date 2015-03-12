---
layout: post
title:  LeetCode-Minimum Depth of Binary Tree
description: "Minimum Depth of Binary Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search]
duoshuo: true
---
##题目
####Minimum Depth of Binary Tree
>Given a binary tree, find its minimum depth.

>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

<!-- more -->
	
##解题思路
该题与[Maximum Depth of Binary Tree][1]的解题思路非常类似，但是在条件方面有一些区别。因为求得是最小深度，当遇到子树为空的情况下，该子树就不应该为考虑。因此条件可以分为如下5种：

	1. 该树为一个空树，则其最小深度为0；
	2. 该树不为空且其左右子树都不为空，则最小深度为左子树最小深度和右子树最小深度中较小的那一个+1；
	3. 该树不为空，但是其左子树为空，右子树不为空，则最小深度为右子树的最小深度+1；
	4. 该树不为空，但是其左子树不为空，右子树为空，则最小深度为左子树的最小深度+1；
	5. 该树不为空，但是其左子树和右子树都为空，则最小深度为1；

根据上述的5种条件，可以判断一棵树的最小深度，然后在采用**递归**的方式进行求解即可。

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
    public int minDepth(TreeNode root) {
        //这与求一个树的最大深度类似，依旧采用递归的方法
        int num=0;
        //如果为空树，直接返回0
        if(root==null)
            return 0;
        //如果两个子树都不为空
        if(root.left!=null && root.right!=null)
			num=1+Math.min(minDepth(root.left),minDepth(root.right));
		//如果左子树为空，右子树不为空
		if(root.left==null && root.right!=null)
			num=1+minDepth(root.right);
		//如果左子树不为空，右子树为空
		if(root.left!=null && root.right==null)
			num=1+minDepth(root.left);
		//如果两个子树都为空
		if(root.left==null && root.right==null)
			num=1;
		return num;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Maximum-Depth-of-Binary-Tree.html




