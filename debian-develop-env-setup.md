# debian 9 开发环境搭建


	
## 1、更新软件源

> + 更新软件源，使用网易的源（保持 apt-get install 安装到较新的软件）

> + 编辑```/etc/apt/sources.list```，加入以下代码段

```code
deb http://mirrors.163.com/debian/ stretch main non-free contrib
deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib
deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib
deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib
deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib

```





## 2、更新源数据

```code
apt-get update
```




## 3、安装 ```vim``` 文字编辑器

```code
apt-get install vim
```


## 4、安装 ```rime```

> + 安装 ```rime``` 中文输入法

> + 官网：[http://rime.im/](http://rime.im/)

> + 安装方法：[https://github.com/rime/home/wiki/RimeWithIBus](https://github.com/rime/home/wiki/RimeWithIBus)

> + 配置文件在```~/.config/ibus/```下

debian/ubuntu系可使用如下方法

```code
sudo apt-get install ibus-rime
```

配置说明：
> + 不要使用root用户操作

> + 进入```Region & Language``` > ```Input Sources``` > ```Add```(查找)添加中文输入法

> + 在```终端```执行```ibus-setup```，然后依次进入```Input Method```>```Add```添加中文的```RIME```输入法

> + 这里需要注意查询终端是否有```dconf```错误信息

> + 出现上诉问题，我忘了解决方法了。。。

> + 完事可能需要重启电脑，因为输入法始终无法使用



## 5、安装 ```git```

```code
sudo apt-get install git
```

设置认证信息存储(通过https拉去的代码，不需要重复输入用户名/密码进行验证)：
```code
git config --global credential.helper store
```

文件diff时忽略权限变动带来的文件变动：
```code
git config --global core.filemode false
```

> + ```git```初始设置：[https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

> + 生成 ```ssh-key``` [https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)




## 6、安装 ```svn```

```code
sudo apt-get install subversion
```




## 7、安装 ```c/c++``` 编译器

> + 在编译很多源码时都需要

```code
apt-get install gcc g++
```



## 8、安装 ```redis```

```code
wget http://download.redis.io/releases/redis-4.0.2.tar.gz
tar -zxf redis-4.0.2.tar.gz
cd redis-4.0.2
make
make install
```



## 9、安装 ```openssl```

> + ```curl```，```nginx-ssl``` 等需要依赖 ```openssl```

```code
git clone https://github.com/openssl/openssl.git
cd openssl/
./config
make
make test
make install
```



## 10、安装 ```pcre```

> + ```nginx``` 需要依赖 ```pcre```

```code
wget https://ftp.pcre.org/pub/pcre/pcre-8.40.tar.gz
tar -zxf pcre-8.40.tar.gz
cd pcre-8.40
./configure
make
make check
make install
```




## 11、安装 ```zlib```

> + ```nginx``` 需要依赖 ```zlib```

```code
wget http://zlib.net/zlib-1.2.11.tar.gz
tar -zxf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make
make install
```





## 12、安装 ```nginx```

```code
wget http://nginx.org/download/nginx-1.12.2.tar.gz
tar -zxf nginx-1.12.2.tar.gz
cd nginx-1.12.2
./configure --with-http_ssl_module --with-pcre
make
make install
```




## 13、安装 ```libaio```

> + ```mysql``` 需要依赖```libaio.so.1```

```code
apt-get install libaio-dev libaio1
```




## 14、安装 ```mysql```

> + 这里的 ```mysql``` 指 ```mariadb```

> + 具体安装可参考 ```INSTALL-BINARY``` 文件

```code
wget https://downloads.mariadb.org/interstitial/mariadb-10.2.10/bintar-linux-x86_64/mariadb-10.2.10-linux-x86_64.tar.gz?serve -O mariadb-10.2.10-linux-x86_64.tar.gz
tar -zxf mariadb-10.2.10-linux-x86_64.tar.gz
mv mariadb-10.2.10-linux-x86_64 mysql
mv mysql/ /usr/local/
cd /usr/local/mysql/
groupadd mysql
useradd -g mysql mysql
chown -R mysql .
chgrp -R mysql .
scripts/mysql_install_db --user=mysql
chown -R root .
chown -R mysql data
cp bin/mysql bin/mysqld_safe bin/mysqldump  /usr/local/bin/
```






## 15、安装 ```php```所需库

```code
apt-get install autoconf automake libtool re2c flex bison
```



## 16、安装 ```curl```

> + ```php``` 需要依赖 ```curl```

```code
git clone https://github.com/curl/curl.git
cd curl/
./buildconf
./configure --with-ssl
make
make install
```





## 17、安装 ```libxml2```

> + ```php``` 需要依赖 ```libxml2```

```code
apt-get install libxml2 libxml2-dev
```




## 18、安装 ```php```

> + 下载页面：[http://php.net/downloads.php](http://php.net/downloads.php)

> + 安装以及配置具体参考：[http://php.net/manual/en/install.unix.nginx.php](http://php.net/manual/en/install.unix.nginx.php)

```code
wget http://am1.php.net/get/php-7.1.11.tar.gz/from/this/mirror -O php-7.1.11.tar.gz
tar -zxf php-7.1.11.tar.gz
cd php-7.1.11
./configure --enable-fpm --with-curl --with-pdo-mysql --with-mysqli --enable-mbstring --enable-ftp --enable-exif
make
make install
```


## 注意
> + 遇到缺失动态链接库什么的，先使用 ```apt-cache``` 搜索，然后分别安装
> + 上诉大部分可解决，不行的话，再使用搜索引擎
> + 笔记本安装 ```debian``` 会出现无线网卡不识别情况，请参考 [https://wiki.debian.org/iwlwifi#Installation](https://wiki.debian.org/iwlwifi#Installation) 下载网卡驱动包或者使用有线进行在线安装网卡驱动



[丸]






