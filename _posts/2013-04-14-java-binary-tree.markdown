---
layout: post
title: java实现的四则运算解析器
date: 2013-04-14 16:19
tags:
  - java
  - tech
---
学过编译原理的同学都知道有最开始的一步就是词法分析.  
下面就是一次入门级的实践.(看之前需要了解一下什么是二叉树)  

###主要有三个类:###

Node.java 二叉树的java model
NodeType.java 节点的枚举类型,四则运算中有数字和运算符两种
Parser.java 关键类,paser的实现

<script src="https://gist.github.com/ichengchao/ee5f06f0ee03766dc750.js"></script>
