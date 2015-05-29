---
layout: post
title:  LeetCode-Add and Search Word - Data structure design
description: "Add and Search Word - Data structure design"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking,Data Structure,Trie]
duoshuo: true
---
##题目
####Add and Search Word - Data structure design
> Design a data structure that supports the following two operations:
>
	void addWord(word)
	bool search(word)

>search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

>For example:
>
	addWord("bad")
	addWord("dad")
	addWord("mad")
	search("pad") -> false
	search("bad") -> true
	search(".ad") -> true
	search("b..") -> true

>######Note:
>You may assume that all words are consist of lowercase letters a-z.

>click to show hint.   
>You should be familiar with how a Trie works. If not, please work on this problem: Implement Trie (Prefix Tree) first.

<!-- more -->
	
##解题思路
该题的思路与[Implement Trie (Prefix Tree)][1]类似,都是trie树的应用。使用trie树进行单词的查找，是一个比较通用的方法。但是这里在搜索单词的时候需要满足正则表达式的要求，即单词中包含了‘.’。因此需要采用递归的方法进行深度优先搜寻，并进行回溯。

##算法代码
代码采用JAVA实现：
{% highlight java %}
	//定义节点的数据结构
	class TrieNode{
		 char content; //节点内容
		 boolean isEnd; //是否是一个单词的结尾
		 LinkedList<TrieNode> children;//所有的孩子节点

		public TrieNode(){  //根结点无内容的构造方法
			this.content=' ';
			this.isEnd=false;
			this.children=new LinkedList<TrieNode>();
		}

		public TrieNode(char content){  //有内容信息的节点
			this.content=content;
			this.isEnd=false;
			this.children=new LinkedList<TrieNode>();
		}

		//在当前节点的孩子节点中查找是否存在内容为content的节点
		public TrieNode subNode(char content){ 
			if(children!=null){
				for(TrieNode child:children){
					if(child.content==content)
						return child;
				}	
			}
			return null;
		}
	}


public class WordDictionary {

	//定义个单词查找树，就是Trie树

	private TrieNode root;  //根结点

	public WordDictionary(){
		root=new TrieNode();
	}


    // Adds a word into the data structure.
    public void addWord(String word) {
    	if(search(word)==true) return;
    	TrieNode current=root;
    	for(int i=0;i<word.length();i++){
    		TrieNode node=current.subNode(word.charAt(i));
    		if(node==null){ //孩子节点中不存在这个字符，则添加
    			TrieNode newNode=new TrieNode(word.charAt(i));
    			current.children.add(newNode);
    			current=current.subNode(word.charAt(i));
    		}else{
    			current=node;
    		}
    	}
    	current.isEnd=true;//设定单词结束的标记
        
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
    	return helper(root,word,0);
    }

    public boolean helper(TrieNode rootnode,String word,int start){
    	TrieNode current=rootnode;
    	//这是一个递归方法，需要设定递归的出口
    	if(current==null) return false;
    	if(start==word.length() && current.isEnd==true) return true;
    	if(start>=word.length()) return false;

    	if(word.charAt(start)!='.')
    	{	
    		//查找下一个字母，根据当前字母的情况进行递归
    		return helper(current.subNode(word.charAt(start)),word,start+1);
    	}else{
    		//对当前节点中的所有孩子节点进行判断
    		LinkedList<TrieNode> cls=current.children;
			if(cls==null) return false;
			for(TrieNode c:cls)
			{
				boolean re=helper(c,word,start+1);
				if(re==true)
					return true;
			}
			return false;
    	}

    	// for(int i=start;i<word.length();i++){
    	// 	if(word.charAt(i)!='.'){
    	// 		TrieNode node=current.subNode(word.charAt(i));
    	// 		if(node!=null){
    	// 			current=node;
    	// 		}else{
    	// 			return false;
    	// 		}
    	// 	}else{
    	// 		//表示为'.'则需要一个一个尝试了，进行深度优先搜索
    	// 		LinkedList<TrieNode> cls=current.children;
    	// 		if(cls==null) return false;
    	// 		for(TrieNode c:cls)
    	// 		{
    	// 			boolean re=helper(c,word,i+1);
    	// 			if(re==true)
    	// 				return true;
    	// 		}
    	// 		return false;
    	// 	}
    	// }
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Implement-Trie-%28Prefix%20Tree%29.html










