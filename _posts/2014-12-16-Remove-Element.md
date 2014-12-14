---
layout: post
title:  LeetCode-Remove Element
description: "Remove Element"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####Remove Element
>Given an array and a value, remove all instances of that value in place and return the new length.

>The order of elements can be changed. It doesn't matter what you leave beyond the new length.

<!-- more -->

##解题思路
该题是移除数组中给定的元素。这里可以设定两个指针`i`和`j`,如果`A[j]`不是要删除的元素，则`A[i]=A[j]`,否则`j`往前移动。这样`j`指针相当于遍历整个数组，而`i`指针则负责保存剩余的元素。这样只需要遍历一遍数组即可。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    //采用两个指针，一次遍历即可
    public int removeElement(int[] A, int elem) {
 		if(A.length<=0) return 0;
 		int i=0,j=0;
 		while(j<A.length)
 		{
 			if(A[j]!=elem)
	 		{
	 			A[i]=A[j];
	 			i++;
	 			j++;
	 		}else{
	 			j++;
	 		}
 		}
 		return i; 		
    }
}
{% endhighlight %}
