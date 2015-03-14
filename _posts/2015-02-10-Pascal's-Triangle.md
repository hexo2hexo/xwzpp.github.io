---
layout: post
title:  LeetCode-Pascal's Triangle
description: "Pascal's Triangle"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Pascal's Triangle
>Given numRows, generate the first numRows of Pascal's triangle.

>For example, given numRows = 5,     
>Return

	[
	     [1],
	    [1,1],
	   [1,2,1],
	  [1,3,3,1],
	 [1,4,6,4,1]
	]

<!-- more -->
	
##解题思路
该题主要是生成帕斯卡三角形。该题通过找规律可以发现，每一行的首位和末尾都为1，从第二位到第length()-1位，其第i位等于上一层的第i-1位与第i位的和。通过不断顺序生成每一行的数据即可求出结果。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> generate(int numRows) {
        ArrayList<ArrayList<Integer>> res=new ArrayList<ArrayList<Integer>>();
        if(numRows==0)
        	return res;
        //首先需要放入1
        ArrayList<Integer> first=new ArrayList<Integer>();
        first.add(1);
       	res.add(first);
       	if(numRows==1);
       		return res;
        ArrayList<Integer> cur=null;
        //如果行数大于1，则从第二行开始计算
        for(int i=1;i<=numRows-1;i++)
        {
        	//第一位为1
        	cur=new ArrayList<Integer>();
        	cur.add(1);
        	//计算中间位置的值
        	for(int j=1;j<=i-1;j++)
        	{
        		cur.add(res.get(i-1).get(j-1)+res.get(i-1).get(j));
        	}
        	//最后一位为1
        	cur.add(1);
        	res.add(new ArrayList<Integer>(cur));
        }
        return res;
    }
}
{% endhighlight %}









