---
layout: post
title:  docker学习笔记
date:   2016-08-27 01:08:00 +0800
categories: document
tag: 教程
published: false
---

* content
{:toc}

```bash
#redis
docker run -it --name redis-master -v /User/yongqiangli/code/docker:/data redis /bin/bash
docker run -it --name redis-slave1 --link redis-master:master -v /User/yongqiangli/code/docker:/data redis /bin/bash
docker run -it --name redis-slave2 --link redis-master:master -v /User/yongqiangli/code/docker:/data redis /bin/bash

#应用
docker run -it --name APP1 --link redis-master:db -v ~/Projects/Django/App1:/usr/src/app django /bin/bash
docker run -it --name APP2 --link redis-master:db -v ~/Projects/Django/App2:/usr/src/app django /bin/bash

#HAProxy
docker run -it --name HAProxy --link APP1:APP1 --link APP2:APP2 -p 6301:6301 -v ~/Projects/HAProxy:/tmp haproxy /bin/bash
```
问题
---------------------
#### /var/lib/docker: No such file or directory
>/var/lib/docker 是mac上docker虚拟机位置，docker虚拟机Preferences->File Sharing中的目录为mac机与docker虚拟机的共享目录。docker run 时需-v指定共享目录。