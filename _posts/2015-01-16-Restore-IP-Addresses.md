---
layout: post
title:  LeetCode-Restore IP Addresses
description: "Restore IP Addresses"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,BackTracking,String]
duoshuo: true
---
##题目
####Restore IP Addresses
>Given a string containing only digits, restore it by returning all possible valid IP address combinations.

>For example:   
>Given `"25525511135"`,

>return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)

<!-- more -->
	
##解题思路
这道题的解法非常接近于NP问题，也是采用递归的解法。基本思路就是取出一个合法的数字，作为IP地址的一项，然后递归处理剩下的项。可以想象出一颗树，每个结点有三个可能的分支（因为范围是0-255，所以可以由一位两位或者三位组成）。并且这里树的层数不会超过四层，因为IP地址由四段组成，到了之后我们就没必要再递归下去，可以结束了。这里除了上述的结束条件外，另一个就是字符串读完了。可以看出这棵树的规模是固定的，不会像平常的NP问题那样，时间复杂度取决于输入的规模，是指数量级的，所以这道题并不是NP问题，因为他的分支是四段，有限制.

实现中需要一个判断数字是否为合法ip地址的一项的函数，首先要在0-255之间，其次前面字符不能是0。剩下的就是NP问题的套路了，递归中套一个for循环，不熟悉的朋友可以看看[N-Queens][1]哈

##算法代码
代码采用JAVA实现：     
{% highlight java %}
public class Solution {
    public ArrayList<String> restoreIpAddresses(String s) {
        ArrayList<String> res = new ArrayList<String>();
        if(s==null || s.length()==0)
        	return res;
        helper(s,0,1,"",res);
        return res; 
    }
    //index：字符串中的位置
    //segment：表示ip地址中的第几段
    //item:表示前面已得到的字符串
    public void helper(String s,int index,int segment,String item,ArrayList<String> res)
	{
		if(index>s.length())
			return;
		//每个ip有四个段，如果达到第4段
		if(segment==4)
		{
			String str = s.substring(index);
			if(isValid(str)){
				//字串合法
				res.add(item+"."+str);
			}
			return;
		}
		//每一段为0~255,字符长度为1~3位
		for(int i=1;i<4 && (index+i)<=s.length();i++){
			String str=s.substring(index,index+i);
			if(isValid(str))
			{
				//第一段有个特例
				if(segment==1){
					helper(s,index+i,segment+1,str,res);
				}else{
					helper(s,index+i,segment+1,item+"."+str,res);
				}
			}
		}

	}

	public boolean isValid(String s)
	{
	 	//长度大于3，不满足	
		if(s==null || s.length()==0 || s.length()>3)
			return false;
		int num = Integer.parseInt(s);
		//首位为0且长度大于1，不满足
		if(s.charAt(0)=='0' && s.length()>1)
			return false;
		//在0~255之间的，满足
		if(num>=0 && num<=255)
			return true;
		return false;
	}
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/N-Queens.html



