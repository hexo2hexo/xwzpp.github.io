---
layout: post
title:  LeetCode-Max Points on a Line
description: "Max Points on a Line"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Math]
duoshuo: true
---
##题目
####Max Points on a Line
>Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.
>
<!-- more -->
	
##解题思路
基本思路是这样的， 每次迭代以某一个点为基准， 看后面每一个点跟它构成的直线， 维护一个HashMap， key是跟这个点构成直线的斜率的值， 而value就是该斜率对应的点的数量， 计算它的斜率， 如果已经存在， 那么就多添加一个点， 否则创建新的key。 这里只需要考虑斜率而不用考虑截距是因为所有点都是对应于一个参考点构成的直线， 只要斜率相同就必然在同一直线上。 最后取map中最大的值， 就是通过这个点的所有直线上最多的点的数量。 对于每一个点都做一次这种计算， 并且后面的点不需要看扫描过的点的情况了， 因为如果这条直线是包含最多点的直线并且包含前面的点， 那么前面的点肯定统计过这条直线了。 因此算法总共需要两层循环， 外层进行点的迭代， 内层扫描剩下的点进行统计

##算法代码
代码采用JAVA实现：
{% highlight java %}
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
    public int maxPoints(Point[] points) {
        if(points==null || points.length==0)
        	return 0;
       //对每个节点维护一个HashMap,其中key为斜率，value为在这个斜率上的点数
        int max=1;
        for(int i=0;i<points.length-1;i++)
        {
        	HashMap<Double,Integer> map=new HashMap<Double,Integer>();
        	int samenum=0;//定义相同的节点数
        	int localmax=1;
        	for(int j=i+1;j<points.length;j++)
        	{
        		double rado=0.0;
        		//如果遇到相同的节点，此时需要记录
        		if(points[i].x==points[j].x && points[i].y==points[j].y)
        		{	
        			samenum++;
        			continue;
        		}
        		else if(points[i].x==points[j].x)
        		{
        			rado=(double)Integer.MAX_VALUE;
        		}else if(points[i].y==points[j].y)
        		{
        			rado=0.0;
        		}else{
        			rado=(double)(points[j].y-points[i].y)/(points[j].x-points[i].x);
        		}

        		if(map.containsKey(rado))
        		{
        			map.put(rado,map.get(rado)+1);
        		}else
        		{
        			map.put(rado,2);  //包含源节点
        		}
        	}

    		for(Integer value:map.values())
    		{
    			localmax=Math.max(localmax,value);
    		}
    		localmax+=samenum;
  			max=Math.max(max,localmax);
        }
        return max;
    }
}
{% endhighlight %}






