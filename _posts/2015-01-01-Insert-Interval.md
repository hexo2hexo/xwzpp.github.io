---
layout: post
title:  LeetCode-Insert Interval
description: "Insert Interval"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Sort]
duoshuo: true
---
##题目
####Insert Interval
>Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

>You may assume that the intervals were initially sorted according to their start times.

>####Example 1:
>Given intervals `[1,3],[6,9]`, insert and merge `[2,5]` in as `[1,5],[6,9]`.

>####Example 2:
>Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.

>This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.

<!-- more -->
	
##解题思路
该题与[Merge Intervals][1]类似，只不过合并是该题的一个子过程，这里首先需要考虑新时间段插入的位置，然后对插入之后，判断其插入是否会产生重叠。

这里的重叠问题有两个情况：

	1. 插入位置前面一个元素与插入的元素产生重叠，这时合并后仍需考虑插入位置后面的元素重叠问题
	2. 插入位置前面一个元素与插入的元素不会产生重叠，这时直接插入，但是需考虑插入位置后面的元素重叠问题

这里需要注意两个细节处理，插入位置为**初始位置**和**最后一个位置**.

##算法代码
代码采用JAVA实现：
{% highlight java %}
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList<Interval> res=new ArrayList<Interval>();
        if(intervals==null || intervals.size()==0)
        {
        	res.add(newInterval);
        	return res;
        }
        int i=0;
        for(;i<intervals.size();i++)
        {
        	if(intervals.get(i).start<=newInterval.start)
        	{
        		res.add(intervals.get(i));
        	}else{
        		//找到newInterval的插入位置，然后判断其前面一个元素是否有重叠
        		if(res.size()!=0 && newInterval.start<=res.get(res.size()-1).end)
	        	{
	        		int start=res.get(res.size()-1).start;
	        		int end=Math.max(res.get(res.size()-1).end,newInterval.end);
	        		res.remove(res.size()-1);
	        		res.add(new Interval(start,end));
	        	}else
	        	{
	        		res.add(newInterval);
	        	}
	        	//插入之后，对插入位置后面的元素判断是否会产生重叠
	        	for(int j=i;j<intervals.size();j++)
		        {
		        	if(intervals.get(j).start<=res.get(res.size()-1).end)
		        	{
		        		int start=res.get(res.size()-1).start;
		        		int end=Math.max(res.get(res.size()-1).end,intervals.get(j).end);
		        		res.remove(res.size()-1);
		        		res.add(new Interval(start,end));
		        	}else{
		        		res.add(intervals.get(j));
		        	}
		        }
		        break;
        	}
        }
        //当插入位置是在最后时，只需判断插入位置前一个元素是否与newInterval产生重叠
        if(i==intervals.size())
        {
        	if(newInterval.start<=res.get(res.size()-1).end)
        	{
        		int start=res.get(res.size()-1).start;
        		int end=Math.max(res.get(res.size()-1).end,newInterval.end);
        		res.remove(res.size()-1);
        		res.add(new Interval(start,end));
        	}else
        	{
        		res.add(newInterval);
        	}
        }
        return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Merge-Intervals.html