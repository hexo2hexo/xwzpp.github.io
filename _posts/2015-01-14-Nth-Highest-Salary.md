---
layout: post
title:  LeetCode-Nth Highest Salary
description: "Nth Highest Salary"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Database]
duoshuo: true
---
##题目
####Nth Highest Salary
>Write a SQL query to get the nth highest salary from the `Employee` table.
>
	+----+--------+
	| Id | Salary |
	+----+--------+
	| 1  | 100    |
	| 2  | 200    |
	| 3  | 300    |
	+----+--------+

>For example, given the above Employee table, the nth highest salary where n = 2 is `200`. If there is no nth highest salary, then the query should return `null`.

<!-- more -->
	
##解题思路
该题是找到表中第n大的元素，这里通过排序后，使用limit进行选去，这里需要注意的是，如果不加`SET M=N-1;`,将`LIMIT M, 1`改为`LIMIT N-1, 1`则会出错，原因是由于mysql有值的限制，而对预先定义的变量除外，详见[Why using LIMIT N-1,1 will cause error][1]。

##算法代码
代码采用mysql实现：
{% highlight mysql %}
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
DECLARE M INT;
SET M=N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT M, 1
  );
END
{% endhighlight %}

[1]:https://oj.leetcode.com/discuss/21320/why-using-limit-n-1-1-will-cause-error

