---
layout: post
title:  LeetCode-The Skyline Problem
description: "The Skyline Problem"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Heap]
duoshuo: true
---
##题目
####The Skyline Problem
>A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are **given the locations and height of all the buildings** as shown on a cityscape photo (Figure A), write a program to **output the skyline** formed by these buildings collectively (Figure B).
![][1]
![][2]
>The geometric information of each building is represented by a triplet of integers `[Li, Ri, Hi]`, where `Li` and `Ri` are the x coordinates of the left and right edge of the ith building, respectively, and Hi is its height. It is guaranteed that `0 ≤ Li, Ri ≤ INT_MAX`, `0 < Hi ≤ INT_MAX`, and `Ri - Li > 0`. You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

>For instance, the dimensions of all buildings in Figure A are recorded as: `[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ] `.

>The output is a list of **"key points"** (red dots in Figure B) in the format of` [ [x1,y1], [x2, y2], [x3, y3], ... ] `that uniquely defines a skyline. **A key point is the left endpoint of a horizontal line segment**. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

>####Notes:
>
+ The number of buildings in any input list is guaranteed to be in the range `[0, 10000]`.
+ The input list is already sorted in ascending order by the left x position `Li`.
+ The output list must be sorted by the x position.
+ There must be no consecutive horizontal lines of equal height in the output skyline. For instance, `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` is not acceptable; the three lines of height 5 should be merged into one in the final output as such: `[...[2 3], [4 5], [12 7], ...]`

>####Credits:
>Special thanks to @stellari for adding this problem, creating these two awesome images and all test cases.

<!-- more -->
	
##解题思路
该题是一个求解SkyLine的问题，其实就是找到那些前后**高度变化**的关键点，在这里我也没有想到非常好的解，可以直接采用顺序遍历的方法求解。

首先定义个数组记录每个位置的skyline高度，然后顺序进入每栋楼，更新每个位置的skyline高度，最后再一次遍历这个数组，如果发现前后两个点的skyline高度发生了改变，则说明这个点就是关键点。 

但是这个有个问题，是开出的数组太大，里面最大的楼的右坐标位置为Integer.MAX_VALUE.因此会造成整个数组的越界。

**问题并未解决**

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
    	List<int[]> res=new ArrayList<int[]>();
        if(buildings==null || buildings.length==0) return res;

        //定义数组来记录每个x坐标位置的Skyline高度
        //这个高度应该是这个x位置的最大高度
        int R=0;
        for(int i=0;i<buildings.length;i++)
        {
        	R=Math.max(R,buildings[i][1]);
        }

        int[] skylineHeigh=new int[R];
        //记录全部楼中的最大的右左边
      	
        for(int i=0;i<buildings.length;i++)
        {
        	int l=buildings[i][0];
        	int r=buildings[i][1];
        	int h=buildings[i][2];
        	for(int j=l;j<=r;j++){
        		skylineHeigh[j]=Math.max(skylineHeigh[j],h);
        	}
        }

        //选取所有的关键点
        for(int i=1;i<=R;i++)
        {
        	if(skylineHeigh[i]!=skylineHeigh[i-1]){
        		int[] tmp={i,skylineHeigh[i]};
        		res.add(tmp);
        	}
        }

        return res;
    }
}
{% endhighlight %}

[1]:img/The Skyline Problem/1.png
[2]:img/The Skyline Problem/2.png

















