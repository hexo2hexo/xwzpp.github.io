---
layout: post
title:  LeetCode-Combination Sum III
description: "Combination Sum III"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Backtracking]
duoshuo: true
---
##题目
####Combination Sum III
> Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

>Ensure that numbers within the set are sorted in ascending order.

>Example 1:

>Input: k = 3, n = 7

>Output:

	[[1,2,4]]


>Example 2:

>Input: k = 3, n = 9

>Output:

	[[1,2,6], [1,3,5], [2,3,4]]

>####Credits:
>Special thanks to @mithmatt for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题的思路与[Combination Sum][1]和[Combination Sum II][2]类似，是一个求解循环子问题，但是这里的结果集中需要元素的长度为K，只需要当和为n的时候，判断当前满足和的元素的个数是否为k即可。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res=new ArrayList<List<Integer>>();
        int[] candidates={1,2,3,4,5,6,7,8,9};
        List<Integer> cur=new ArrayList<Integer>();
        helper(candidates,0,k,n,cur,res);
        return res;
    }

    //cur保存当前已经放入的元素
    public void helper(int[] candidates,int start,int k,int n,List<Integer> cur,List<List<Integer>> res)
    {
    	if(n<0) return;
    	if(n==0){
    		if(cur.size()==k)
    			res.add(new ArrayList<Integer>(cur));
    		else
    			return;
    	}

    	//循环处理子问题
    	for(int i=start;i<candidates.length;i++)
    	{
    		//这里不需要考虑重复元素，因为是1-9的元素，没有重复
    		cur.add(candidates[i]);
    		helper(candidates,i+1,k,n-candidates[i],cur,res);
    		cur.remove(cur.size()-1);
    	}
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Combination-Sum.html
[2]:http://pisxw.com/algorithm/Combination-Sum-II.html















