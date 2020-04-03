---
layout: post
title: "从零开始学Laravel之初始化项目"
tag: PHP Laravel
---   

# 从零开始学Laravel之初始化项目  

## 准备条件  

确保服务器达到如下要求：    
- PHP >= 7.1.3
- OpenSSL PHP 拓展
- PDO PHP 拓展
- Mbstring PHP 拓展
- Tokenizer PHP 拓展
- XML PHP 拓展
- Ctype PHP 拓展
- JSON PHP 拓展
- BCMath PHP 拓展
- composer已安装

## 安装和配置    

- 通过composer进行安装:     
`composer global require laravel/installer`    

- 设置环境变量:   
    * macOS: `$HOME/.composer/vendor/bin`  
    * GNU / Linux 发行版: `$HOME/.config/composer/vendor/bin`  
    或者`$HOME/.composer/vendor/bin`     
    * Windows: `%USERPROFILE%\AppData\Roaming\Composer\vendor\bin`    


- 建立项目    
1. `laravel new blog`   
2. `composer create-project --prefer-dist laravel/laravel blog "5.8.*"`  

- 相关配置   
1. 路径配置   
安装完 Laravel 之后，你应该配置你的 web 服务的文档目录指向 public 路径。该路径下的 index.php 文件作为进入应用的所有 HTTP 请求的前端控制器。  
2. 权限配置  
在安装 Laravel 后，你可能需要配置一些权限。 storage 和 bootstrap/cache 目录在你的 web 服务下应该是可写的权限，否则 Laravel 将无法运行。如果你用的是 Homestead 虚拟机，这些权限应该已经设置好了。    
3. 应用秘钥  
安装好 Laravel 之后的下一步是设置你的应用密钥为随机字符串。如果你通过 composer 或者 Laravel 安装器安装的，这个密钥已经通过 `php artisan key:generate` 命令为你设置好了。     
通常，这个字符串应该是 32 个字符长度。这个密钥将会设置在环境变量文件 .env 中。如果你还没有将 .env.example 文件重命名为 .env 文件，你需要将 .env.example 文件重命名为 .env 文件。如果应用密钥还没有设置，你的用户会话和其他的加密数据将会不安全！   
 
