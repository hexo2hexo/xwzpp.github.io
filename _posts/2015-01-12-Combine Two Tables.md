---
layout: post
title:  LeetCode-Combine Two Tables
description: "Combine Two Tables"
category: Database
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode]
duoshuo: true
---
##题目
####Combine Two Tables
>Table: `Person`
>
	+-------------+---------+
	| Column Name | Type    |
	+-------------+---------+
	| PersonId    | int     |
	| FirstName   | varchar |
	| LastName    | varchar |
	+-------------+---------+
	PersonId is the primary key column for this table.

>Table: `Address`
>	
	+-------------+---------+
	| Column Name | Type    |
	+-------------+---------+
	| AddressId   | int     |
	| PersonId    | int     |
	| City        | varchar |
	| State       | varchar |
	+-------------+---------+
	AddressId is the primary key column for this table.

>Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:
>
	FirstName, LastName, City, State

<!-- more -->
	
##解题思路
该题是合并两个表，可以通过链接操作。

##SQL语句
代码采用mysql实现：
{% highlight mysql %}
# Write your MySQL query statement below
select FirstName,LastName,City,State from Person
left join Address using(PersonId)
{% endhighlight %}

