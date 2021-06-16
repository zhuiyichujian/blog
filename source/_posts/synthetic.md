---
title: mac根目录下创建文件夹
date: 2021-06-16 14:49:51
tags: [mac]
category: mac
---

修改 /etc/synthetic.conf


    sudo vim /etc/synthetic.conf
添加一行记录(如果有两列需要使用 tab 进行分割，注意空格分割是无效的)，然后重启即可
举例

    bar System/Volumes/Data/bar
将会在根目录下创建 bar 软连接到根目录下的 System/Volumes/Data/bar 目录
具体可参考 man synthetic.conf
