---
layout: post
title:  LeetCode-Maximum Gap
description: "Maximum Gap"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Sort]
duoshuo: true
---
##题目
####Maximum Gap
>Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

>Try to solve it in linear time/space.

>Return 0 if the array contains less than 2 elements.

>You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.

>####Credits:
>Special thanks to @porker2008 for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这道题首先一定要有“排序”的思想，但是常用的排序算法复杂度至少是O(NlogN)，不满足题意。进一步思考可以得出，这里的“排序”不一定非要“完整排序”，可以只要“部分排序”即可，这可以想到桶排序，只要意识到了桶排序，这道题就解决了一大半。

假设有取值范围为A到B的N个元素，则他们的最大gap不会小于celling[(B - A) / (N - 1)]。     
让桶的长度len = celling[(B - A) / (N - 1)]，则我们最多会有num = (B - A) / len + 1个桶。    
对于数组中的任意元素K，我们可以通过计算toc = (K - A) / len轻松的找到它属于哪一个桶，然后我们维护每个桶中的最大值和最小值。       
由于同一个桶中元素的最大差值是len - 1，所有最后的答案不会是来自同一个桶中的两个元素。     
对于每一个非空的桶p，找到下一个非空的桶q，然后q.min - p.max就是该问题的潜在的最大值。返回这些值的最大值。           

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {

	class bucket{
		public int min;
		public int max;
		public int count=0;

		bucket(int min,int max){
			this.min=min;
			this.max=max;
		}
	}

    public int maximumGap(int[] num) {
        if(num==null || num.length<2)
        	return 0;
        int maxnum=Integer.MIN_VALUE;
        int minnum=Integer.MAX_VALUE;
        for(int val:num)
        {
        	maxnum=Math.max(maxnum,val);
        	minnum=Math.min(minnum,val);
        }

        int bucketlen=(int)Math.ceil((double)(maxnum-minnum)/(num.length-1));
        int bucketnum=(maxnum-minnum)/bucketlen+1;
        bucket[] bucketsum=new bucket[bucketnum];
        for(int i=0;i<bucketsum.length;i++)
        	bucketsum[i]=new bucket(Integer.MAX_VALUE,Integer.MIN_VALUE);
        for(int val:num)
        {
        	int index=(val-minnum)/bucketlen;
        	bucketsum[index].min=Math.min(bucketsum[index].min,val);
        	bucketsum[index].max=Math.max(bucketsum[index].max,val);
        	bucketsum[index].count++;
        }

        int maxdef=0;
        //放置不为空的桶
        ArrayList<bucket> arraylist = new ArrayList<bucket>();  
        for(int i=0; i<bucketsum.length;i++){  
             if(bucketsum[i].count!=0){  
                    arraylist.add(bucketsum[i]);  
            }  
        }
        //求最大间隔
        for(int i=0;i<arraylist.size()-1;i++)
        {
        	
        	maxdef=Math.max(maxdef,Math.abs(arraylist.get(i).max-arraylist.get(i+1).min));
        	
        }

        return maxdef;

    }
}
{% endhighlight %}





