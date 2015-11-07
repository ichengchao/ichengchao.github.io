---
layout: post
title: Git入门
date: 2015-11-07 10:54
tags:
  - tech
  - git

---

![](http://www.chengchao.name/resource-container/image/git.jpg)

###环境准备
想要学习git,就必须先有个git环境.最有名的当然就是Github.不过访问速度时好时坏,所以建议用一个国内的git仓库.我推荐的是oschina: [http://git.oschina.net/](http://git.oschina.net/) 使用方式跟Github几乎一样,速度快了很多.btw:他家的maven仓库的速度也不错.[http://maven.oschina.net/home.html](http://maven.oschina.net/home.html)
申请好之后,导入ssh公钥就可以开始测试了.


###配置

```
git config --global user.name "charles"
git config --global user.email "charles@chengchao.name"
git config --global push.default simple
git config --global http.postBuffer 10485760 #上传最大10MB

#别名
git config --global alias.s status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.b branch
```

常用配置命令:

```
#查看配置,一般在~/.gitconfig
git config -l
#删除配置
git config --global --unset #key#
```

###使用
基本的使用命令,有很多地方都有,这边就不做介绍了.下面我通过一个测试项目来模拟一个真实的开发过程.
首先在git仓库新建一个项目,暂且叫`git-test`.  
第一步就是先导出到本地.命令很简单,就是git clone,可以选择http和ssh两种方式,我使用的ssh.由于之前已经把公钥导入到git仓库中.所以后续的操作都不用再输入用户名和密码了.  
`git clone git@git.oschina.net:ichengchao/git-test.git`  
有个比较特殊的文件需要简单介绍一下`.gitignore`,该文件用于忽略一些文件或者文件夹,这个文件或者文件夹就不会提交到仓库中.简单的语法如下:

```
#忽略所有.class结尾的文件
*.class

#不包含vip.class
!vip.class

#忽略根目录下的build文件夹,会忽略/build,但不会忽略/tmp/build目录
/build/

#忽略所有target目录,会同时忽略/target和/tmp/target目录
target/
```


