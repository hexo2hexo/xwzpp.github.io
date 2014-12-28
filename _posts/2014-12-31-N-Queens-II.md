---
layout: post
title:  LeetCode-N-Queens II
description: "N-Queens II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking]
duoshuo: true
---
##题目
####N-Queens II
>Follow up for N-Queens problem.

>Now, instead outputting board configurations, return the total number of distinct solutions.

![][1]

<!-- more -->
	
##解题思路
该题和[N-Queens][2]基本相同，只是最后返回的是解得个数。但是这里需要注意的是:用java写的时候，基本数据类型是**值传递**，因此不能用`int`来作为递归的结果参数。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int totalNQueens(int n) {
        ArrayList<Integer> res = new ArrayList<Integer>(); //这里不能用int类型
        res.add(0);
        helper(n,0,new int[n],res);
        return res.get(0);
    }
    //columnForRow 记录每一行中皇后的位置
    void helper(int n,int row,int[] columnForRow, ArrayList<Integer> res) 
    {	
    	if(row==n)
    	{
    		int num=res.get(0)+1;
    		res.set(0,num);
    		return;
    	}else{
    		for(int i=0;i<n;i++)
    		{
    			columnForRow[row]=i;
    			if(check(row,columnForRow))
		        {
		            helper(n,row+1,columnForRow,res);
		        }
    		}
    	}
    }

    boolean check(int row,int[] columnForRow)
    {
    	for(int i=0;i<row;i++)
    	{
    		if(columnForRow[row]==columnForRow[i] || Math.abs(columnForRow[row]-columnForRow[i])==(row-i))
    			return false;
    	}
    	return true;
    }
}
{% endhighlight %}

[1]:/img/N-Queens/1.png
[2]:http://pisxw.com/algorithm/N-Queens.html