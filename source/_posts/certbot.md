---
title: 使用pip安装Certbot
---

## 此种方法比较简单，最好先创建一个Python虚拟环境，然后再安装Certbot

### 安装虚拟环境软件包（针对于Python2.7）

``` bash
$ sudo yum install python-virtualenv
```

### 创建虚拟环境

``` bash
$ sudo virtualenv /usr/local/python-certbot
```

### 激活虚拟环境

``` bash
$ source /usr/local/python-certbot/bin/activate
```

### 首先更新pip

``` bash
$ pip install --upgrade pip
```

### 安装Certbot

``` bash
$ pip install certbot
```

### 安装Certbot Nginx插件：

``` bash
$ pip install certbot-nginx
```

### 获取Let's Encrypt证书,同时配置Nginx服务器

``` bash
$ sudo certbot --nginx
```