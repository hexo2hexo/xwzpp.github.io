---
layout: post
title:  LeetCode-Binary Tree Level Order Traversal
description: "Binary Tree Level Order Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Breadth-first Search]
duoshuo: true
---
##题目
####Binary Tree Level Order Traversal
>Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

>For example:     
>Given binary tree `{3,9,20,#,#,15,7}`,
>
	    3
	   / \
	  9  20
	    /  \
	   15   7

>return its level order traversal as:
>
	[
	  [3],
	  [9,20],
	  [15,7]
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
该题是对二叉树进行层次优先遍历，层次遍历主要采用队列的形式进行存储，通过将每个节点的左孩子和右孩子放入队列中，然后每次从队列中取出元素即可。在java中使用LinkedList来实现队列操作，其中主要方法为：入队：addLast(),出队：revomeFirst(),获取第一个元素：getFirst(),判断队列是否为空：isEmpty();

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
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
        //该队列中放入节点
        LinkedList<TreeNode> queen=new LinkedList<TreeNode>();
        //该队列中放入queen中对应节点的层次
        LinkedList<Integer> cequeen=new LinkedList<Integer>();
        if(root==null)
        	return res;
        queen.addLast(root);
        cequeen.addLast(0);
        int cengshu=0;
        ArrayList<Integer> cur=new ArrayList<Integer>();
        while(!queen.isEmpty())
        {
        	int ce=cequeen.getFirst();
        	if(ce==cengshu)
        	{
        		TreeNode no=queen.removeFirst();
        		int noce=cequeen.removeFirst();
        		cur.add(no.val);
        		if(no.left!=null)
        		{
        			queen.addLast(no.left);
        			cequeen.addLast(noce+1);
        		} 			
        		if(no.right!=null)
        		{
        			queen.addLast(no.right);
        			cequeen.addLast(noce+1);
        		}       			
        	}else{
        		res.add(new ArrayList<Integer>(cur));
        		cur.clear();
        		cengshu++;
        	}
        }
        res.add(new ArrayList<Integer>(cur));
        return res;
    }
}
{% endhighlight %}



