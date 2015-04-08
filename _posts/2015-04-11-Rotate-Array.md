---
layout: post
title:  LeetCode-Rotate Array
description: "BRotate Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Rotate Array
>Rotate an array of n elements to the right by k steps.

>For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

>####Note:
>Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

>####Hint:
+ Could you do it in-place with O(1) extra space?
+ Related problem: Reverse Words in a String II

>####Credits:
>Special thanks to @Freezen for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这道题如果用extra space O(n)的话很简单，就是把第i个元素移动到 (i+k)%size 位置就行。        
但是如果只能用O(1) extra space的话，就是把一个元素移动到它对应的新位置，再把新位置的元素移动到下一个新位置，直到又回到初始位置为止。但这样的话，进行了一个圈，回到初始位置后，不一定是把数组中所有位置都移动了，而是看（size, k）的最大公约数，一共有gcd个圈，每个圈的起始位置是 0，1，2，... (gcd-1)，但是这里没必要算出来gcd，只需要有一个counter变量，记录移了几个数了，一圈后，如果counter==size，说明移完了，如果counter<size，说明没移完，则把起始位置加1，继续移动新圈。这样的话，空间复杂度O(1)，时间复杂度O(n)   

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public void rotate(int[] nums, int k) {
        int size = nums.length;  
	    int counter = 0;  
	    int start = 0;  
	    while(counter<size){  
	        int last = start;  
	        int next = (start+k)%size;  
	        int val = nums[last];  
	        do{  
	            int tmp = nums[next];  
	            nums[next] = val;  
	            val = tmp;  
	            last = next;  
	            next = (next+k)%size;  
	            counter++;  
	        }while(last!=start);  
	          
	        start++;  
	    }  
    }
}
{% endhighlight %}








