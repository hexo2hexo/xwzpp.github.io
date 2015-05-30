---
layout: post
title:  LeetCode-Word Search II
description: "Word Search II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking,Trie]
duoshuo: true
---
##题目
####Word Search II
>  Given a 2D board and a list of words from the dictionary, find all words in the board.

>Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

>For example,
>Given words = `["oath","pea","eat","rain"]` and board =
>
	[
	  ['o','a','a','n'],
	  ['e','t','a','e'],
	  ['i','h','k','r'],
	  ['i','f','l','v']
	]

>Return ["eat","oath"].

>######Note:
>You may assume that all inputs are consist of lowercase letters a-z.

>######click to show hint.

>You would need to optimize your backtracking to pass the larger test. Could you stop backtracking earlier?

>If the current candidate does not exist in all words' prefix, you could stop backtracking immediately. What kind of data structure could answer such query efficiently? Does a hash table work? Why or why not? How about a Trie? If you would like to learn how to implement a basic trie, please work on this problem: Implement Trie (Prefix Tree) first.


<!-- more -->
	
##解题思路
该方法首先想到的思路是与[Word Search][1]相同，但是在测试数据集中存在一个特别大的用例，会造成结果的超时。因此需要进行优化。

首先我们想是不是每个单词都需要从头开始来进行查找呢，显然不是，我们会发现有些单词会存在公共的前缀，因此我们可以通过构建一个`trie`树，然后将需要查找的单词都加入其中，然后对网格进行深度优先搜索，并对当前已经访问过的字母序列进行判断是否在trie树中有这个前缀的单词存在，如果存在，则将该单词加入结果集中，否则没有这个前缀，说明当前位置不需要继续深度搜索下去。

##算法代码
代码采用JAVA实现：
超时的方法
{% highlight java %}
public class Solution {
    public ArrayList<String> findWords(char[][] board, String[] words) {
        //可以对Array中的每一个单词进行查找，如果能够找到，则加入结果List中
        ArrayList<String> result=new ArrayList<String>();
        if(words==null || words.length==0) return result;
        if(board==null || board.length==0 || board[0].length==0) return result;

        for(String word:words){
        	boolean re=findWord(board,word);
        	if(re==true)
        		result.add(word);
        }

        return result;
    }

    //查找一个单词
    public boolean findWord(char[][] board,String word)
    {
    	if(word==null || word.length()==0) return true;

    	boolean[][] used=new boolean[board.length][board[0].length];
    	for(int i=0;i<board.length;i++)
    		for(int j=0;j<board[0].length;j++)
    		{
    			if(search(board,word,0,i,j,used))
    				return true;
    		}
    	return false;
    }
    //采用深度优先搜索的方法进行查找
    public boolean search(char[][] board,String word,int index,int i,int j,boolean[][] used)
    {
    	if(index==word.length())
    		return true;

    	if(i<0 || j<0 || i>=board.length || j>=board[0].length || used[i][j]==true || board[i][j]!=word.charAt(index))
    		return false;

    	used[i][j]=true;
    	//对四个方位进行搜索，只要满足一个方位找到即可
    	boolean res=search(board,word,index+1,i-1,j,used) || search(board,word,index+1,i+1,j,used) || search(board,word,index+1,i,j-1,used) || search(board,word,index+1,i,j+1,used);
    	//需要重置使用标记
    	used[i][j]=false;

    	return res;
    }
}
{% endhighlight %}

通过构建trie树进行优化的方法
{% highlight java %}
//优化的方法
public class Solution {
    public ArrayList<String> findWords(char[][] board, String[] words) {
         //这边设定一个hashset，防止一个单词被重复的加入
        ArrayList<String> re=new ArrayList<String>();
    	HashSet<String> result=new HashSet<String>();
        if(words==null || words.length==0) return re;
        if(board==null || board.length==0 || board[0].length==0) return re;

        Trie tr=new Trie();
        for(String word:words){
        	tr.insertWord(word);
        }
        boolean[][] used=new boolean[board.length][board[0].length];
        for(int i=0; i<board.length; i++) {  
            for(int j=0; j<board[0].length; j++) {  
                search(board, used, tr, i, j, new StringBuilder(), result);  
            }  
        }  
       
        for(String hs:result)
          re.add(hs);
        return re;
   }

   //sb中记录深度过程中访问过的节点，然后便于前缀搜索
   public void search(char[][] board,boolean[][] used,Trie tr,int i,int j,StringBuilder sb,HashSet<String> re){
   		if(i<0 || j<0 || i>=board.length || j>=board[0].length || used[i][j]) return;

   		used[i][j]=true;
   		sb.append(board[i][j]);
   		String s=sb.toString();
   		//只有存在这个单词前缀的时候，才需要进行深度下去，否则不需要深度下去了，因为没有意义，这里进行了剪枝
   		if(tr.searchPrefix(s)){
   			if(tr.searchWord(s)) re.add(s);
   			//从四个方面进行搜索
   			search(board,used,tr,i-1,j,sb,re);
   			search(board,used,tr,i+1,j,sb,re);
   			search(board,used,tr,i,j-1,sb,re);
   			search(board,used,tr,i,j+1,sb,re);
   		}
   		//回溯上去进行还原工作
   		sb.deleteCharAt(sb.length()-1);
   		used[i][j]=false;
   }
}

//trie树中节点的结构
class TrieNode{
	char content;
	boolean isEnd;
	LinkedList<TrieNode> children;

	public TrieNode(){
		this.content=' ';
		this.isEnd=false;
		this.children=new LinkedList<TrieNode>();
	}

	public TrieNode(char content){
		this.content=content;
		this.isEnd=false;
		this.children=new LinkedList<TrieNode>();
	}

	//检查当前节点的孩子节点是否存在需要查找的字母
	public TrieNode subNode(char c){
		if(children!=null){
			for(TrieNode child:children)
				if(child.content==c)
					return child;
		}
		return null;
	}
}

class Trie{
	TrieNode root;

	public Trie(){
		root=new TrieNode();
	}

	//插入单词
	public void insertWord(String word){
		if(searchWord(word)==true) return;
		TrieNode current=root;
		for(int i=0;i<word.length();i++){
			TrieNode node=current.subNode(word.charAt(i));
			if(node==null)
			{
				current.children.add(new TrieNode(word.charAt(i)));
				current=current.subNode(word.charAt(i));
			}else{
				current=node;
			}
		}
		current.isEnd=true;

	}

	//查找单词

	public boolean searchWord(String word){
		TrieNode current=root;
		for(int i=0;i<word.length();i++){
			TrieNode node=current.subNode(word.charAt(i));
			if(node==null)
				return false;
			else
				current=node;
		}	

		if(current.isEnd)
			return true;
		else
			return false;
	}
	//查找前缀

	public boolean searchPrefix(String word){
		TrieNode current=root;
		for(int i=0;i<word.length();i++){
			TrieNode node=current.subNode(word.charAt(i));
			if(node==null)
				return false;
			else
				current=node;
		}
		return true;
	}
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Word-Search.html












