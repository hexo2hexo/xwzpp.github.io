---
layout: post
title:  LeetCode-Text Justification
description: "Text Justification"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Text Justification
>Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

>You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

>Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

>For the last line of text, it should be left justified and no extra space is inserted between words.

>For example,    
>**words**: `["This", "is", "an", "example", "of", "text", "justification."]`
>**L**: `16`.

>Return the formatted lines as:  
>
	[
	   "This    is    an",
	   "example  of text",
	   "justification.  "
	]

>**Note**: Each word is guaranteed not to exceed L in length.

>**Corner Cases**:   
>A line other than the last line might contain only one word. What should you do in this case?   
>In this case, that line should be left-justified.

<!-- more -->
	
##解题思路
这道题属于纯粹的字符串操作，要把一串单词安排成多行限定长度的字符串。   
主要难点在于空格的安排，首先每个单词之间必须有空格隔开，而当当前行放不下更多的单词并且字符又不能填满长度`L`时，我们要把空格均匀的填充在单词之间。如果剩余的空格量刚好是间隔倍数那么就均匀分配即可，否则还必须把多的空格依次从左往右放到前面的间隔里面。最后一个细节就是最后一行不需要均匀分配空格，句尾留空就可以，所以要单独处理一下。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<String> fullJustify(String[] words, int L) {
        ArrayList<String> res = new ArrayList<String>();  
	    if(words==null || words.length==0)  
	        return res;  
	    int first=0; //一行中第一个单词的位置
	    int last=0;  //一行中最后一个单词的位置
	    int count=0; //一行中的字符数(不包括空格)
	    for(;last<words.length;last++)
	    {
	    	if((count+words[last].length()+last-first)>L)  //last-first表示单词间隔数,因为单词之间至少一个空格
	    	{
	    		last--; //最后一个单词不满足
	    		int konggenum=L-count;
	    		//判断空格是否可以被间隔均分
	    		int isjunfen=0;
	    		int countkongge=0;
	    		if((last-first)>0)
	    		{
	    			isjunfen=konggenum%(last-first);
	    			countkongge=konggenum/(last-first);
	    		}
	    		StringBuilder row=new StringBuilder();
	    		for(int j=first;j<=last;j++)
				{
					row.append(words[j]);
					if(j<last)
					{
						for(int i=0;i<countkongge;i++)
							row.append(" ");
						if(isjunfen>0) //不可以均分 ，多出的空格依次放在左边
							row.append(" ");
						isjunfen--;
					}
					
				}
				for(int j=row.length();j<L;j++)  
	            {  
	                row.append(" ");  
	            }    
    			res.add(row.toString());
    			first=last+1;
    			count=0;	

	    	}else{
	    		count+=words[last].length();
	    	}
	    }
	    //单独处理最后一行.因为最后一行的空格分布与前面不一样
	    StringBuilder row=new StringBuilder();
	    for(int i=first;i<words.length;i++)
	    {
	    	row.append(words[i]); 
	    	if(row.length()<L)
	    		row.append(" ");
	    }
	    for(int i=row.length();i<L;i++)  
	    {  
	        row.append(" ");  
	    }  
	    res.add(row.toString());
	    return res;    	
    }
}
{% endhighlight %}

