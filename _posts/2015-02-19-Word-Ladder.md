---
layout: post
title:  LeetCode-Word Ladder
description: "Word Ladder"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Breadth-first Search]
duoshuo: true
---
##题目
####Word Ladder
>Given two words (start and end), and a dictionary, find the length of shortest transformation sequence from start to end, such that:
>
1.Only one letter can be changed at a time
2.Each intermediate word must exist in the dictionary
For example,

>Given:
>start = `"hit"`   
>end = `"cog"`  
>dict = `["hot","dot","dog","lot","log"]`   
>As one shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,
return its length `5`.    

>####Note:
+ Return 0 if there is no such transformation sequence.
+ All words have the same length.
+ All words contain only lowercase alphabetic characters.

<!-- more -->
	
##解题思路
该题是一个寻找字符串中最短路径的问题，我们可以把它转变成图来求解。我们先给题目进行图的映射，顶点则是每个字符串，然后两个字符串如果相差一个字符则我们进行连边。接下来看看这个方法的优势，注意到我们的字符集只有小写字母，而且字符串长度固定，假设是L。那么可以注意到每一个字符可以对应的边则有25个（26个小写字母减去自己），那么一个字符串可能存在的边是25*L条。接下来就是检测这些边对应的字符串是否在字典里，就可以得到一个完整的图的结构了。根据题目的要求，等价于求这个图一个顶点到另一个顶点的最短路径，一般我们用广度优先搜索即可。

下面的代码框架整体上是一个图的广度优先搜索问题，只不过在判断边的时候需要改变字符，并判断是否在字典中。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public int ladderLength(String start, String end, Set<String> dict) {
        if(start==null || end==null || dict==null || start.length()==0 || end.length()==0 || start.length()!=end.length())
        	return 0;
        //把这道题抽象为图中寻找最短路径长度的问题，可以采用图的广度优先遍历
        LinkedList<String> queen=new LinkedList<String>();//定义队列
        HashSet<String> isVisited=new HashSet<String>();//定义已经访问过的节点
        int level=1;//定义当前的层级
        int curNum=1;//定义当前一层的节点数
        int nextNum=0;//定义下一层的节点数
        queen.offer(start);
        isVisited.add(start);
        while(!queen.isEmpty())
        {
        	String str=queen.poll();
        	curNum--;
        	//去寻找和该节点可能差一个字母的所有单词
        	for(int i=0;i<str.length();i++)
        	{
        		char[] charStr=str.toCharArray();
        		//对每一个字符进行设定，判断是否存在这个单词
        		for(char a ='a';a<='z';a++) //这里其实包含了其自身
        		{
        			charStr[i]=a;
        			String gstr=new String(charStr);
        			if(gstr.equals(end)) //找到了end 单词，返回最短路径，即最短层级
        				return level+1;
        			if(dict.contains(gstr) && !isVisited.contains(gstr))
        			{
        				nextNum++;
        				queen.offer(gstr);
        				isVisited.add(gstr);
        			}
        		}
        	}
        	if(curNum==0) //说明该层访问结束，需要进入下一层
        	{
        		curNum=nextNum;
        		nextNum=0;
        		level++;
        	}
        }
        return 0;
    }
}
{% endhighlight %}









