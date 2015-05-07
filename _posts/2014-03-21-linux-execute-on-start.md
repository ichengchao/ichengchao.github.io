---
layout: post
title: linux开机运行命令
date: 2014-03-21 11:13
author: charles
comments: true
tags:
 - linux
 - tech
---

`sudo vi /etc/rc.local`


我的树莓派的rc.local看起来是这样的:  


```sh
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will &quot;exit 0&quot; on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
# Print the IP address
_IP=$(hostname -I) || true
if [ &quot;$_IP&quot; ]; then
  printf &quot;My IP address is %s\n&quot; &quot;$_IP&quot;
fi

#在这里加入自己的脚本：
printf &quot;hello,my first run&quot;

exit 0
```



