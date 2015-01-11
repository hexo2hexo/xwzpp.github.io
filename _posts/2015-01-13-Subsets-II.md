---
layout: post
title:  LeetCode-Subsets II
description: "Subsets II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Backtracking]
duoshuo: true
---
##题目
####Subsets II
>Given a collection of integers that might contain duplicates, S, return all possible subsets.

>**Note**:
>    
+ Elements in a subset must be in non-descending order.    
+ The solution set must not contain duplicate subsets.  
 
>For example,    
>If **S** = `[1,2,2]`, a solution is:
>
	[
	  [2],
	  [1],
	  [1,2,2],
	  [2,2],
	  [1,2],
	  []
	]

<!-- more -->
	
##解题思路
这道题跟[Subsets][1]一样是经典的`NP`问题--求子集。比[Subsets][1]稍微复杂一些的是这里的集合中可能出现重复元素，因此我们在求子集的时候要避免出现重复的子集。在[Subsets][1]中我们每次加进一个元素就会把原来的子集都加上这个元素，然后再加入到结果集中，但是这样重复的元素就会产生重复的子集。为了避免这样的重复，需要用个小技巧。

其实比较简单，就是每当遇到重复元素的时候我们就只把当前结果集的后半部分加上当前元素加入到结果集中，因为后半部分就是上一步中加入这个元素的所有子集，上一步这个元素已经加入过了，前半部分如果再加就会出现重复。所以算法上复杂度上没有提高，反而少了一些操作，就是遇到重复时少做一半，不过这里要对元素集合先排序，否则不好判断重复元素。同样的还是可以用递归和非递归来解，不过对于重复元素的处理是一样的。

##算法代码
代码采用JAVA实现：     
{% highlight java %}
public class Solution {
   public ArrayList<ArrayList<Integer>> subsetsWithDup(int[] num) {  
        if(num == null)  
            return null;  
        Arrays.sort(num);  
        ArrayList<Integer> lastSize = new ArrayList<Integer>();  
        lastSize.add(0);  
        return helper(num, num.length-1, lastSize);  
    }  
    private ArrayList<ArrayList<Integer>> helper(int[] num, int index, ArrayList<Integer> lastSize)  
    {  
        if(index == -1)  
        {  
            ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();  
            ArrayList<Integer> elem = new ArrayList<Integer>();  
            res.add(elem);  
            return res;  
        }  
        ArrayList<ArrayList<Integer>> res = helper(num,index-1,lastSize);  
        int size = res.size();  
        int start = 0;  
        if(index>0 && num[index]==num[index-1])  
            start = lastSize.get(0);  
        for(int i=start;i<size;i++)  
        {  
            ArrayList<Integer> elem = new ArrayList<Integer>(res.get(i));  
            elem.add(num[index]);  
            res.add(elem);  
        }  
        lastSize.set(0,size);  
        return res;  
    }  
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Subsets.html




