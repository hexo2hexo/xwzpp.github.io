---
layout: post
title:  LeetCode-Implement Trie (Prefix Tree)
description: "Implement Trie (Prefix Tree)"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Data Structure,Trie]
duoshuo: true
---
##题目
####Implement Trie (Prefix Tree)
>Implement a trie with insert, search, and startsWith methods.

>####Note:
>You may assume that all inputs are consist of lowercase letters a-z.

<!-- more -->
	
##解题思路
该题是实现trie树。   
Trie，又称单词查找树或键树，是一种树形结构。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。  
它有3个基本性质：   
       
* 根节点不包含字符，除根节点外每一个节点都只包含一个字符。     
* 从根节点到某一节点，路径上经过的字符连接起来，为该节点对应的字符串。     
* 每个节点的所有子节点包含的字符都不相同。 

此外，每个节点存在一个判断其是否是一个单词结尾的标记，用来表明该trie树中包含该单词。因此我们首先需要定义节点的数据结构。      
节点的属性主要包含以下几点：

* 节点字符内容
* 节点是否为一个单词结束的标记
* 该节点的所有的孩子节点
   
trie树的定义可以参考[该网址][1]。
##算法代码
代码采用JAVA实现：
{% highlight java %}
class TrieNode {
    // Initialize your data structure here.
     char content; //节点内容
     boolean isEnd;//是否为一个单词的结尾
     LinkedList<TrieNode> childNode;//该节点所有的孩子节点

    //此为根结点的构造函数，根结点不包含任何内容
    public TrieNode() {
        this.content=' ';
        this.isEnd=false;
        this.childNode=new LinkedList<TrieNode>();
    }

    //此为包含内容节点的构造函数
    public TrieNode(char content)
    {
        this.content=content;
        this.isEnd=false;
        this.childNode=new LinkedList<TrieNode>();
    }

    //在该节点的孩子节点查找某一个节点
    public TrieNode subNode(char content)
    {
        if(childNode!=null){
            for(TrieNode node:childNode)
            {
                if(node.content==content)
                    return node;
            }
        }
        return null;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {

        if(search(word)==true) return;
        TrieNode current=root;
        for(int i=0;i<word.length();i++)
        {
            //需要在current节点的孩子节点中查找是否存在该字符的节点。如果不存在则需要插入，否则直接往下遍历。
            TrieNode node=current.subNode(word.charAt(i));
            if(node==null){
                current.childNode.add(new TrieNode(word.charAt(i)));
                node=current.subNode(word.charAt(i));
            }
            current=node;
        }
        //最后需要定义单词结束标记，表明该trie树包含该单词
        current.isEnd=true;   
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {

        TrieNode current=root;
        for(int i=0;i<word.length();i++)
        {
            TrieNode node=current.subNode(word.charAt(i));
            if(node==null)
                return false;
            current=node;
        }

        //虽然有这个单词序列，但是需要判断其结束标记是否为true，以便得知其在该trie中。
        if(current.isEnd==false)
            return false;
        else
            return true;

        
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode current=root;
        for(int i=0;i<prefix.length();i++)
        {
            TrieNode node=current.subNode(prefix.charAt(i));
            if(node==null)
                return false;
            current=node;
        }
        return true;
        
    }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
{% endhighlight %}

[1]:http://blog.csdn.net/beiyetengqing/article/details/7856113










