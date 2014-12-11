---
layout: post
title:  LeetCode-Roman to Integer
description: "Roman to Integer"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math，String]
duoshuo: true
---
##题目
####Roman to Integer

>Given a roman numeral, convert it to an integer.

>Input is guaranteed to be within the range from 1 to 3999.

<!-- more -->

##解题思路
该题是将罗马数字转化为整数，与[Integer to Roman][1]的解法比较类似，都是字符串的处理问题，只需要知道罗马数字和整数之间的对应关系即可。

	罗马数字为以下表示形式：
	  I 1
	  V 5
	  X 10
	  L 50
	  C 100
	  D 500
	  M 1,000
	
	  罗马数字对于每个位有三个单位：1,5,10，对于1到9，表示方法如下：
	  1-3：用1表示；
	  4: 5左边加一个1；
	  5： 直接用5表示； 
	  6-8: 5右边加相应的1；
	  9： 10左边加一个1。

其中需要注意的是：如果1下一个字符是对应位的5或者10，则减去该位的1（例如4，9），否则加之。遇到5或者10就直接加上对应位的5或者10

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    //就是维护一个整数，然后如果1下一个字符是对应位的5或者10则减对应位的1，否则加之。遇到5或者10就直接加上对应位的5或者10
    /*
	  I	1
      V	5
      X	10
      L	50
      C	100
      D	500
      M	1,000

      罗马数字对于每个位有三个单位：1,5,10，对于1到9，表示方法如下：
	  1-3：用1表示；
	  4: 5左边加一个1；
	  5： 直接用5表示； 
	  6-8: 5右边加相应的1；
	  9： 10左边加一个1。
	*/
    public int romanToInt(String s) {
        int num=0;
        char[] c=s.toCharArray();
        if(c.length==0) return 0;
        for(int i=0;i<c.length;i++)
        {
        	switch(c[i])
        	{
        		case 'I':{
        			if((i<c.length-1)&&(c[i+1]=='V'||c[i+1]=='X'))
        				num-=1;
        			else
        				num+=1;
        			break;
        		}
        		case 'V':{num+=5;break;}
        		case 'X':{
        			if((i<c.length-1)&&(c[i+1]=='L'||c[i+1]=='C'))
        				num-=10;
        			else
        				num+=10;
        			break;
        		}
        		case 'L':{num+=50;break;}
        		case 'C':{
        			if((i<c.length-1)&&(c[i+1]=='D'||c[i+1]=='M'))
        				num-=100;
        			else
        				num+=100;
        			break;
        		}
        		case 'D':{num+=500;break;}
        		case 'M':{num+=1000;break;}
        		default:break;
        	}
        }
        return num;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/leetcode-Integer-to-Roman.html