---
layout: post
title:  LeetCode-Clone Graph
description: "Clone Graph"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search,Breadth-first Search,Graph]
duoshuo: true
---
##题目
####Clone Graph
>Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.


>####OJ's undirected graph serialization:
>Nodes are labeled uniquely.

>We use `#` as a separator for each node, and `,` as a separator for node label and each neighbor of the node.    
>As an example, consider the serialized graph {0,1,2#1,2#2,2}.

>The graph has a total of three nodes, and therefore contains three parts as separated by #.

>First node is labeled as `0`. Connect node `0` to both nodes `1` and `2`.   
>Second node is labeled as `1`. Connect node `1` to node `2`.    
>Third node is labeled as `2`. Connect node `2` to node `2` (itself), thus forming a self-cycle.    
>Visually, the graph looks like the following:     

       1
      / \
     /   \
    0 --- 2
         / \
         \_/

<!-- more -->
	
##解题思路 
该题是对图进行复制，也就是对图进行遍历。而图的遍历方法主要分为深度和广度两种，这里两种都可以实现。在这里我们使用`HashMap`来存放旧节点和新节点的对应关系，以便能够迅速找到对应的节点。

##算法代码
代码采用JAVA实现： 
广度优先遍历：
{% highlight java %}
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node==null)
            return null;
        LinkedList<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        UndirectedGraphNode copy = new UndirectedGraphNode(node.label);
        map.put(node,copy);
        queue.offer(node);
        while(!queue.isEmpty())
        {
            UndirectedGraphNode cur = queue.poll();
            for(int i=0;i<cur.neighbors.size();i++)
            {
                if(!map.containsKey(cur.neighbors.get(i)))
                {
					//创建新节点
                    copy = new UndirectedGraphNode(cur.neighbors.get(i).label);
                    map.put(cur.neighbors.get(i),copy);
                    queue.offer(cur.neighbors.get(i));
                }
				//存入邻居节点
                map.get(cur).neighbors.add(map.get(cur.neighbors.get(i)));
            }
        }
        return map.get(node);
    }
}
{% endhighlight %}


深度优先遍历：
{% highlight java %}
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */

//深度优先遍历
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node==null)
            return null;
        LinkedList<UndirectedGraphNode> stack = new LinkedList<UndirectedGraphNode>();
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        UndirectedGraphNode copy = new UndirectedGraphNode(node.label);
        map.put(node,copy);
        stack.push(node);
        while(!stack.isEmpty())
        {
            UndirectedGraphNode cur = stack.pop();
            for(int i=0;i<cur.neighbors.size();i++)
            {
                if(!map.containsKey(cur.neighbors.get(i)))
                {
                    copy = new UndirectedGraphNode(cur.neighbors.get(i).label);
                    map.put(cur.neighbors.get(i),copy);
                    stack.push(cur.neighbors.get(i));
                }
                map.get(cur).neighbors.add(map.get(cur.neighbors.get(i)));
            }
        }
        return map.get(node);
    }
}

{% endhighlight %}








