---
layout: post
title:  LeetCode-Unique Binary Search Trees II
description: "Unique Binary Search Trees II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Dynamic Programming]
duoshuo: true
---
##题目
####Unique Binary Search Trees II
>Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

>For example,   
>Given n = 3, your program should return all 5 unique BST's shown below.
>
	   1         3     3      2      1
	    \       /     /      / \      \
	     3     2     1      1   3      2
	    /     /       \                 \
	   2     1         2                 3

>confused what `"{1,#,2,3}"` means? > read more on how binary tree is serialized on OJ.


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
这道题是求解所有可行的二叉查找树,算法上还是用求解NP问题的方法来求解，也就是[N-Queens][1]中介绍的在循环中调用递归函数求解子问题。思路是每次一次选取一个结点为根，然后递归求解左右子树的所有结果，最后根据左右子树的返回的所有子树，依次选取然后接上（每个左边的子树跟所有右边的子树匹配，而每个右边的子树也要跟所有的左边子树匹配，总共有左右子树数量的乘积种情况），构造好之后作为当前树的结果返回。

##算法代码
代码采用JAVA实现：    
{% highlight java %}
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; left = null; right = null; }
 * }
 */
public class Solution {
    public ArrayList<TreeNode> generateTrees(int n) {
        if(n<0)
        	return null;
        return helper(1,n);  
    }

    //表示从left节点到right节点构造可行的二叉查找树
    public ArrayList<TreeNode> helper(int left,int right)
    {
    	ArrayList<TreeNode> res=new ArrayList<TreeNode>();
    	//不存在这样的树
    	if(left>right){
    		res.add(null); //表示空树
    		return res;
    	}
    	//取left到right间每个节点作为根
    	for(int i=left;i<=right;i++)
    	{
    		//递归获取每个左子树和右子树的可行二叉查找树情况
    		// helper函数得到的是范围从left到right的所有满足条件的树~ 从left到right，我们选取i作为根，那么剩下的左子树就是left到i-1,右子树就是i+1到right~
    		ArrayList<TreeNode> leftres=helper(left,i-1);
    		ArrayList<TreeNode> rightres=helper(i+1,right);
    		//每个左边的子树跟所有右边的子树匹配，而每个右边的子树也要跟所有的左边子树匹配，总共有左右子树数量的乘积种情况
    		for(int j=0;j<leftres.size();j++)
    		{
    			for(int k=0;k<rightres.size();k++)
    			{
    				TreeNode root=new TreeNode(i);
    				root.left=leftres.get(j);
    				root.right=rightres.get(k);
    				res.add(root);
    			}
    		}
    	}
    	return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/N-Queens.html

