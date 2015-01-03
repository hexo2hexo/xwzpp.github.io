---
layout: post
title:  LeetCode-Valid Number
description: "Valid Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math,String]
duoshuo: true
---
##题目
####Valid Number
>Validate if a given string is numeric.

>Some examples:   
>`"0"` => `true`  
>`" 0.1 "` => `true`  
>`"abc"` => `false`   
>`"1 a"` => `false`   
>`"2e10"` => `true`   

>**Note**: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

>Update (2014-12-06):    
>New test cases had been added. Thanks unfounder's contribution.

<!-- more -->
	
##解题思路
基本规则是按照科学计数法，所以会出现的特殊字符有以下几个：符号位‘+’，‘-’，小数点‘.’，还有‘e’和‘E’，剩下的就只有数字0-9了，其他字符如果出现就是非法字符，返回false。数字字符在哪里出现都是ok的，我们主要考虑几个特殊字符的情况。

对于小数点出现的时候，我们要满足一下这些条件：   
（1）前面不能有小数点或者‘e’和‘E’；    
（2）前一位是数字（不能是第一位）或者后一位要是数字（不能是最后一位）。    

对于正负号出现的情况，要满足条件：    
（1）必须是第一位或者在‘e’和‘E’后一位；    
（2）后一位要是数字。    

对于‘e’和‘E’的情况，要满足：    
（1）前面不能有‘e’和‘E’出现过；    
（2）不能是第一位（前面没数字科学计数没有意义）或者最后一位（后面没数字就不用写指数了）。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean isNumber(String s) {
	    if(s==null)
	        return false;
	    s = s.trim();
	    if(s.length()==0)
	        return false;
	    boolean dotFlag = false;
	    boolean eFlag = false;
	    for(int i=0;i<s.length();i++)
	    {
	        switch(s.charAt(i))
	        {
	            case '.':
	                if(dotFlag || eFlag 
	                || ((i==0||!(s.charAt(i-1)>='0'&&s.charAt(i-1)<='9')) 
	                    && (i==s.length()-1||!(s.charAt(i+1)>='0'&&s.charAt(i+1)<='9'))))
	                    return false;
	                dotFlag = true;
	                break;
	            case '+':
	            case '-':
	                if((i>0 && (s.charAt(i-1)!='e' && s.charAt(i-1)!='E'))
	                  || (i==s.length()-1 || !(s.charAt(i+1)>='0'&&s.charAt(i+1)<='9'||s.charAt(i+1)=='.')))
	                    return false;
	                break;
	            case 'e':
	            case 'E':
	                if(eFlag || i==s.length()-1 || i==0)
	                    return false;
	                eFlag = true;
	                break;
	            case '0':
	            case '1':
	            case '2':
	            case '3':
	            case '4':
	            case '5':
	            case '6':
	            case '7':
	            case '8':
	            case '9':
	                break;
	            default:
	                return false;
	        }
	    }
	    return true;
	}
}
{% endhighlight %}

