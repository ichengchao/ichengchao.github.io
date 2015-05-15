---
title: 从wordpress到jekyll
layout: post
date: 2015-02-05 17:49
tags:
  - tech
  - blog
  
---

![jekyll](http://chengchao.name/resource-container/image/logo-jekyll.png)

## 起因
我也算是比较早接触blog的,那是没有新浪博客(当然现在也快没了),当时觉得blog都是高大上的人写的.
直到后来越来越多的人都开始写了,才意识到是不是自己也可以开个博客.
于是开始在各个博客系统间转悠,从blogcn,到网易个人空间,一直觉得不满意.
想想是不是应该买虚拟主机自己搞,但由于当时的虚拟主机又贵又不好用于是作罢.
再后来用了blogger,感觉很满意,用邮件发文也很方便.断断续续坚持了大半年,后来被GFW封了,然后就没有然后了.
就这样很长一段时间就没再写blog,直到阿里云开始卖虚机了,我抱着试试看的心态买了一台.
搭了mysql,nginx,wordpress于是又开始折腾.用自己的主机感觉还真不一样.换主题,装插件,玩得不亦乐乎.
有一次偶然的机会看到了[jekyll](http://jekyllrb.com/),号称是`为coder而生的blog`.于是又开始折腾.当然类似的还有很多,比如[Hexo](https://hexo.io/)  
  

## 行动
怎么搭建的就不说了,网上多的是,没有github账号的申请一下.然后按照教程一步步下去就ok了.
最重要的还是迁移wordpress的数据.
虽然jekyll本身就提供了原生的迁移工具,但我觉得还是太麻烦了.
上网搜寻了一下,找到一个很轻量级的从wordpress的xml文件生成jekyll的markdown文件.
轻量级迁移工具:[wpXml2Jekyll](https://github.com/theaob/wpXml2Jekyll),只提供了windows版本.
基本不用改动就能用了.当然像语法高亮这种还是需要手工调整的.
找了一套简洁的模版,做了些修改就用上了.所有模版的源码在[Github](https://github.com/ichengchao/ichengchao.github.io)上都有.需要的请自取.  
  

## 感受
自从换成jekyll,blog的访问速度提高了很多.基本没有动态渲染的过程.全部静态化.
同时把原来的模本中的一些远程的css和js全部放在自己服务器上,访问速度就更快了.
我跟一般人用jekyll的方式还有一点不太一样,就是一般人都是直接托管在github的page上的.
我除了在github的page外,还在自己服务器上也同步一份.这样访问速度就比直接访问github快多了.
还有一点很重要,就是图片该保存在哪里?原来用wordpress的时候是存在mysql中的.这是workpress自带的附件上传的功能.
但总感觉不是特别爽,用了jekyll就开始寻找允许外链的图床服务.什么百度云,网易相册通通不支持.
后来看到`七牛`有个免费的图床服务,就用了一段时间,感觉还不错,管理界面中还能看到各种各样的访问统计数据.
有天我想为什么不放在自己的服务器上呢.于是就在github上开了一个project专门放图片.然后同步到自己服务器,perfect!
毫不夸张的说,现在这个blog方案是我最满意的,没有之一.要不信你也可以试试！

