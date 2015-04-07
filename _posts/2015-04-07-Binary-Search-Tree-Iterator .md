---
layout: post
title:  LeetCode-Binary Search Tree Iterator
description: "Binary Search Tree Iterator"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Stack]
duoshuo: true
---
##题目
####Binary Search Tree Iterator
>Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

>Calling next() will return the next smallest number in the BST.

>**Note**: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
就是找到以这个 root 为 根节点的最小的 值。 用一个 stack 作为buffer 来存储， 先存入 左边节点， 当输出以后， 再向右节点移动一个， 然后再存储 进去所有左节点， 和 [inorder 遍历 的非递归解法][1]一样。

易错点： 要检查 node.right ！＝ null， 才能向右移动， 否则就不用管， 意思就是向上移动一个。

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

public class BSTIterator {
	LinkedList<TreeNode> stack=new LinkedList<TreeNode>();
    public BSTIterator(TreeNode root) {
        while(root!=null)
        {
        	stack.push(root);
        	root=root.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode cur=stack.pop();
        int res=cur.val;
        if(cur.right!=null)
        {
        	cur=cur.right;
        	while(cur!=null)
        	{
        		stack.push(cur);
        		cur=cur.left;
        	}
        }
        return res;
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Binary-Tree-Postorder-Traversal.html






