---
layout: post
title:  LeetCode-Single Number 
description: "Single Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Bit Manipulation]
duoshuo: true
---
##题目
####Single Number 
>Given an array of integers, every element appears twice except for one. Find that single one.

>####Note:
>Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

<!-- more -->
	
##解题思路 
这个题比较直接的想法是用一个HashMap对于出现的元素进行统计，key是元素，value是出现个数，如果元素出现三次，则从HashMap中移除，最后在HashMap剩下来的元素就是我们要求的元素（因为其他元素都出现两次，有且仅有一个元素不是如此）。这样需要对数组进行一次扫描，所以时间复杂度是O(n)，而需要一个哈希表来统计元素数量，所以空间复杂度是O(n)。这个方法非常容易实现，就不列举代码了。       
在LeetCode的题目中要求我们不要用额外空间来实现，也就是O(1)空间复杂度。实现的思路是基于数组的元素是整数，我们通过统计整数的每一位来得到出现次数。我们知道如果每个元素重复出现两次，那么每一位出现1的次数也会是2的倍数，如果我们统计完对每一位进行取余2，那么结果中就只剩下那个出现一次的元素。总体只需要对数组进行一次线性扫描，统计完之后每一位进行取余3并且将位数字赋给结果整数，这是一个常量操作（因为整数的位数是固定32位），所以时间复杂度是O(n)。而空间复杂度需要一个32个元素的数组，也是固定的，因而空间复杂度是O(1)。

##算法代码
代码采用JAVA实现： 
{% highlight java %}

{% endhighlight %}



