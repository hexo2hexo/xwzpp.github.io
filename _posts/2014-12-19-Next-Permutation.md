---
layout: post
title:  LeetCode-Next Permutation
description: "Next Permutation"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Arrays]
duoshuo: true
---
##题目
####Next Permutation 
>Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

>If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

>The replacement must be in-place, do not allocate extra memory.

>Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
>
	1,2,3 → 1,3,2
	3,2,1 → 1,2,3
	1,1,5 → 1,5,1

<!-- more -->

##解题思路
该题是找下一个排列的问题。该题需要知道如何进行变换。下面我们用一个例子进行说明：

	比如排列是(2,3,6,5,4,1)。
	求下一个排列的基本步骤是这样：
		1) 先从后往前找到第一个不是依次增长的数，记录下位置p。比如例子中的3，对应的位置是1;
		2) 接下来分两种情况：
    		(1) 如果上面的数字都是依次增长的，那么说明这是最后一个排列，下一个就是第一个，其实把所有数字反转过来即可(比如(6,5,4,3,2,1)下一个是(1,2,3,4,5,6));
  			(2) 否则，如果p存在，从p开始往后找，找到下一个数就比p对应的数小的数字，然后两个调换位置，比如例子中的4。调换位置后得到(2,4,6,5,3,1)。最后把p之后的所有数字倒序，比如例子中得到(2,4,1,3,5,6), 这个即是要求的下一个排列。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public void nextPermutation(int[] num) {
        int len=num.length;
        if(len<=1) return;
        int p=-1;
        for(int i=len-2;i>=0;i--)
        {
        	if(num[i]<num[i+1])
        	{
        		p=i;  //找到p位置
        		int j=p+1;
        		for(;j<len;j++)
        		{
        			if(num[j]<=num[p])
        			{
        				break;
        			}
        		}
        		int temp=num[p];
				num[p]=num[j-1];
				num[j-1]=temp;
				reverse(num,p+1);
				return;
        	}
        }
        reverse(num,0);
        return;     	
    }

    public void reverse(int[] num,int index)
    {
    	int s=index;
    	int e=num.length-1;
    	while(s<e)
    	{
    		int temp=num[s];
    		num[s]=num[e];
    		num[e]=temp;
    		s++;
    		e--;
    	}
    	return;
    }
}
{% endhighlight %}
