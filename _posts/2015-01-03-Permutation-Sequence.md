---
layout: post
title:  LeetCode-Permutation Sequence
description: "Permutation Sequence"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking,Math]
duoshuo: true
---
##题目
####Permutation Sequence
>The set `[1,2,3,…,n]` contains a total of n! unique permutations.

>By listing and labeling all of the permutations in order,   
>We get the following sequence (ie, for n = 3):
>
1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

>Given n and k, return the kth permutation sequence.

>**Note**: Given n will be between 1 and 9 inclusive.

<!-- more -->
	
##解题思路
该题可以发现如下规律，如果元素个数为`n`,则相同的其实元素会有`(n-1)!`种可能，也就是`(n-1)!`排列后会换一个起始元素，因此只要当前的`k`进行`(n-1)!`取余，得到的数字就是当前剩余数组的`index`，如此就可以得到对应的元素。如此递推直到数组中没有元素结束。实现中我们要维护一个数组来记录当前的元素，每次得到一个元素加入结果数组，然后从剩余数组中移除。

这里一开始把`k--`，目的是让下标从`0`开始，这样下标就是从`0`到`n-1`，不用考虑`n`时去取余，更好地跟数组下标匹配。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder res=new StringBuilder();
        if(n<0)
        	return "";
        ArrayList<Integer> list=new ArrayList<Integer>(); //n个元素的列表
        for(int i=0;i<n;i++)
        {
        	list.add(i+1);
        }
        int fac=1;
        for(int i=2;i<n;i++)
        	fac*=i;                //计算(n-1)!
        k--;                   //首先将k-1作为小标 这样与下边从0开始进行对应
        for(int i=n-1;i>=0;i--)
        {
        	int index=k/fac;
        	k%=fac;
        	res.append(list.get(index));
        	list.remove(index);
        	if(i>0)
        		fac/=i;

        }
        return res.toString();
    }
}
{% endhighlight %}

