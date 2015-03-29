---
layout: post
title:  LeetCode-Reverse Words in a String
description: "Reverse Words in a String"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Reverse Words in a String
>Given an input string, reverse the string word by word.

>For example,   
>Given s = `"the sky is blue"`,    
>return `"blue is sky the"`.   

>####Update (2015-02-12):   
>For C programmers: Try to solve it in-place in O(1) space.

>click to show clarification.

>####Clarification:
+ What constitutes a word?
A sequence of non-space characters constitutes a word.
+ Could the input string contain leading or trailing spaces?
Yes. However, your reversed string should not contain leading or trailing spaces.
+ How about multiple spaces between two words?
Reduce them to a single space in the reversed string.

<!-- more -->
	
##解题思路
我们先介绍一种很直接的做法，就是类似于java中String::split函数做的操作，把字符串按空格分开，不过我们把重复的空格直接忽略过去。接下来就是把得到的结果单词反转过来得到结果。因为过程中就是一次扫描得到字符串，然后再一次扫描得出结果，所以时间复杂度是O(n)。空间上要用一个数组来存，所以是O(n)。实现思路比较清晰，这里就不列举迭代实现的代码了。

接下来我们再介绍另一种方法，思路是先把整个串反转并且同时去掉多余的空格，然后再对反转后的字符串对其中的每个单词进行反转，比如"the sky is blue"，先反转成"eulb si yks eht"，然后在对每一个单词反转，得到"blue is sky the"。这种方法先反转的时间复杂度是O(n)，然后再对每个单词反转需要扫描两次（一次是得到单词长度，一次反转单词）,所以总复杂度也是O(n)，比起上一种方法并没有提高，甚至还多扫描了一次，不过空间上这个不需要额外的存储一份字符串，不过从量级来说也还是O(n)。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public String reverseWords(String s) {
    if(s==null) return null;
    s = s.trim(); //去掉前导空白符和后导空白符
    if(s.length()==0) return "";
    StringBuilder res = new StringBuilder();
    for(int i=s.length()-1; i>=0; i--){
        if(i!=s.length()-1 && s.charAt(i)==' ' && s.charAt(i)==s.charAt(i+1)) continue;
        res.append(s.charAt(i));
    }
    int left=0;
    int right=0;
    while(right<res.length()){
        while(right<res.length() && res.charAt(right)!=' '){
     		right++;
        }
        int next = right+1;
        right--;
        while(left<right){
            char temp = res.charAt(left);
            res.setCharAt(left++, res.charAt(right));
            res.setCharAt(right--, temp);
        }
        left = next;
        right = next;
    }
    return res.toString();
}
{% endhighlight %}






