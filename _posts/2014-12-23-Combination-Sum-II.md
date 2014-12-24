---
layout: post
title:  LeetCode-Combination Sum II
description: "Combination Sum II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Backtracking]
duoshuo: true
---
##题目
####Combination Sum II
>Given a collection of candidate numbers (**C**) and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

>Each number in **C** may only be used once in the combination.

>####Note:
* All numbers (including target) will be positive integers.
* Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
* The solution set must not contain duplicate combinations. 
   
>For example, given candidate set `10,1,2,7,6,1,5` and target `8`,
    
>A solution set is:
   
>`[1, 7]`
 
>`[1, 2, 5]`
 
>`[2, 6]`
 
>`[1, 1, 6]` 

<!-- more -->

##解题思路
该题与[Combination Sum][1]的解法相同，只是该题中每个元素只能用一次，所以对`i`元素的递归求解应该从第`i+1`个开始，为了避免最后结果中出现重复的问题，需要跳过重复的元素。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> combinationSum2(int[] num, int target) {
        ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
        if(num==null||num.length==0)
        	return res;
        Arrays.sort(num);
        helper(num,0,target,new ArrayList<Integer>(),res);
        return res;
    }

    void helper(int[] num,int start,int target,ArrayList<Integer> cur,ArrayList<ArrayList<Integer>> res)
    {
    	if(target<0)
    		return;
    	if(target==0)
    	{
    		res.add(new ArrayList<Integer>(cur));
    		return;
    	}
    	for(int i=start;i<num.length;i++)
    	{
    		if(i!=start&&num[i]==num[i-1]) //去除重复的问题，跳过重复的元素
    			continue;
    		cur.add(num[i]);
    		helper(num,i+1,target-num[i],cur,res);
    		cur.remove(cur.size()-1);
    	}
    	return;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Combination-Sum.html
