---
layout: post
title:  LeetCode-Course Schedule
description: "Course Schedule"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search,Breadth-first Search,Graph,Topological Sort]
duoshuo: true
---
##题目
####Course Schedule
>There are a total of n courses you have to take, labeled from `0` to `n - 1`.

>Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

>Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

>For example:
>
	2, [[1,0]]

>There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.
>
	2, [[1,0],[0,1]]

>There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

>click to show more hints.

>####Hints:
>
* This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
* There are several ways to represent a graph. For example, the input prerequisites is a graph represented by a list of edges. Is this graph representation appropriate?
* Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
* Topological sort could also be done via BFS.

<!-- more -->
	
##解题思路
该题如果想清楚，会发现其实是找出一个有向图中是否存在环的问题，而有向图中环的问题可以转换为求其拓扑结构，如果能够完美的构成拓扑结构，则说明不存在环，否则说明其中存在环。

求解拓扑结构的算法思路是这样的：对每个节点的入度出度进行计算，然后选取其中入度为0的节点，放入拓扑序中，然后对每一个和该节点关联的节点的出度进行-1操作，然后重复上述的过程直到没有找到入度为0的节点，然后判断拓扑序中元素的个数，如果等于图中节点的个数则说明完美生成拓扑结构，不存在环路，否则存在环路。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        Graph g=new Graph(numCourses,prerequisites);
        return g.topoGraph();
    }

    class Graph{
    	private int n;
    	private HashMap<Integer,ArrayList<Integer>> alledges=new HashMap<Integer,ArrayList<Integer>>();
    	private int[] indegree;
    	private int[] outdegree; 

    	//构造图结构，由于只需要构建拓扑结构，因此只需要保存入度及出度，这里需要注意一点的是
    	//哪一个节点是源节点，哪一个节点是目标节点
    	public Graph(int nvatex,int[][] edges){
    		this.n=nvatex;
    		this.indegree=new int[nvatex];
    		this.outdegree=new int[nvatex];
    		for(int i=0;i<edges.length;i++){
				if(alledges.containsKey(edges[i][1]))
				{
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

    	public boolean topoGraph()
    	{
    		int count=0;
    		LinkedList<Integer> queen=new LinkedList<Integer>();
    		//将所有入度为0的点入队
			for(int i=0;i<n;i++){
				if(indegree[i]==0)
					queen.offer(i);
			}

			//构建拓扑结构图
			while(!queen.isEmpty())
			{
				int ver=queen.poll();
				count++;
				ArrayList<Integer> tmp=alledges.get(ver);
				if(tmp!=null)
				{
					//对该节点所有邻居节点的入度进行-1，然后判断是否为0,
					//如果为0,则应该入队列
					for(int num:tmp)
					{
						indegree[num]--;
						if(indegree[num]==0)
							queen.offer(num);
					}
				}
			}

			//如果最后拓扑结构中的节点数等于图中的节点数，则不存在环路
			//否则则存在环路
			if(n==count)
				return true;
			else
				return false;

    	}

    }
}
{% endhighlight %}










