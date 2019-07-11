---
title: php7编译mysqlnd扩展解决openssl找不到的问题
date: 2018-01-9 16:38:14
tags: [c,php]
category: php源码
---
## 编译php和mysqlnd扩展
### phpbrew的坑?

　　前几天看到phpbrew，觉得挺方便的，就想用phpbrew装个7.2.4，结果装的时候一直报evp.h找不到，查了下是openssl没找到。然后装好了openssl,再装php：

`sudo yum install -y openssl.x86_64 openssl-devel.x86_64`

`phpbrew install 7.2.4 +default +openssl`

一切都很顺利，还有好多扩展没有装，在装mysqlnd的时候又出了问题：
![img](/images/php_mysqlnd.png)
明明已经装好了openssl，结果还是找不到，指定openssl的路径也不对，索性一次性编译:

`phpbrew install 7.2.4 +default +dbs`

也很顺利，一次性成功，暂时推断是用phpize编译mysqlnd扩展的时候会出问题。

### 溯源

为了验证，下载php7.2.4的源码进行编译安装：

```
./buildconf –force
./configure --prefix=/usr/local --program-suffix=7 --with-config-file-path=/usr/local/etc/php7 --with-config-file-scan-dir=/usr/local/etc/php7/conf.d/ --enable-fpm --enable-posix --enable-pcntl --enable-sysvshm --enable-mysqlnd --libdir=/usr/local/lib/php7 --includedir=/usr/local/include/php7 --with-pear --enable-mbstring --with-mysql-sock=/tmp/mysql.sock --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --enable-sockets --with-curl=/usr/include/curl --with-gd --enable-phar --sysconfdir=/usr/local/etc/php7 --enable-pdo --with-openssl-dir=/usr
make && make install
```

也没问题，然后单独编译mysqlnd
```
cd ext/mysqlnd
cp config9.m4 config.m4
phpize7
./configure --with-php-config=php-config7
```
果然还是同样的错误：

configure: error: Cannot find OpenSSL’s 
打开configure文件查看报错的地方

![img](/images/php_mysqlnd1.png)

看脚本，如果PHP_OPENSSL_DIR=yes，会默认从/usr/local/ssl、/usr/local、/usr /usr/local/openssl这几个目录找openssl。
在编译前执行下面的命令可以解决问题：

`export PHP_OPENSSL_DIR=yes`

