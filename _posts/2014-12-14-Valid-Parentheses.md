---
layout: post
title:  LeetCode-Valid Parentheses
description: "Valid Parentheses"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Stack,String]
duoshuo: true
---
##题目
####RValid Parentheses
>Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

>The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

<!-- more -->

##解题思路
该题是匹配括号是否匹配合法问题，可以采用栈来实现，而栈一般采用数组来进行标示。如果遇到字符`(`,`{`和`[`，则将其压入栈中，如果遇到`)`,`}`和`]`，则需要对栈顶元素进行判定，看是否与括号相匹配，如果匹配则弹出栈顶元素，否则则认为匹配不合法，直接结束匹配过程。

算法流程如下：

	定义数组栈stack;
	foreach c in String:
		if c 为（，{，[  then stack.push(c);
		if c 为 ), }, ]	then 判定stack是否为空和stack.top是否与c相匹配。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//利用数组栈来求解问题
    public boolean isValid(String s) {
        char[] c=s.toCharArray();
        int len=c.length;
        char[] temp=new char[len];  //数组栈
        if(len<=1)
        	return false;
        int i=-1,j=0;
        while(j<len){
        	switch(c[j]){
        		case '[':
        		case '{':
        		case '(':{i++;temp[i]=c[j];j++;break;}
        		case ']':{
        			if(i!=-1&&temp[i]=='['){
        				i--;
        				j++;
        				break;
        			}else
        				return false;
        		}
        		case '}':{
        			if(i!=-1&&temp[i]=='{'){
        				i--;
        				j++;
        				break;
        			}else
        				return false;
        		}
        		case ')':{
					if(i!=-1&&temp[i]=='('){
						i--;
						j++;
						break;
					}else
						return false;
				}
        	}
        }
        if(i==-1)
        	return true;
        else
        	return false;
    }
}
{% endhighlight %}
