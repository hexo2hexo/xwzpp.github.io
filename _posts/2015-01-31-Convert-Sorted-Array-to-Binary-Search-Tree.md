---
layout: post
title:  LeetCode-Convert Sorted Array to Binary Search Tree
description: "Convert Sorted Array to Binary Search Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Convert Sorted Array to Binary Search Tree
>Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

<!-- more -->
	
##解题思路
该题是根据已排好序的数组得到一个高度平衡的二叉查找树，高度平衡指的是左右子树的高度只差不大于1。因此这里可以采用**递归**的方式进行求解。   
每次选取待求解数组中的中间元素作为根，然后左边递归得到左子树，右边递归得到右子树即可。

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
    public TreeNode sortedArrayToBST(int[] num) {
        if(num==null || num.length==0)
        	return null;
        return helper(num,0,num.length-1);
    }
    //采用递归的方式
    public TreeNode helper(int[] num,int left,int right)
    {
    	if(left>right)
    		return null;
    	//为了确保得到的二叉查找树是高度平衡的，此时选取中点作为根
    	int mid=(right+left)/2;
    	TreeNode root=new TreeNode(num[mid]);
    	root.left=helper(num,left,mid-1); //递归求解左子树
    	root.right=helper(num,mid+1,right);//递归求解右子树
    	return root;
    }
}
{% endhighlight %}




