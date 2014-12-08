---
layout: post
title:  LeetCode-ZigZag Conversion
description: "ZigZag Conversion"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####ZigZag Conversion CentOS

>The string `PAYPALISHIRING` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)  
 
	P   A   H   N  
	A P L S I I G  
	Y   I   R    

>And then read line by line: `PAHNAPLSIIGYIR`  
>Write the code that will take a string and make this conversion given a number of rows:

	string convert(string text, int nRows);

>convert("PAYPALISHIRING", 3) should return `PAHNAPLSIIGYIR`.

<!-- more -->
##解题思路
该题是将字符串按锯齿形进行排列，然后按行进行输出。该题指定了行数`nRows`,则每个锯齿(ZigZag)中的元素个数为`2*nRows-2`,接下来就是对每一行进行遍历，由于其中从**第1行**到**第nRows-2行**中会有穿插的元素，例如上述的`P`，所以需要考虑这些元素的坐标，其实他们的坐标为`j+zigzag-2*i`,因为他们是zigzag中倒数第`2*i`个元素，`i`为行坐标。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String convert(String s, int nRows) {
        //每个zigzag是2*m-2个字符就可以，这里m是结果的行的数量
        char[] c=s.toCharArray();
        int len=c.length;
        if(len==0)
            return "";
        if(nRows==1)
            return s;
        String result="";
        int zigsize=2*nRows-2;
        for(int i=0;i<nRows;i++)
        {
          for(int j=i;j<len;j+=zigsize)
          {
              result+=c[j];
              //需要判断j后面紧跟的元素，它的坐标为j+zigsize-2*i,因为i表示行，正好为倒数第2*i个元素
              if(i!=0&&i!=nRows-1&&(j+zigsize-2*i)<len)
                    result+=c[j+zigsize-2*i];
          }
          
        }
        return result;       
    }
}
{% endhighlight %}

