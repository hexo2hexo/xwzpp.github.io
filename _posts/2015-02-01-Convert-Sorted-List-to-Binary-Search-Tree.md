---
layout: post
title:  LeetCode-Convert Sorted List to Binary Search Tree
description: "Convert Sorted List to Binary Search Tree"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search,Linked List]
duoshuo: true
---
##题目
####Convert Sorted List to Binary Search Tree
>Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

<!-- more -->
	
##解题思路
该题是根据已排好序的链表得到一个高度平衡的二叉查找树，高度平衡指的是左右子树的高度只差不大于1。当然，这道题与[Convert Sorted Array to Binary Search Tree][1]很类似，但是在链表中不能用常量的时间获取中间节点，但是我们可以遍历得到中间节点，这样就得到自顶向下的解法1.

当然利用到树的中序遍历了，按照递归中序遍历的顺序对链表结点一个个进行访问，就能得到自底向上的解法2，而我们要构造的二分查找树正是按照链表的顺序来的。思路就是先对左子树进行递归，然后将当前结点作为根，迭代到下一个链表结点，最后在递归求出右子树即可。这种方法比较不容易想到，而且递归过程有点复杂。这种构造的方式比较绕，因为一般来说我们都是对于存在的树进行遍历，这里是模拟一个中序遍历的过程把树从无到有地构造出来。过程比较不常规。

##算法代码
代码采用JAVA实现：
自顶向下的方法，但是需要获取链表中的中间节点    
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; next = null; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
	 	//自顶向下的方法
	 	if(head==null)
	 		return null;
	 	ListNode cur=head;
	 	int len=0;
	 	while(cur!=null)
	 	{
	 		cur=cur.next;
	 		len++;
	 	}
	 	return helper(head,0,len-1);	        
    }
    //递归求解
    public TreeNode helper(ListNode head,int left,int right)
    {
    	if(left>right)
    		return null;
    	int mid=(left+right)/2;
    	//找到中间节点
    	int count=mid;
    	ListNode midnode=head;
    	while(count>left)
    	{
    		midnode=midnode.next;
    		count--;
    	}
    	TreeNode root=new TreeNode(midnode.val);
    	root.left=helper(head,left,mid-1);
    	root.right=helper(midnode.next,mid+1,right);
    	return root;

    }
}
{% endhighlight %}


自底向上的方法，递归比较复杂，需要好好思考    
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; next = null; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
	 	//自底向上的方法
	 	if(head==null)
	 		return null;
	 	ListNode cur=head;
	 	int len=0;
	 	while(cur!=null)
	 	{
	 		cur=cur.next;
	 		len++;
	 	}
	 	return helper(head,0,len-1);	        
    }
    //递归求解
    public TreeNode helper(ListNode head,int left,int right)
    {
    	if(left>right)
    		return null;
    	int mid=(left+right)/2;
    	//中序遍历的方法
    	//递归获取左子树
    	TreeNode rootleft=helper(head,left,mid-1);
    	//定义根结点
    	TreeNode root=new TreeNode(head.val);
    	root.left=rootleft;
    	//每次递归后，head都要向后移动
    	if(head.next!=null)
    	{
    		head.val=head.next.val;
    		head.next=head.next.next;
    	}
    	//这样当递归右子树的时候，head正好指向midnode.next，正好是右子树开始的位置
    	TreeNode rootright=helper(head,mid+1,right);
    	root.right=rootright;
    	return root;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Convert-Sorted-Array-to-Binary-Search-Tree.html




