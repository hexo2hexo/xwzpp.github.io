---
layout: post
title:  LeetCode-Construct Binary Tree from Inorder and Postorder Traversal
description: "Construct Binary Tree from Inorder and Postorder Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Array,Depth-first Search]
duoshuo: true
---
##题目
####Construct Binary Tree from Inorder and Postorder Traversal
>Given inorder and postorder traversal of a tree, construct the binary tree.

>####Note:
>You may assume that duplicates do not exist in the tree.

<!-- more -->
	
##解题思路
该题和[Construct Binary Tree from Preorder and Inorder Traversal][1]的解法类似，只不过后序中最后一个节点才是根结点，因此与前序的差别是需要从后往前遍历。代码与[Construct Binary Tree from Preorder and Inorder Traversal][1]非常类似。

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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if(inorder==null || postorder==null)
        	return null;
        //将元素和其下标存放在map中，便于寻找
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<inorder.length;i++)
        	map.put(inorder[i],i);
        return helper(inorder,0,inorder.length-1,postorder,0,postorder.length-1,map);
    }

    public TreeNode helper(int[] inorder,int inL,int inR,int[] postorder,int postL,int postR,HashMap<Integer,Integer> map)
    {
    	if(inL>inR || postL>postR)
    		return null;
    	TreeNode root=new TreeNode(postorder[postR]);
    	int val=root.val;
    	int index=map.get(val);
    	root.left=helper(inorder,inL,index-1,postorder,postL,postL+index-inL-1,map);
    	root.right=helper(inorder,index+1,inR,postorder,postR-inR+index,postR-1,map);
    	return root;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal.html



