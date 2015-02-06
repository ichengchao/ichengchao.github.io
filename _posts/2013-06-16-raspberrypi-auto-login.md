---
layout: post
title: 树莓派(raspberry pi)自动登录
date: 2013-06-16 11:57
author: charles
comments: true
tags:
 - raspberrypi
 - tech
 
---
<ul>
	<li>sudo vi /etc/inittab</li>
	<li>找到行 1:2345:respawn:/sbin/getty 115200 tty1</li>
	<li>注释这行: #1:2345:respawn:/sbin/getty 115200 tty1</li>
	<li>增加一行 1:2345:respawn:/bin/login -f pi tty1 /dev/tty1 2&gt;&amp;1</li>
	<li>保存并退出,reboot试试.</li>
</ul>
大功告成.终于可以不用外接键盘了.启动后,直接ssh
