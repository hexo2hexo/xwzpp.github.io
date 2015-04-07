---
layout: post
title:  LeetCode-Largest Number
description: "Largest Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Sort]
duoshuo: true
---
##题目
####Largest Number
>Given a list of non negative integers, arrange them such that they form the largest number.

>For example, given `[3, 30, 34, 5, 9]`, the largest formed number is `9534330`.

>Note: The result may be very large, so you need to return a string instead of an integer.

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
1 对于两个备选数字a和b, 如果str(a) + str(b) > str(b) + str(a), 则a在b之前，否则b在a之前，按照这个原则对原数组从大到小排序即可。我们只需要写出sort函数的自定义比较函数即可。还有我们，要注意一个特殊情况，如果字符串后的字符串从0开始，我们返回“0”。

2 首先，我们将num转成字符串存入数组，然后根据自定义比较函数排序，之后再对排序后的字符串连接成一个字符串，最后排除特殊情况，得到所求结果。

因此，本题的关键就是根据以上的推导建立比较规则，借助Comparator（或者Comparable，如果你的类可以实现该接口）

得到顺序。使用到Arrays.sort(str[],new Comparator{});

本题提醒我们数字可能会很大，因此组合和比较的时候都是用字符串。还好字符串的比较可以使用comparatorTo方法。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String largestNumber(int[] num) {
        if(num==null || num.length==0)
        	return "";
        String[] cur=new String[num.length];
        for(int i=0;i<num.length;i++)
        {
        	cur[i]=num[i]+"";
        }
        Arrays.sort(cur,new MyComparator());
        String RST="";  
        for(int i=0;i<cur.length;i++){  
            RST+=cur[i];  
        }  
        if(RST.charAt(0)=='0')
            RST="0";
  
        return RST;  
    }

	//自己实现比较函数
    public class MyComparator implements Comparator<String> {  

        public int compare(String o1, String o2) {  
            return (o2+o1).compareTo(o1+o2);  
        }  
    }  
}
{% endhighlight %}








