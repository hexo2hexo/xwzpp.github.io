---
layout: post
title:  LeetCode-Binary Tree Zigzag Level Order Traversal
description: "Binary Tree Zigzag Level Order Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Breadth-first Search,Stack]
duoshuo: true
---
##题目
####Binary Tree Zigzag Level Order Traversal
>Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

>For example:    
>Given binary tree `{3,9,20,#,#,15,7}`,
>
	    3
	   / \
	  9  20
	    /  \
	   15   7

>return its zigzag level order traversal as:
>
	[
	  [3],
	  [20,9],
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
该题其实还是对树的层次遍历，只不过有一点区别：在奇数层上是从左往右遍历，而在偶数层上是从右往左遍历，因此由于顺序是相反的，我们很容易想到的是用栈来存储每一层的节点。因此这里选用两个栈，一个栈用于读取节点，一个栈用于保存每一层的节点。

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
  public ArrayList<ArrayList<Integer>> zigzagLevelOrder(TreeNode root) {
	    ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
	    if(root==null)
	        return res;
	    LinkedList<TreeNode> stack = new LinkedList<TreeNode>();
	    int level=1;
	    ArrayList<Integer> item = new ArrayList<Integer>();
	    item.add(root.val);
	    res.add(item);
	    stack.push(root);
	    while(!stack.isEmpty())
	    {
	        LinkedList<TreeNode> newStack = new LinkedList<TreeNode>();
	        item = new ArrayList<Integer>();
	        while(!stack.isEmpty())
	        {
	            TreeNode node = stack.pop();
	            if(level%2==0)
	            {
	                if(node.left!=null)
	                {
	                    newStack.push(node.left);
	                    item.add(node.left.val);
	                }
	                if(node.right!=null)
	                {
	                    newStack.push(node.right);
	                    item.add(node.right.val);
	                }
	            }
	            else
	            {
	                if(node.right!=null)
	                {
	                    newStack.push(node.right);
	                    item.add(node.right.val);
	                }
	                if(node.left!=null)
	                {
	                    newStack.push(node.left);
	                    item.add(node.left.val);
	                }                   
	            }
	        }
	        level++;
	        if(item.size()>0)
	            res.add(item);
	        stack = newStack;
	    }
	    return res;
	}
}
{% endhighlight %}



