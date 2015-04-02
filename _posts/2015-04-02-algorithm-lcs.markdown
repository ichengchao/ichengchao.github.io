---
layout: post
title: [算法]最长公共子序列
date: 2015-04-02 23:49
tags:
  - java
  - tech
  - algorithm
---

### 背景 ###
之前做项目,需要做一个文本文件的在线diff.其中用到的就是LCS算法.
今天心血来潮,打算用java写个示例

### LCS算法介绍 ###
[维基百科的解释](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem)
  
网上的介绍比较多,不细讲  
就是用一个二维矩阵来记录两个字符串中所有位置的匹配情况,若是匹配则为1,否则为0.  
然后求出对角线最长的1序列，其对应的位置就是最长匹配子串的位置.  
当然如果扩展成一个文本文件的话,就是一行一个单位.  
这里就不贴图了,直接google,或者看wikipedia里面的图.

### 代码示例 ###
<script src="https://gist.github.com/ichengchao/517721eed0cc29e7c2a5.js"></script>