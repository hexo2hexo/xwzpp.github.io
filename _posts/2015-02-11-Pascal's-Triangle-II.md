---
layout: post
title:  LeetCode-Pascal's Triangle II
description: "Pascal's Triangle II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Pascal's Triangle II
>Given an index k, return the kth row of the Pascal's triangle.

>For example, given k = 3,      
>Return [1,3,3,1].    

>####Note:    
>Could you optimize your algorithm to use only O(k) extra space?

<!-- more -->
	
##解题思路
这道题跟[Pascal's Triangle][1]很类似，只是这里只需要求出某一行的结果。[Pascal's Triangle][1]中因为是求出全部结果，所以我们需要上一行的数据就很自然的可以去取。而这里我们只需要一行数据，就得考虑一下是不是能只用一行的空间来存储结果而不需要额外的来存储上一行呢？这里确实是可以实现的。对于每一行我们知道如果从前往后扫，res[i]=res[i-1]+res[i]， res[i+1]=res[i]+res[i+1]，可以看到res[i]会被覆盖掉。所以这里采取的方法是从后往前扫，res[i]=res[i]+res[i-1]，res[i-1]=res[i-1]+res[i-2],我们需要的数据不会被覆盖，因为需要的res[i]只在当前步用，下一步就不需要了。这个技巧在动态规划省空间时也经常使用，主要就是看我们需要的数据是原来的数据还是新的数据来决定我们遍历的方向。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public ArrayList<Integer> getRow(int rowIndex) {
        ArrayList<Integer> res=new ArrayList<Integer>();
        if(rowIndex<0)
        	return res;
        res.add(1);
        for(int i=1;i<=rowIndex;i++)
        {
        	//从后往前进行求解
        	for(int j=res.size()-2;j>=0;j--)  
	        {  
	            res.set(j+1,res.get(j)+res.get(j+1));  
	        }  
	        res.add(1); 
        }
        return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Pascal's-Triangle.html









