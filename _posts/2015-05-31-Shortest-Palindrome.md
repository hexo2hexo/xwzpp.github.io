---
layout: post
title:  LeetCode-Shortest Palindrome
description: "Shortest Palindrome"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode]
duoshuo: true
---
##题目
####Shortest Palindrome
> Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

>For example:

>Given `"aacecaaa"`, return `"aaacecaaa"`.

>Given `"abcd"`, return `"dcbabcd"`.

>####Credits:
>Special thanks to @ifanchu for adding this problem and creating all test cases. Thanks to @Freezen for additional test cases.

<!-- more -->
	
##解题思路
该题其实难度不大，主要是存在特别长的测试用例，到时时间或者内存超时。

首先，我们从[Longest Palindromic Substring][1]的思路出发，首先找到从开头开始的最长的回文串的长度，然后再将后面的字符进行翻转添加到前面，但是这个方法虽然时间上比较快，却造成了内存超出。

那么我们看有没有比较简化的方法，首先我们对整个字符串进行翻转，然后不断判断其后缀字符串是否为原字符串的模式字串，如果是，说明这个模式字串就是从开头开始的最长回文。则将原来字符串的不是模式字串的部分加入到翻转字符串的后面即可。这里求解模式字串的方法采用的是经典的[KMP][2]算法
##算法代码
代码采用JAVA实现：
方法一：
{% highlight java %}

//内存超出的方法
//从求解最长的回文串的思想出发，求得从开头开始的最长回文串，然后将剩余的字符添加到开头。
public class Solution {
    public String shortestPalindrome(String s) {
        if(s==null || s.length()==0) return s;
        //首先需要找到从开头开始的最长回文串
        //定义p[i][j]表示从i到j为回文串

        int[][] p=new int[s.length()][s.length()];
        for(int i=0;i<s.length();i++)
        	Array.fill(p[i],0);

        //设定从开头出发的最大回文长度
        int maxstartlen=1;

        //进行初始化设定
        for(int i=0;i<s.length();i++)
        	p[i][i]=1;

        for(int i=0;i<s.length()-1;i++){
        	if(s.charAt(i)==s.charAt(i+1)){
        		p[i][i+1]=1;
        		if(i==0)
        			maxstartlen=2;
        	}
        		

        }
        	

        for(int i=3;i<=s.length();i++)
        {
        	for(int j=0;j<s.length()-i+1;j++)
        	{
        		if(s.charAt(j)==s.charAt(j+i-1) && p[j+1][j+i-1-1]==1)
        		{
        			p[j][j+i-1]=1; 
        			if(j==0)
        				maxstartlen=i;
        		}
        			
        	}
        }

        //需要添加的后缀字符串为
        String str=s.subString(maxstartlen-1);
        StringBuilder sb=new StringBuilder();

        for(int i=str.length()-1;i>=0;i--){
        	sb.append(str.charAt(i));
        }
        sb.append(s);

        return sb.toString();
    }
}
{% endhighlight %}

方法二：
{% highlight java %}
//将整个字符串进行逆转，然后对逆转后的字符串的每个后缀字串判断是否是原来字符串的模式串，然后进行拼接即可
//判断模式串的方法采用KMP算法

public class Solution {
    public String shortestPalindrome(String s) {
        if(s==null || s.length()==0)
        	return s;
        StringBuilder sb=new StringBuilder(s);
        StringBuilder sbnext=sb.reverse();

        int index=0;
        for(int i=0;i<sbnext.length();i++)
        	if(isSubString(s,sbnext.substring(i).toString()))
        	{
        		index=i;
        		break;
        	}

        StringBuilder res=new StringBuilder();
        res.append(sbnext);
        res.append(s.substring(sbnext.length()-index));
        return res.toString();

    }
    
    
    //采用KMP算法进行字串的判断
    public boolean isSubString(String s,String snext){
    	char[] hay=s.toCharArray();
        char[] need=snext.toCharArray();
        if(hay.length==0&&need.length==0) return true;
        if(hay.length==0) return false;
        if(need.length==0) return true;
        if(need.length>hay.length) return false;
        
        //求解next数组
        int[] next=new int[need.length];
        next[0]=-1;
        int i=0;
        int k=-1;
        while(i<need.length-1){
        	if(k==-1 || need[i]==need[k]){
        		i++;
        		k++;
        		next[i]=k;
        	}else{
        		k=next[k];
        	}

        }

        //进行字串查找
        int j=0;
        i=0;
        while(i<hay.length){
        	if(hay[i]==need[j]){
        		i++;
        		j++;
        	}else{
        		j=next[j];
        		if(j==-1){
        			i++;
        			j=0;
        		}
        	}
        	if(j==need.length)
        		break;
        }

        if(j==need.length)
        	return true;
        else
        	return false;

    }
}
{% endhighlight %}

{% highlight java %}
public class Solution {
    public String shortestPalindrome(String s) {  
        StringBuilder sb = new StringBuilder(s).reverse();  
        for(int i=0; i<s.length(); i++) {  
            if(s.startsWith(sb.substring(i))) {  
                return sb.substring(0, i)+s;  
            }  
        }  
        return s;  
    }  
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/leetcode-Longest-Palindromic-Substring.html
[2]:http://pisxw.com/algorithm/Implement-strStr%28%29.html













