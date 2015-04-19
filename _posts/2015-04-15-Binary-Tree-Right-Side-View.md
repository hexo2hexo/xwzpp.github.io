---
layout: post
title:  LeetCode-Binary Tree Right Side View
description: "Binary Tree Right Side View"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search,Breadth-first Search]
duoshuo: true
---
##题目
####Binary Tree Right Side View
>Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

>For example:
>Given the following binary tree,
>
	   1            <---
	 /   \
	2     3         <---
	 \     \
	  5     4       <---
>You should return [1, 3, 4].

>####Credits:
>Special thanks to @amrsaqr for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这道题我们可以发现，从右边看树，看到的其实是每一层的最后一个节点，因此我们可以采用广度优先遍历，并且记录每一个节点的层数，当该层最后一个节点出现的时候，就将其放入结果中。

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
    public List<Integer> rightSideView(TreeNode root) {
    	ArrayList<Integer> res=new ArrayList<Integer>();
    	if(root==null)
    		return res;
    	//使用广度优先搜索
    	LinkedList<TreeNode> queen=new LinkedList<TreeNode>();
    	LinkedList<Integer> ceng=new LinkedList<Integer>(); //记录每个节点的层数
    	int curceng=0;
    	queen.offer(root);
    	ceng.offer(0);
    	TreeNode cur=root;
    	while(!queen.isEmpty())
    	{
    		TreeNode tmp=queen.poll();
    		int tmpc=ceng.poll();
    		if(tmpc!=curceng)
    		{
    			res.add(cur.val);
    			curceng=tmpc;
    		}
			if(tmp.left!=null)
			{
				queen.offer(tmp.left);
				ceng.offer(tmpc+1);
			}
			if(tmp.right!=null)
			{
				queen.offer(tmp.right);
				ceng.offer(tmpc+1);
			}
    		cur=tmp;
    	}
    	res.add(cur.val);
    	return res;
        
    }
}
{% endhighlight %}










