---
layout: post
title: "redis安装部署-Linux"
tag: redis
---   

# redis设置

---
## 下载

<https://redis.io/download>

## 安装

切换到安装目录

1. 解压  
`tar -zxf redis-x.y.z.tar.gz`   
重命名  
`mv redis-x.y.z redis`

2. 编译&&安装   
    ```shell
    cd redis
    make 
    make install
    ```

---
## 部署   

为了方便管理，将Redis文件中的conf配置文件和常用命令移动到统一文件中

1. 创建bin和etc文件  
    ```shell
    mkdir etc
    mkdir bin
    ```

2. 回到刚刚安装目录，找到redis.conf
`mv redis.conf /usr/local/redis/etc/`

3. 进入src目录，移动mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-rdb redis-cli redis-server到/usr/local/redis/bin/    
`mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-rdb redis-cli redis-server /usr/local/redis/bin/`

4. 配置环境变量   
配置`/usr/local/redis/bin`到PATH中，全局的为: `/etc/profile`,配置过程就不多说了。

---
## 启动

$: `redis-server`

---
---
## 参考blog

<https://www.cnblogs.com/zdd-java/p/10288734.html>