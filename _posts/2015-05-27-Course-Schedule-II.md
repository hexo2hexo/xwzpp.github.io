---
layout: post
title:  LeetCode-Course Schedule II
description: "Course Schedule II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search,Breadth-first Search,Graph,Topological Sort]
duoshuo: true
---
##题目
####Course Schedule II
>There are a total of n courses you have to take, labeled from 0 to n - 1.

>Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

>Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

>There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

>For example:
>
	2, [[1,0]]
>There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]
>
	4, [[1,0],[2,0],[3,1],[3,2]]
>There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

>######Note:
>The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

>click to show more hints.

>#######Hints:
+ This problem is equivalent to finding the topological order in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
+ Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
+ Topological sort could also be done via BFS.

<!-- more -->
	
##解题思路
该题的思路与[Course Schedule][1]类似，只不过在这题中需要保存最后拓扑结构的序列，因此在返回结果的时候稍微有所变动。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        Graph graph=new Graph(numCourses,prerequisites);
        return graph.topoGraph();
    }

    class Graph{
    	private int n; // 图中节点数量
    	private HashMap<Integer,ArrayList<Integer>> alledges; //所有的边
    	private int[] indegree; //每个节点的入度
    	private int[] outdegree; //每个节点的出度

    	public Graph(int num,int[][] edges)
    	{
    		this.n=num;
    		alledges=new HashMap<Integer,ArrayList<Integer>>();
    		indegree=new int[n];
    		outdegree=new int[n];
    		for(int i=0;i<edges.length;i++){
    			if(alledges.containsKey(edges[i][1])){
    				ArrayList<Integer> tmp=alledges.get(edges[i][1]);
    				tmp.add(edges[i][0]);
    				alledges.put(edges[i][1],tmp);
    			}else{
    				ArrayList<Integer> tmp=new ArrayList<Integer>();
    				tmp.add(edges[i][0]);
    				alledges.put(edges[i][1],tmp);
    			}
    			indegree[edges[i][0]]++;
    			outdegree[edges[i][1]]++;
    		}

    	}

    	public int[] topoGraph()
    	{
    		int count=0;
    		int[] result=new int[n];
    		//对其进行拓扑结构求解
    		//定义个队列其中存放入度为0的节点
    		LinkedList<Integer> queen=new LinkedList<Integer>();
    		for(int i=0;i<indegree.length;i++)
    		{
    			if(indegree[i]==0)
    				queen.offer(i);
    		}

    		while(!queen.isEmpty()){
    			int tmp=queen.poll();
    			result[count]=tmp;
    			count++;
    			//对该节点其所有孩子节点的入度进行-1操作，并判断是否为0
    			ArrayList<Integer> childs=alledges.get(tmp);
    			if(childs!=null){
    				for(int child:childs){
    					indegree[child]--;
    					if(indegree[child]==0)
    						queen.offer(child);
    				}
    			}
    		}

    		if(count==n) //表示完美生成拓扑结构，即可以完成所有课程
    			return result;
    		else
    		{
    			return new int[]{}; //返回一个空的数组
    		}
    	}

    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Course-Schedule.html










