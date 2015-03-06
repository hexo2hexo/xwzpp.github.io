---
layout: post
title:  LeetCode-Validate Binary Search Tree
description: "Validate Binary Search Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Validate Binary Search Tree
>Given a binary tree, determine if it is a valid binary search tree (BST).

>Assume a BST is defined as follows:
>
* The left subtree of a node contains only nodes with keys less than the node's key.   
* The right subtree of a node contains only nodes with keys greater than the node's key.   
* Both the left and right subtrees must also be binary search trees.
    
>confused what `"{1,#,2,3}"` means? > read more on how binary tree is serialized on OJ.
>
####OJ's Binary Tree Serialization:
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
这道题是检查一颗二分查找树是否合法，二分查找树是非常常见的一种数据结构，因为它可以在O(logn)时间内实现搜索.  
利用二分查找树的性质，就是它的中序遍历结果是按顺序递增的。根据这一点我们只需要中序遍历这棵树，然后保存前驱结点，每次检测是否满足递增关系即可。注意以下代码我么用一个一个变量的数组去保存前驱结点，原因是java没有传引用的概念，如果传入一个变量，它是按值传递的，所以是一个备份的变量，改变它的值并不能影响它在函数外部的值，算是java中的一个小细节

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
   public boolean isValidBST(TreeNode root) {
        ArrayList<Integer> pre = new ArrayList<Integer>();
        pre.add(null);
        return helper(root, pre);
    }
    private boolean helper(TreeNode root, ArrayList<Integer> pre)
    {
        if(root == null)
            return true;
        boolean left = helper(root.left,pre);
        if(pre.get(0)!=null && root.val<=pre.get(0))
            return false;
        pre.set(0,root.val);
        return left && helper(root.right,pre);
    }
}
{% endhighlight %}



