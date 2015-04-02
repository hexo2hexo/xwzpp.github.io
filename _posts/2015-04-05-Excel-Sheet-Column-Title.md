---
layout: post
title:  LeetCode-Excel Sheet Column Title
description: "Excel Sheet Column Title"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math]
duoshuo: true
---
##题目
####Excel Sheet Column Title
>Given a positive integer, return its corresponding column title as appear in an Excel sheet.

>For example:
>
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
>####Credits:
>Special thanks to @ifanchu for adding this problem and creating all test cases..

<!-- more -->
	
##解题思路
该题每次对数字进行26取模，就能能到其尾数是哪一个字母，然后得到的余数如果大于26，则继续循环处理，否则就在结果的前端插入字母下标位置为余数的字母。
##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String convertToTitle(int n) {
        if(n<=0)
        	return "";
        //定义个hashmap存放26个字母及其对应的数字 ,A-0,B-1,....,Z-25
        HashMap<Integer,Character> map=new HashMap<Integer,Character>();
        char ch='A';
        map.put(0,ch);
        for(int i=1;i<26;i++)
        {
        	ch+=1;
        	map.put(i,ch);
        }
        StringBuilder res=new StringBuilder();
        while(n>26)
        {	
			//每次取模进行处理，并将结果插入到StringBuilder的前端。
        	int shang=(n-1)%26;
        	res.insert(0,map.get(shang));
        	n=(n-1)/26;
        }
        res.insert(0,map.get(n-1));
        return res.toString();       	
    }
}
{% endhighlight %}





