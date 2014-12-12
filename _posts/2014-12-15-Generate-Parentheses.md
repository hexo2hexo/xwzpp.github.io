---
layout: post
title:  LeetCode-Generate Parentheses
description: "Generate Parentheses"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking,String]
duoshuo: true
---
##题目
####Generate Parentheses
>Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

>For example, given n = 3, a solution set is:

>`"((()))", "(()())", "(())()", "()(())", "()()()"`

<!-- more -->

##解题思路
一般来说是用递归的方法，因为可以归结为子问题去操作。在每次递归函数中记录左括号和右括号的剩余数量，然后有两种选择，一个是放一个左括号，另一种是放一个右括号。当然有一些否定条件，比如剩余的右括号不能比左括号少，或者左括号右括号数量都要大于0。正常结束条件是左右括号数量都为0。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//采用递归求解
    public ArrayList<String> generateParenthesis(int n) {
        ArrayList<String> lists=new ArrayList<String>();
    	if(n<=0) return lists;
    	helper(n,n,new String(),lists);
    	return lists;
    }
    
    public void helper(int l,int r,String term,ArrayList<String> lists)
    {
        if(l>r)
            return;
        if(l==0&&r==0)
            lists.add(term);
        if(l>0)
            helper(l-1,r,term+"(",lists);
        if(r>0)
            helper(l,r-1,term+")",lists);          
    }
}
{% endhighlight %}
