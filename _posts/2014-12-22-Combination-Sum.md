---
layout: post
title:  LeetCode-Combination Sum
description: "Combination Sum"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Backtracking]
duoshuo: true
---
##题目
####Combination Sum
>Given a set of candidate numbers (**C**) and a target number (**T**), find all unique combinations in C where the candidate numbers sums to T.

>The **same** repeated number may be chosen from C unlimited number of times.

>####Note:
>1. All numbers (including target) will be positive integers.
2. Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
3. The solution set must not contain duplicate combinations.

>For example, given candidate set `2,3,6,7` and target `7`,
 
>A solution set is: 

>`[7]` 

>`[2, 2, 3]` 

<!-- more -->

##解题思路
该题是一个求解循环子问题的题目，采用递归进行深度优先搜索。基本思路是先排好序，然后每次递归中把剩下的元素一一加到结果集合中，并且把目标减去加入的元素，然后把剩下元素（包括当前加入的元素）放到下一层递归中解决子问题。算法复杂度因为是NP问题，所以自然是指数量级的。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
        if(candidates.length==0)
        	return res;
        Arrays.sort(candidates);
        helper(candidates,0,target,new ArrayList<Integer>(),res);
        return res;
    }

    public void helper(int[] candidates,int start,int target,ArrayList<Integer> cur,ArrayList<ArrayList<Integer>> res)
    {
    	if(target<0) //不满足条件
    		return;
    	if(target==0) //满足条件
    	{
    		res.add(new ArrayList<Integer>(cur)); //这边不能写成res.add(cur)，如果写成这样就是传递的是引用，会在后面改变cur的时候改变res
    		return;
    	}else{
    		for(int i=start;i<candidates.length;i++)
    		{
    			//去除重复解的问题,跳过重复出现的元素。
    			if(i!=start&&candidates[i]==candidates[i-1])
    				continue;
    			cur.add(candidates[i]);  //先加进来
    			helper(candidates,i,target-candidates[i],cur,res);  //返回的时候加进来求解的问题已经求完了
    			cur.remove(cur.size()-1); //然后在去除掉
    		}
    	}
    }
}
{% endhighlight %}

