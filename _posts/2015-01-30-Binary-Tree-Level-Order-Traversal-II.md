---
layout: post
title:  LeetCode-Binary Tree Level Order Traversal II
description: "Binary Tree Level Order Traversal II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Breadth-first Search]
duoshuo: true
---
##题目
####Binary Tree Level Order Traversal II
>Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

>For example:   
>Given binary tree `{3,9,20,#,#,15,7}`,
>
	    3
	   / \
	  9  20
	    /  \
	   15   7

>return its bottom-up level order traversal as:
>
	[
	  [15,7],
	  [9,20],
	  [3]
	]

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
该题和[Binary Tree Level Order Traversal][1]的解法相同，只不过在最后结果上是其结果的转置。

这道题我没有想到什么好的做法可以一次的自底向上进行层序遍历，能想到的就是进行[Binary Tree Level Order Traversal][1]中的遍历，然后对结果进行一次reverse.

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
    public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
    	ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
    	if(root==null)
    		return res;
    	//使用队列来存储节点
    	LinkedList<TreeNode> queen=new LinkedList<TreeNode>();
    	//使用队列来存储上述队列中节点的层数
    	LinkedList<Integer> cequeen=new LinkedList<Integer>();
    	queen.addLast(root);
    	cequeen.addLast(0);
    	int ce=0;
    	ArrayList<Integer> cur=new ArrayList<Integer>();
    	while(!queen.isEmpty())
    	{
    		if(ce==cequeen.getFirst())
    		{
    			TreeNode no=queen.removeFirst();
    			int cengshu=cequeen.removeFirst();
    			cur.add(no.val);
    			if(no.left!=null)
    			{
    				queen.addLast(no.left);
    				cequeen.addLast(cengshu+1);
    			}
    			if(no.right!=null)
    			{
    				queen.addLast(no.right);
    				cequeen.addLast(cengshu+1);
    			}
    		}else{
    			res.add(new ArrayList<Integer>(cur));
    			ce++;
    			cur.clear();
    		}
    	}
    	//最后一次不要忘记加入
    	res.add(new ArrayList<Integer>(cur));
    	Collections.reverse(res);
    	return res;

    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Binary-Tree-Level-Order-Traversal.html



