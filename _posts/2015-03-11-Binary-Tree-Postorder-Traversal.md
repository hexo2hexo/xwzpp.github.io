---
layout: post
title:  LeetCode-Binary Tree Postorder Traversal
description: "Binary Tree Postorder Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Stack]
duoshuo: true
---
##题目
####Binary Tree Postorder Traversal
>Given a binary tree, return the postorder traversal of its nodes' values.

>For example:     
>Given binary tree `{1,#,2,3}`,
>
	   1
	    \
	     2
	    /
	   3

>return `[3,2,1]`.

>**Note**: Recursive solution is trivial, could you do it iteratively?

<!-- more -->
	
##解题思路
该题是对二叉树进行后序遍历，如果使用递归求解非常简单，这里代码就不写了。

题目中要求不要使用递归写法，因此可以使用**栈**来将递归写法变成非递归写法。但是后序遍历的非递归算法还是比较复杂的。

最下面在弹栈的时候需要分情况一下：
1）如果当前栈顶元素的右结点存在并且还没访问过（也就是右结点不等于上一个访问结点），那么就把当前结点移到右结点继续循环；
2）如果栈顶元素右结点是空或者已经访问过，那么说明栈顶元素的左右子树都访问完毕，应该访问自己继续回溯了。

在下面代码中，都用相似的结构实现了前序，中序的遍历，以便于记忆。

##算法代码
代码采用JAVA实现：
 
先序遍历非递归：
{% highlight java %}
//先序遍历
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
    public ArrayList<Integer> postpreorderTraversal(TreeNode root) {
    	ArrayList<Integer> res=new ArrayList<Integer>();
        if(root==null)
        	return res;
        LinkedList<TreeNode> stack=new LinkedList<TreeNode>();//定义栈
        while(root!=null || !stack.isEmpty())
        {
        	if(root!=null)
        	{
        		stack.push(root);
        		res.add(root.val);
        		root=root.left;
        	}else{
        		root=stack.pop();
        		root=root.right;
        	}
        	
        }
        return res;

    }
}
{% endhighlight %}


中序遍历非递归：
{% highlight java %}
//中序遍历
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
    public ArrayList<Integer> postinorderTraversal(TreeNode root) {
    	ArrayList<Integer> res=new ArrayList<Integer>();
        if(root==null)
        	return res;
        LinkedList<TreeNode> stack=new LinkedList<TreeNode>();//定义栈
        while(root!=null || !stack.isEmpty())
        {
        	if(root!=null)
        	{
        		stack.push(root);
        		root=root.left;
        	}else{
        		root=stack.pop();
        		res.add(root.val);
        		root=root.right;
        	}
        	
        }
        return res;

    }
}
{% endhighlight %}


后序遍历非递归：
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
    public ArrayList<Integer> postorderTraversal(TreeNode root) {
    	ArrayList<Integer> res=new ArrayList<Integer>();
        if(root==null)
        	return res;
        LinkedList<TreeNode> stack=new LinkedList<TreeNode>();//定义栈
        TreeNode pre=null;//记录前一个访问的节点
        while(root!=null || !stack.isEmpty())
        {
        	if(root!=null) //root表示当前节点
        	{
        		 stack.push(root);
        		 root=root.left;
        	}else{
        		TreeNode peeknode=stack.peek();
        		if(peeknode.right!=null && peeknode.right!=pre)
        		{
        			root=peeknode.right;
        		}else{
        			stack.pop();
        			res.add(peeknode.val);
        			pre=peeknode;
        		}
        	}
        }
        return res;

    }
}
{% endhighlight %}





