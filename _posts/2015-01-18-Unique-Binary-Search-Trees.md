---
layout: post
title:  LeetCode-Unique Binary Search Trees
description: "Unique Binary Search Trees"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Tree,Dynamic Programming]
duoshuo: true
---
##题目
####Unique Binary Search Trees
>Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

>For example,    
>Given n = 3, there are a total of 5 unique BST's.
	
	   1         3     3      2      1
	    \       /     /      / \      \
	     3     2     1      1   3      2
	    /     /       \                 \
	   2     1         2                 3

<!-- more -->
	
##解题思路
这道题要求可行的二叉查找树的数量，其实二叉查找树可以任意取根，只要满足中序遍历有序的要求就可以。从处理子问题的角度来看，选取一个结点为根，就把结点切成左右子树，以这个结点为根的可行二叉树数量就是左右子树可行二叉树数量的乘积，所以总的数量是将以所有结点为根的可行结果累加起来.

这是一个典型的动态规划的定义方式（根据其实条件和递推式求解结果）。所以思路也很明确了，维护量res[i]表示含有i个结点的二叉查找树的数量。根据上述递推式依次求出1到n的的结果即可。

动态规划定义如下：

	res[i]:表示含有i个节点的可行二叉树的数量
	其中res[0]=1,res[1]=1
	res[i]+=res[j]*res[i-j+1] j=0,2....i-1

##算法代码
代码采用JAVA实现：    
{% highlight java %}
public class Solution {
    public int numTrees(int n) {
        if(n<0)
        	return 0;
        int[] res=new int[n+1];
        //动态规划的初始条件
        res[0]=1;
        res[1]=1;
        for(int i=2;i<=n;i++)
        {
        	//i个节点的可行查找树个数为多个左右子树情况的乘积之和
        	for(int j=0;j<i;j++)
        	{
        		res[i]+=res[j]*res[i-j-1];
        	}
        }
        return res[n];
    }
}
{% endhighlight %}

