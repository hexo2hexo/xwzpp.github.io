---
layout: post
title:  LeetCode-Letter Combinations of a Phone Number
description: "Letter Combinations of a Phone Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking,String]
duoshuo: true
---
##题目
####Letter Combinations of a Phone Number

>Given a digit string, return all possible letter combinations that the number could represent.

>A mapping of digit to letters (just like on the telephone buttons) is given below.

![][1]

>
	Input:Digit string "23"
	Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

>####Note:
>Although the above answer is in lexicographical order, your answer could be in any order you want.

<!-- more -->

##解题思路
该题是给定一个数字，然后将在手机上该数字所对应的每一位字符进行组合，得到所有的组合。这里需要知道手机上的每一位代表的字符集。

		手机数字对应
		1：""
		2: "abc"
		3: "def"
		4: "ghi"
		5: "jkl"
		6: "mno"
		7: "pqrs"
		8: "tuv"
		9: "wxyz"
		0: " "
得到一个数字代表的字符后，只需要对字符进行全排列组合即可得到结果。这里可以采用**递归**的方法对多个数字进行字符组合。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	/*
		手机数字对应
		1：""
		2: "abc"
		3: "def"
		4: "ghi"
		5: "jkl"
		6: "mno"
		7: "pqrs"
		8: "tuv"
		9: "wxyz"
		0: " "

	*/
    public ArrayList<String> letterCombinations(String digits) {
        char[] cdigit=digits.toCharArray();
        ArrayList<String> strList=new ArrayList<String>();
        ArrayList<String> strListPre=new ArrayList<String>();
        ArrayList<String> strListLast=new ArrayList<String>();
        if(cdigit.length==0) 
        {
            strList.add("");
            return strList;
        }
            
        if(cdigit.length==1)
        {
        	switch(cdigit[0])
        	{
        		case '1':break;
        		case '2':{
        			strList.add("a");
        			strList.add("b");
        			strList.add("c");
        			break;
        		}
        		case '3':{
        			strList.add("d");
        			strList.add("e");
        			strList.add("f");
        			break;
        		}
        		case '4':{
        			strList.add("g");
        			strList.add("h");
        			strList.add("i");
        			break;
        		}
        		case '5':{
        			strList.add("j");
        			strList.add("k");
        			strList.add("l");
        			break;
        		}
        		case '6':{
        			strList.add("m");
        			strList.add("n");
        			strList.add("o");
        			break;
        		}
        		case '7':{
        			strList.add("p");
        			strList.add("q");
        			strList.add("r");
        			strList.add("s");
        			break;
        		}
        		case '8':{
        			strList.add("t");
        			strList.add("u");
        			strList.add("v");
        			break;
        		}
        		case '9':{
        			strList.add("w");
        			strList.add("x");
        			strList.add("y");
        			strList.add("z");
        			break;
        		}
        		case '0':{
        			strList.add(" ");
        			break;
        		}
        	}
        }else{
        	strListPre=letterCombinations(String.valueOf(cdigit,0,cdigit.length-1)); //前cdigit.length-1个数的字符组合结果
        	strListLast=letterCombinations(String.valueOf(cdigit,cdigit.length-1,1)); //最后一个数的字符组合结果
        	for(String str1:strListPre)
        	{
        		for(String str2:strListLast)
        		{
        			String s=str1+str2;
        			strList.add(s);
        		}
        	}
        		
        }
        return strList;
    }
}
{% endhighlight %}

[1]:/img/Letter-Combinations-of-a-Phone-Number/Phone.png


