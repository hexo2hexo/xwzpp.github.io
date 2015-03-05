---
layout: post
title:  LeetCode-Interleaving String
description: "Interleaving String"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,String]
duoshuo: true
---
##题目
####Interleaving String
>Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

>For example,    
>Given:     
>s1 = `"aabcc"`,     
>s2 = `"dbbca"`,    

>When s3 = `"aadbbcbcac"`, return true.     
>When s3 = `"aadbbbaccc"`, return false.

<!-- more -->
	
##解题思路
这是一道关于字符串操作的题目，要求是判断一个字符串能不能由两个字符串按照他们自己的顺序，每次挑取两个串中的一个字符来构造出来。
   
像这种判断能否按照某种规则来完成某个量的题目，很容易会想到用**动态规划**来实现。  
  
先说说维护量，res[i][j]表示用s1的前i个字符和s2的前j个字符能不能按照规则表示出s3的前i+j个字符，如此最后结果就是res[s1.length()][s2.length()]，判断是否为真即可。接下来就是递推式了，假设知道res[i][j]之前的所有历史信息，我们怎么得到res[i][j]。可以看出，其实只有两种方式来递推，一种是选取s1的字符作为s3新加进来的字符，另一种是选s2的字符作为新进字符。而要看看能不能选取，就是判断s1(s2)的第i(j)个字符是否与s3的i+j个字符相等。如果可以选取并且对应的res[i-1][j](res[i][j-1])也为真，就说明s3的i+j个字符可以被表示。这两种情况只要有一种成立，就说明res[i][j]为真，是一个或的关系。所以递推式可以表示成

	res[i][j] = res[i-1][j]&&s1.charAt(i-1)==s3.charAt(i+j-1) || res[i][j-1]&&s2.charAt(j-1)==s3.charAt(i+j-1)

时间上因为是一个二维动态规划，所以复杂度是O(m*n)，m和n分别是s1和s2的长度

把动态规划中的二维数组如何降维成一维数组：
这个降下来并不是通过循环的哈~ 就是说本来是二维的历史信息，但是如果历史信息只需要用到上一行的信息，那么说明前面的信息就不需要了，只留一行即可，然后在更新当前一行覆盖上一行的信息，所以就只需要一维数组了

##算法代码
代码采用JAVA实现：    
{% highlight java %}
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int l1 = s1.length();
        int l2 = s2.length();
        int l3 = s3.length();
        if(l1 != l3 -l2)
            return false;
        boolean [][] res = new boolean[l1 + 1][l2 + 1];
        res[0][0] = true;
        for(int k = 1; k <= l3; k++){
            for(int i = 0; i <= k && i <= l1; i++){
                int j = k - i;
                if(j > l2)
                    continue;
                res[i][j] = false;
                if(i>0 && s1.charAt(i-1) == s3.charAt(k-1) && res[i-1][j])
                    res[i][j] = true;
                if(j > 0 && s2.charAt(j-1) == s3.charAt(k-1) && res[i][j-1])
                    res[i][j] = true;
            }
            
        }
        return res[l1][l2];
    }
}
{% endhighlight %}



