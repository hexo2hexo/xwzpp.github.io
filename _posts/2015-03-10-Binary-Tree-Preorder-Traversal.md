---
layout: post
title:  LeetCode-Binary Tree Preorder Traversal
description: "Binary Tree Preorder Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Stack]
duoshuo: true
---
##题目
####Binary Tree Preorder Traversal
>Given a binary tree, return the preorder traversal of its nodes' values.

>For example:      
>Given binary tree {1,#,2,3},
>
	   1
	    \
	     2
	    /
	   3

>return [1,2,3].

>**Note**: Recursive solution is trivial, could you do it iteratively?

<!-- more -->
	
##解题思路
该题是对二叉树进行先序遍历，如果使用递归求解非常简单，这里代码就不写了。

题目中要求不要使用递归写法，因此可以使用**栈**来将递归写法变成非递归写法。这里需要注意的是先要压入右节点，然后在压入左节点，这样首先访问的就是左节点了哈。

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
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> res=new ArrayList<Integer>();
        if(root==null)
        	return res;
        //定义一个栈
        LinkedList<TreeNode> stack=new LinkedList<TreeNode>();
        stack.push(root);
        while(!stack.isEmpty())
        {
        	TreeNode node=stack.pop();
        	res.add(node.val);
        	if(node.right!=null)
        		stack.push(node.right);
        	if(node.left!=null)
        		stack.push(node.left);
        }
        return res;
    }
}
{% endhighlight %}





