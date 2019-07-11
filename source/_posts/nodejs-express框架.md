---
title: 安装nodejs并搭建express框架
date: 2016-12-20 15:25:16
tags: [nodejs,express]
category: nodejs
thumbnail: /images/thumb_node.png
---

## 一、安装node
　直接到[官网](http://nodejs.cn/)下载安装。如果是macos,直接下载安装包安装就可以了。linux系统可以下载源码安装也可以下载已经编译好的包。
　![node](/images/node_01.png)
　
### 下载编译好的文件
* 下载
　　选择相应的版本，下载到本地再传到服务器（这个比较笨……），当然作为程序员肯定喜欢用命令行搞定一切，直接复制下载地址（这个应该难不倒你，实在不行用查看网页源代码呀），在服务器上下载即可。
　　 
`wget https://nodejs.org/dist/v6.2.0/node-v6.2.0-linux-x64.tar.gz`
* 解压
`tar -xvvf node-v6.2.0-linux-x64.tar.gz`
* 添加环境变量
可以直接把bin目录添加到环境变量path中，也可以选择软链接到/usr/local/bin
`sudo ln -s ~/node-v6.2.0-linux-x64/bin/npm  /usr/local/bin/npm`
`sudo ln -s ~/node-v6.2.0-linux-x64/bin/node  /usr/local/bin/node`

### 源码安装
* 下载源码
`wget https://nodejs.org/dist/v6.2.0/node-v6.2.0.tar.gz`
* 安装
`tar -xvf node-v6.2.0.tar.gz`
`cd node-v6.2.0`
`make && make install`
## 二、搭建express

> 　express是一个基于 Node.js 平台，快速、开放、极简的 web 开发框架。
* 安装

```
mkdir express
cd express
npm install express --save
```
检验是否安装成功
`$ express --version`
> 在mac上一点问题也没有，可以使用，结果在linux上发现没有这个命令，还是去查看下资料吧。原来express4.X的有一些变化，4.x版本中将命令工具单独分出来了（详见[express github](https://github.com/expressjs/generator)）,所有要先按装express-generator，否则创建项目时，会提示express命令没找到。

`$ npm install -g express-generator #需先安装express-generator`

* 使用

```
express -e test #express的默认模版采用jade，若需要ejs模版支持，加上-e选项
npm install #需要等待一段时间，因为需要获取很多的库文件
npm start
express@0.0.0 start /opt/local/share/nginx/html/express
node ./bin/www
```
访问http://localhost:3000/ 就可以了


　　 

