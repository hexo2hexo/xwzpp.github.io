---
layout: post
title:  LeetCode-Merge Intervals
description: "Merge Intervals"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Sort]
duoshuo: true
---
##题目
####Merge Intervals
>Given a collection of intervals, merge all overlapping intervals.

>For example,   
>Given `[1,3],[2,6],[8,10],[15,18]`,   
>return `[1,6],[8,10],[15,18]`.

<!-- more -->
	
##解题思路
该题是合并重叠的时间区间，首先先按照`start`时间进行排序，然后遍历，如果一个时间段的`start`时间小于上一时间段的`end`时间（这里是上一时间段，因为已经按照`start`时间进行排序了），则合并两个时间段，`end`时间为两个时间段`end`中最大的那个。

下面举一个例子：

	定义t1=[start1,end1],t2=[start2,end2]
	按start排序后，使得start1<=start2

	如果start2<end2,则进行合并得到t3=[start1,max(end1,end2)]
	否则则不需要合并。
	

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
    public ArrayList<Interval> merge(ArrayList<Interval> intervals) {
    	ArrayList<Interval> res=new ArrayList<Interval>();
        if(intervals==null || intervals.size()==0)
        	return res;
        //对interval以start进行排序
        Collections.sort(intervals, new Comparator() {
	      public int compare(Object o1, Object o2) {
	          Interval in1=(Interval)o1;
	          Interval in2=(Interval)o2;
	          if(in1.start>in2.start)
	                return 1;
	          else{
	          	if(in1.start==in2.start)
	                    return 0;
	               else
	                    return -1;
	          }
	      }
   		});

		//遍历进行合并判断
        res.add(intervals.get(0));
        for(int i=1;i<intervals.size();i++)
        {
        	if(intervals.get(i).start<=res.get(res.size()-1).end)
        	{
        		int start=res.get(res.size()-1).start;
        		int end=Math.max(res.get(res.size()-1).end,intervals.get(i).end);
        		res.remove(res.size()-1);
        		res.add(new Interval(start,end));
        	}else{
        		res.add(intervals.get(i));
        	}
        }
        return res;
    }
}
{% endhighlight %}
