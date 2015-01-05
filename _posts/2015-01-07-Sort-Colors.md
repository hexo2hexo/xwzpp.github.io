---
layout: post
title:  LeetCode-Sort Colors
description: "Sort Colors"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers,Sort]
duoshuo: true
---
##题目
####Sort Colors
>Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

>Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

>**Note**:   
>You are not suppose to use the library's sort function for this problem.

>**Follow up**:   
>A rather straight forward solution is a two-pass algorithm using counting sort.   
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

>Could you come up with an one-pass algorithm using only constant space?

<!-- more -->
	
##解题思路
该题是按颜色进行排序，由于有三种颜色，按红，白，蓝进行排序。如果我们知道每种颜色出现的次数，则最终的排序结果我们就知道了。因此这里可以采用**计数排序**。首先统计每个颜色的出现次数，然后按照颜色和出现次数对原数组`A`中的元素直接进行修改，最终的结果就是排好序的结果。这个方法遍历了两遍数组。见代码1

如果想使用常量的空间，则需要就地排序。这个题目其实我们很容易就能联想到快排的划分上来，但是仔细一想，如果按照划分来做达不到题目要求，比如你按照1来划分，一次划分的结果只能保证1后的元素都为2，但不能保证前面1和0之间的关系。
在此基础上可以继续拓展下，标准的划分是按照一个pivot来划分，这里我能不能指定2个pivot。假如指定2个pivot，一个是0，一个是2，那么分割后就有3段，一段是小于等于0，中间段大于0小于2，最后一段大于等于2。这个正好符合题意，也只需要遍历一次数组。见代码2

##算法代码
代码采用JAVA实现：
代码1：
{% highlight java %}
public class Solution {
    public void sortColors(int[] A) {
        //因为有三种颜色，可以采用计数排序
        int[] colors=new int[3];
        //每个颜色的出现次数        
        for(int i=0;i<A.length;i++)
        {
        	colors[A[i]]++;
        }
        //按颜色进行排序
       	int weizhi=0;
        for(int i=0;i<colors.length;i++)
        {
        	for(int j=0;j<colors[i];j++)
        	{
        		A[weizhi]=i;
        		weizhi++;
        	}
        }
    }
}
{% endhighlight %}

代码2：
{% highlight java %}
public class Solution {
    public void sortColors(int[] A) {
       int p0=0;
       int p2=A.length-1;
       int p=0;
       while(p<A.length && p<=p2 && p0<=p2)
       {
       		if(A[p]==0)
       		{
       			int tmp=A[p0];
       			A[p0]=A[p];
       			A[p]=tmp;
       			p0++;
       			p++;
       		}else if(A[p]==2)
       		{
       			int tmp=A[p2];
       			A[p2]=A[p];
       			A[p]=tmp;
       			p2--;
       		}else
       		{
       			p++;
       		}
       }
    }
}
{% endhighlight %}