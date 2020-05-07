---
layout: post
title:  "Java诊断工具Arthas简介"
date:   2020-04-10 10:24:19 +0800
categories: Java
---
# Java诊断工具Arthas

## 简介

`arthas` 是Alibaba开源的Java诊断工具。

Arthas支持JDK 6+，支持Linux/Mac/Windows，采用命令行交互模式，同时提供丰富的 Tab 自动补全功能，进一步方便进行问题的定位和诊断。

## 安装

```shell
curl -O https://alibaba.github.io/arthas/arthas-boot.jar
java -jar arthas-boot.jar
```

打印帮助信息
```shell
java -jar arthas-boot.jar -h
```

使用aliyun镜像
```shell
java -jar arthas-boot.jar --repo-mirror aliyun --use-http
```


## 相关文档

[Arthas基础教程](https://alibaba.github.io/arthas/arthas-tutorials?language=cn)


