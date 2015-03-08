---
layout: post
title:  LeetCode-Construct Binary Tree from Preorder and Inorder Traversal
description: "Construct Binary Tree from Preorder and Inorder Traversal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Array,Depth-first Search]
duoshuo: true
---
##题目
####Construct Binary Tree from Preorder and Inorder Traversal
>Given preorder and inorder traversal of a tree, construct the binary tree.

>####Note:
>You may assume that duplicates do not exist in the tree.

<!-- more -->
	
##解题思路
这道题是树中比较有难度的题目，需要根据先序遍历和中序遍历来构造出树来。这道题看似毫无头绪，其实梳理一下还是有章可循的。下面我们就用一个例子来解释如何构造出树。    
假设树的先序遍历是12453687，中序遍历是42516837。这里最重要的一点就是先序遍历可以提供根的所在，而根据中序遍历的性质知道根的所在就可以将序列分为左右子树。比如上述例子，我们知道1是根，所以根据中序遍历的结果425是左子树，而6837就是右子树。接下来根据切出来的左右子树的长度又可以在先序便利中确定左右子树对应的子序列（先序遍历也是先左子树后右子树）。根据这个流程，左子树的先序遍历和中序遍历分别是245和425，右子树的先序遍历和中序遍历则是3687和6837，我们重复以上方法，可以继续找到根和左右子树，直到剩下一个元素。可以看出这是一个比较明显的**递归**过程，对于寻找根所对应的下标，我们可以先建立一个**HashMap**，以免后面需要进行线行搜索，这样每次递归中就只需要常量操作就可以完成对根的确定和左右子树的分割。

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder==null || inorder==null)
            return null;
		//将值和下标存放到HashMap中，以便后续可以方便得到
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i=0;i<inorder.length;i++)
        {
            map.put(inorder[i],i);
        }
        return helper(preorder,0,preorder.length-1,inorder,0,inorder.length-1, map);
    }
    private TreeNode helper(int[] preorder, int preL, int preR, int[] inorder, int inL, int inR, HashMap<Integer, Integer> map)
    {
        if(preL>preR || inL>inR)
            return null;
        TreeNode root = new TreeNode(preorder[preL]);
        int index = map.get(root.val);
        root.left = helper(preorder, preL+1, index-inL+preL, inorder, inL, index-1, map);
        root.right = helper(preorder, preL+index-inL+1, preR, inorder, index+1, inR,map);
        return root;
    }
}
{% endhighlight %}



