---
layout: post
title:  LeetCode-Integer to Roman
description: "Integer to Roman"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math,String]
duoshuo: true
---
##题目
####Integer to Roman

>Given an integer, convert it to a roman numeral.

>Input is guaranteed to be within the range from 1 to 3999.

<!-- more -->

##解题思路
该题是将整数变为罗马数字，主要考虑的是字符串操作。需要注意的数字和罗马数字的对应关系。
	
	罗马数字为以下表示形式：
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
	
##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
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
    public String intToRoman(int num) {
        if(num<0||num>3999) return "";
        int dev=1000;
        ArrayList<Integer> list=new ArrayList<Integer>();
        while(dev>0)
        {
        	list.add(num/dev);
        	num=num%dev;
        	dev=dev/10;
        }
        //从千位开始，对每一位进行转换，但是每一位对应的罗马数字也有范围
        String result="";
        result+=convert(list.get(0),'M',' ',' ');
        result+=convert(list.get(1),'C','D','M');
        result+=convert(list.get(2),'X','L','C');
        result+=convert(list.get(3),'I','V','X');
        return result;

    }

    public String convert(int num,char c1,char c5,char c10)
    {
    	String s="";
    	switch(num)
    	{
    		case 9:{s+=c1;s+=c10;break;}
    		case 8:{s+=c5;s+=c1;s+=c1;s+=c1;break;}
    		case 7:{s+=c5;s+=c1;s+=c1;break;}
    		case 6:{s+=c5;s+=c1;break;}
    		case 5:{s+=c5;break;}
    		case 4:{s+=c1;s+=c5;break;}
    		case 3:{s+=c1;s+=c1;s+=c1;break;}
    		case 2:{s+=c1;s+=c1;break;}
    		case 1:{s+=c1;break;}
    		default:break;
    	}
    	return s;
    }
}
{% endhighlight %}

