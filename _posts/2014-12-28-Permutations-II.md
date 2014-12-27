---
layout: post
title:  LeetCode-Permutations II 
description: "Permutations II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking]
duoshuo: true
---
##题目
####Permutations II
>Given a collection of numbers that might contain duplicates, return all possible unique permutations.

>For example,

>`[1,1,2]` have the following unique permutations:

>`[1,1,2]`, `[1,2,1]`, and `[2,1,1]`.

<!-- more -->
	
##解题思路
该题与[Permutations][1]类似，只是这题数组中存在重复的元素，需要考虑会产生重复的结果问题。对于重复的元素循环时跳过递归函数的调用，只对第一个未被使用的进行递归，我们那么这一次结果会出现在第一个的递归函数结果中，而后面重复的会被略过。如果第一个重复元素前面的元素还没在当前结果中，那么我们不需要进行递归。如果第一个重复元素前面的元素还没在当前结果中，那么我们不需要进行递归

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> permuteUnique(int[] num) {
    	ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
        if(num==null || num.length==0)
        	return res;
        int[] used=new int[num.length];
        for(int i=0;i<num.length;i++)
        	used[i]=0;
        Arrays.sort(num);
        helper(num,used,new ArrayList<Integer>(),res);
        return res;
    }

    void helper(int[] num,int[] used,ArrayList<Integer> cur,ArrayList<ArrayList<Integer>> res)
    {
    	if(cur.size()==num.length)
    	{
    		res.add(new ArrayList<Integer>(cur));
    		return;
    	}else
    	{
    		for(int i=0;i<num.length;i++)
    		{
    			if(i!=0 && num[i]==num[i-1] && used[i-1]==0) //对于重复的元素循环时跳过递归函数的调用，只对第一个未被使用的进行递归
    				continue;
    			if(used[i]==0)
    			{
    				used[i]=1;
    				cur.add(num[i]);
    				helper(num,used,cur,res);
    				cur.remove(cur.size()-1);
    				used[i]=0;
    			}
    		}
    	}
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Permutations.html