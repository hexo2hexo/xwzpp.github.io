---
layout: post
title:  LeetCode-Recover Binary Search Tree
description: "Recover Binary Search Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Depth-first Search]
duoshuo: true
---
##题目
####Recover Binary Search Tree
>Two elements of a binary search tree (BST) are swapped by mistake.

>Recover the tree without changing its structure.

>####Note:
>A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?   
>confused what `"{1,#,2,3}"` means? > read more on how binary tree is serialized on OJ.
>
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
该题是在二叉查找树中有一对元素顺序出现了调换，需要将其恢复出来。根据二叉查找树的性质，自身中序遍历后肯定是有序的，如果有两个元素被调换，则中序遍历的有序性将会被打破，那么调换的是哪两个元素呢？   
可以发现，有两种情况的元素会被调用，一是相邻的元素，二是不相邻的元素。第一种情况，如果是相邻的元素，此时在中序顺序中只有一对逆序，此时只需要调换他们两个即可。第二种情况，如果不相邻，则在中序顺序中会出现两对逆序，例如：`1234567`,调换`5`和`1`，此时得到`5234167`，会发现`52`和`41`是逆序，此时需要调换的是第一个逆序的第一个元素和第二个逆序的第二个元素。因此需要对逆序的个数进行判定。   
搞清楚了规律就容易实现了，中序遍历寻找逆序情况，调换的第一个元素，永远是第一个逆序的第一个元素，而调换的第二个元素如果只有一次逆序，则是那一次的后一个，如果有两次逆序则是第二次的后一个.

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
    public void recoverTree(TreeNode root) {
    	//pre中存放前缀节点，因为java是值传递，所以保存在全局变量中
    	ArrayList<TreeNode> pre=new ArrayList<TreeNode>();
    	pre.add(null);
    	//res中存在的是需要调换的两个节点
    	ArrayList<TreeNode> res=new ArrayList<TreeNode>();
        helper(root,pre,res); //进行中序遍历处理
        if(res.size()!=0) //说明有需要调换的节点
        {
        	int tmp=res.get(0).val;
        	res.get(0).val=res.get(1).val;
        	res.get(1).val=tmp;
        }
    }

    public void helper(TreeNode root,ArrayList<TreeNode> pre,ArrayList<TreeNode> res)
    {
    	if(root == null)
    		return;
    	helper(root.left,pre,res);
    	//如果前缀的值比root值大，说明出现了逆序
    	if(pre.get(0)!=null && pre.get(0).val>root.val)
    	{
    		//判断这是第几个逆序
    		if(res.size()==0)//说明是第一个逆序
    		{
    			res.add(pre.get(0));
    			res.add(root);
    		}else{ //说明是第二个逆序
    			res.set(1,root); //只需要修改第二个交换的值，因为第二个值是第二个逆序的后一个元素
    		}
    	}
    	//设定前缀值为root
    	pre.set(0,root);
    	helper(root.right,pre,res);
    }
}
{% endhighlight %}



