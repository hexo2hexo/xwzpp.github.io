---
layout: post
title:  LeetCode-Longest Valid Parentheses
description: "Longest Valid Parentheses"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,String]
duoshuo: true
---
##题目
####Longest Valid Parentheses 
>Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

>For `"(()"`, the longest valid parentheses substring is `"()"`, which has length = 2.

>Another example is `")()())"`, where the longest valid parentheses substring is `"()()"`, which has length = 4.

<!-- more -->

##解题思路
这道题是求最长的括号序列，比较容易想到用栈这个数据结构。   
基本思路就是维护一个栈，遇到左括号就进栈，遇到右括号则出栈，并且判断当前合法序列是否为最长序列。不过这道题看似思路简单，但是有许多比较刁钻的测试集。具体来说，主要问题就是遇到右括号时如何判断当前的合法序列的长度。 
 
	比较健壮的方式如下：
	(1) 如果当前栈为空，则说明加上当前右括号没有合法序列（有也是之前判断过的）；
	(2) 否则弹出栈顶元素，如果弹出后栈为空，则说明当前括号匹配，我们会维护一个合法开始的起点start，合法序列的长度即为当前元素的位置-start+1；否则如果栈内仍有元素，则当前合法序列的长度为当前栈顶元素的位置下一位到当前元素的距离，因为栈顶元素后面的括号对肯定是合法的，而且左括号出过栈了。

因为只需要一遍扫描，算法的时间复杂度是O(n)，空间复杂度是栈的空间，最坏情况是都是左括号，所以是O(n)。

当然使用DP也可以解答，不过时间复杂度略高，解题如下：

	用longestValid[i][j]表示从S串中的字符i到j的最长well-formed表达式的长度；isValid[i][j]表示从i到j是否是一个valid的表达式。
	如何判断longestValid[i][j]的取值呢？有下面几种情况：
	假定有一个maxlength变量。
	1. 如果i='(' 并且 j=')'，
		a. 如果j = i+1,那这是一个valid的表达式；
      	b. 如果isValid[i+1][j-1]为真，那这也是一个valid表达式；
		c. 对所有在i到j之间的k，如果isValid[i,k]&&isValid[k+1,j]为真，那么这是一个valid表达式，这三种情况maxlength都是i到j的距离；
		d.其他情况，maxlength = longestValid[i][j-1]和 longestValid[i+1][j]比较大的那个。
	2. 如果i='(' 并且 j='(', maxlength等于longestValid[i][j-1]。
	3. 如果i=')' 并且 j=')', maxlength等于longestValid[i+1][j]。
	4. 如果i=')‘ 并且 j='(', maxlength等于longestValid[i+1][j-1].
	判断完成后，longestValid[i][j]赋值于maxlength。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int longestValidParentheses(String s) {
        char[] c=s.toCharArray();
        int start=0;
        int max=0;
        LinkedList<Integer> stack=new LinkedList<Integer>();
        for(int i=0;i<c.length;i++)
        {
        	if(c[i]=='(')
        	{
        		stack.push(i);
        	}else
        	{
        		if(stack.size()==0)
        			start=i+1;
        		else{
        			stack.pop();
        			max=stack.size()==0?Math.max(max,i-start+1):Math.max(max,i-stack.peek());
        		}
        	}
        }
        return max;
    }
}
{% endhighlight %}
