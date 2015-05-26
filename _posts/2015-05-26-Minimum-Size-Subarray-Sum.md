---
layout: post
title:  LeetCode-Minimum Size Subarray Sum
description: "Minimum Size Subarray Sum"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers,Binary Search]
duoshuo: true
---
##题目
####Minimum Size Subarray Sum
>Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

>For example, given the array `[2,3,1,2,4,3]` and `s = 7`,      
>the subarray `[4,3]` has the minimal length under the problem constraint.

>click to show more practice.

>#####More practice:
>If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

>#####Credits:
>Special thanks to @Freezen for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题是求解和大于目标值的最小长度，比较容易想到的方法是采用滑动窗口的方法，满足滑动窗口中的元素和大于目标元素，且维护一个最小长度值，但是这种方法需要遍历一遍数组，整个时间复杂度为`O(n)`。

有没有更加快速的方法，其实是有的，我们可以通过一个数组sum,sum[i]记录从0到i-1的所有元素之和，思路就是记录每个位置上到当前位置前面的和：sum[i] 为0->i-1的所有数字和，如果sum[i]>= 目标数字，就2分查找比sum[i]-target+1小且是最大的数字。如果找到，index=j那么j到i-1就是这个subarray， length=i-1-j+1=i-j。整体的时间复杂度能够达到`O(nlogn)`
。

##算法代码
代码采用JAVA实现：
{% highlight java %}
//时间复杂度为O(n)的方法
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        //采用滑动窗口的方法
        if(nums.length==0 || nums==null) return 0;
        int head=0,tail=0,cursum=0;
        int min=Integer.MAX_VALUE;
        while(tail<nums.length)
        {
        	cursum+=nums[tail];
        	while(cursum>=s){
        		min=Math.min(min,tail-head+1);
        		cursum-=nums[head];
        		head++;
        	}
        	tail++;
        }
        return min==Integer.MAX_VALUE?0:min;
    }
}

//时间复杂度为O(nlogn)的方法
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
	    if(nums.length==0 || nums==null) return 0;
	    //定义一个sum数组，其中存放当前位置之前的左右元素之和
	    int min=Integer.MAX_VALUE;
	    int[] sum=new int[nums.length+1];
	    for(int i=0;i<nums.length;i++)
	    {
	    	sum[i+1]=sum[i]+nums[i];
	    	if(sum[i+1]>=s){
	    		int j=binarySearch(0,i,sum[i+1]-s+1,sum);
	    		if(j>-1){
	    			min=Math.min(min,i-j+1);
	    		}
	    	}
	    }
	    return min==Integer.MAX_VALUE?0:min;
    }


    int binarySearch(int left, int right, int target, int[] sum) {  
        int result = -1;  
        while (left < right-1) {  
            int m = left + (right-left)/2;  
            if (sum[m] >= target) {  
                right = m-1;  
            } else if (sum[m] < target) {  
                left = m;  
            }  
        }  
        if (sum[right] < target) {  
            return right;  
        } else if (sum[left] < target) {  
            return left;  
        } else {  
            return -1;  
        }  
    }  

}
{% endhighlight %}











