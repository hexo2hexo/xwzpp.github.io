---
layout: post
title:  LeetCode-Permutations 
description: "Permutations"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking]
duoshuo: true
---
##题目
####Permutations
>Given a collection of numbers, return all possible permutations.

>For example,

>`[1,2,3]` have the following permutations:

>`[1,2,3]`, `[1,3,2]`, `[2,1,3]`, `[2,3,1]`, `[3,1,2]`, and `[3,2,1]`.

<!-- more -->
	
##解题思路
该题可以采用递归的思想，求解循环子问题。区别是这里并不是一直往后推进的，前面的数有可能放到后面，所以我们需要维护一个used数组来表示该元素是否已经在当前结果中，因为每次我们取一个元素放入结果，然后递归剩下的元素，所以不会出现重复。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> permute(int[] num) {
    	ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
   		if(num==null || num.length==0)
   			return res;
        int[] used=new int[num.length];
        for(int i=0;i<num.length;i++)
        	used[i]=0;
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

