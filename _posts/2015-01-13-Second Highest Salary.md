---
layout: post
title:  LeetCode-Second Highest Salary
description: "Second Highest Salary"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Database]
duoshuo: true
---
##题目
####Second Highest Salary
>Write a SQL query to get the second highest salary from the Employee table.
>
	+----+--------+
	| Id | Salary |
	+----+--------+
	| 1  | 100    |
	| 2  | 200    |
	| 3  | 300    |
	+----+--------+

>For example, given the above Employee table, the second highest salary is `200`. If there is no second highest salary, then the query should return `null`.

<!-- more -->
	
##解题思路
该题是找到表中第二大的值，首先我们可以找到最大的值，然后再在比最大值小的值中找到最大的那个即可。

##算法代码
代码采用mysql实现：
{% highlight mysql %}
# Write your MySQL query statement below
select max(Salary) from Employee
where Salary < (select max(Salary) from Employee)
{% endhighlight %}

