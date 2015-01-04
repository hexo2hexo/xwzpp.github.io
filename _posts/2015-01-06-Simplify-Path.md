---
layout: post
title:  LeetCode-Simplify Path
description: "Simplify Path"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Stack,String]
duoshuo: true
---
##题目
####Simplify Path
>Given an absolute path for a file (Unix-style), simplify it.

>For example,    
>path = `"/home/"`, => `"/home"`   
>path = `"/a/./b/../../c/"`, => `"/c"`  
>
>**Corner Cases**:
>
>1. Did you consider the case where path = `"/../"`?   
>In this case, you should return `"/"`.
>2. Another corner case is the path might contain multiple slashes `'/'` together, such as "`/home//foo/`".   
>In this case, you should ignore redundant slashes and return "/home/foo". 

<!-- more -->
	
##解题思路
思路比较明确，就是维护一个栈，对于每一个块（以`/`作为分界）进行分析，如果遇到`..`则表示要上一层，那么就是进行出栈操作，如果遇到`.`则是停留当前，直接跳过，其他文件路径则直接进栈即可。最后根据栈中的内容转换成路径即可（这里是把栈转成数组，然后依次添加）。

java中栈的实现可以使用	`LinkedList`，元素的插入和删除是在链表头部进行。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
   public String simplifyPath(String path) {  
        if(path == null || path.length()==0)  
        {  
            return "";  
        }  
        LinkedList<String> stack = new LinkedList<String>();  
        StringBuilder res = new StringBuilder();  
        int i=0;  
          
        while(i<path.length())  
        {  
            int index = i;  
            StringBuilder temp = new StringBuilder();  
            while(i<path.length() && path.charAt(i)!='/')  
            {  
                temp.append(path.charAt(i));  
                i++;  
            }  
            if(index!=i)  
            {  
                String str = temp.toString();  
                if(str.equals(".."))  
                {  
                    if(!stack.isEmpty())  
                        stack.pop();  
                }  
                else if(!str.equals("."))  
                {  
                    stack.push(str);  
                }  
            }  
            i++;  
        }  
        if(!stack.isEmpty())  
        {  
            String[] strs = stack.toArray(new String[stack.size()]);  
            for(int j=strs.length-1;j>=0;j--)  //LinkedList是在头部进行插入和删除的
            {  
              res.append("/"+strs[j]);  
            }  
        }  
        if(res.length()==0)  
            return "/";  
        return res.toString();  
    }  
}
{% endhighlight %}

