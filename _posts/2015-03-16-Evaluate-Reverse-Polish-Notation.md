---
layout: post
title:  LeetCode-Evaluate Reverse Polish Notation
description: "Evaluate Reverse Polish Notation"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,stack]
duoshuo: true
---
##题目
####Evaluate Reverse Polish Notation
>Evaluate the value of an arithmetic expression in Reverse Polish Notation.

>Valid operators are `+`, `-`, `*`, `/`. Each operand may be an integer or another expression.

>Some examples:
>
	  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
	  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6

<!-- more -->
	
##解题思路
该题是给出表达式的后序表示，然后对其进行求值。我们可以使用一个栈来进行维护，当遇到数字时则入栈，当遇到操作符的时候，则弹出栈顶的两个元素，进行表达式运算，然后将结果压入栈中，最终栈中的元素即为最后表达式的结果。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int evalRPN(String[] tokens) {
        if(tokens==null || tokens.length==0)
        	return 0;
        LinkedList<String> stack=new LinkedList<String>();
        for(int i=0;i<tokens.length;i++)
        {
        	switch(tokens[i])
        	{
        		case "+":
        		{
        			int a=Integer.parseInt(stack.pop());
        			int b=Integer.parseInt(stack.pop());
        			int c=a+b;
        			stack.push(c+"");
        			break;
        		}
        		case "-":
        		{
        			int a=Integer.parseInt(stack.pop());
        			int b=Integer.parseInt(stack.pop());
        			int c=b-a;
        			stack.push(c+"");
        			break;
        		}
        		case "*":
        		{

        			int a=Integer.parseInt(stack.pop());
        			int b=Integer.parseInt(stack.pop());
        			int c=a*b;
        			stack.push(c+"");
        			break;
        		}
        		case "/":
        		{
        			int a=Integer.parseInt(stack.pop());
        			int b=Integer.parseInt(stack.pop());
        			int c=b/a;
        			stack.push(c+"");
        			break;
        		}
        		default:{
        			stack.push(tokens[i]);
        		}
        	}
        }
        return Integer.parseInt(stack.pop());
    }
}
{% endhighlight %}






