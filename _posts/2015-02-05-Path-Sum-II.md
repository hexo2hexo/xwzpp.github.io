---
layout: post
title:  LeetCode-Path Sum II
description: "Path Sum II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search]
duoshuo: true
---
##题目
####Path Sum II
>Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

>For example:
>Given the below binary tree and `sum = 22`,
>
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

>return
>
	[
	   [5,4,11,2],
	   [5,8,4,5]
	]

<!-- more -->
	
##解题思路
这道题与[Path Sum][1]的解题思路相同，只不过该题的最终需要把满足条件路径上的每个节点值进行保存。因此该题需要一个递归保存的过程。但是需要注意的是，递归回溯上来的时候要进行清理工作，代码框架与前面写的需要保存递归中间结果的方法都基本类似。

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
    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
    	ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
    	helper(root,sum,new ArrayList<Integer>(),res);
    	return res;
    }

    public void helper(TreeNode root,int sum,ArrayList<Integer> cur,ArrayList<ArrayList<Integer>> res)
    {
    	if(root==null)
    		return;
		//到达叶子节点且根结点的值等于sum
    	if(root.left==null && root.right==null && root.val==sum)
    	{
    		cur.add(root.val);
    		res.add(new ArrayList<Integer>(cur));
    		//清除操作
    		cur.remove(cur.size()-1);
    		return;
    	}
    	//没有到达叶子节点，左子树不为空
    	if(root.left!=null)
    	{
    		cur.add(root.val);
			//对左子树进行递归调用
    		helper(root.left,sum-root.val,cur,res);
    		//返回时，清除操作
    		cur.remove(cur.size()-1);
    	}
	    //没有到达叶子节点，右子树不为空
    	if(root.right!=null)
    	{
    		cur.add(root.val);
			//对右子树进行递归调用
    		helper(root.right,sum-root.val,cur,res);
    		//返回时，清除操作
    		cur.remove(cur.size()-1);
    	}
    		
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Path-Sum.html






