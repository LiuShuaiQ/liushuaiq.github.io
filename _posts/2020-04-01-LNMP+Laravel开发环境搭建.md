---
layout: post
title: "LNMP+Laravel开发环境搭建记录"
tag: PHP Laravel
---   

# LNMP+Laravel开发环境搭建记录

--- 

## 准备工作  

- Linux操作系统
- git工具

--- 

## 安装LNMP   

- clone LNMP项目  
`$git clone https://github.com/licess/lnmp`  

- 切换分支  
`$git checkou vx.y`  

- 运行脚本(执行会需要一段时间)  
`$sudo ./install.sh`  

--- 

## 安装php composer和npm

### php composer安装  

```shell
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

设置全局生效    
```shell
mv composer.phar /usr/local/bin/composer
#查看composer版本
composer -V
```

切换镜像    

```shell
composer config -g repo.packagist composer  
 
#恢复到packagist官方源命令
#composer config -g --unset repos.packagist
```

更新composer   

```shell
composer selfupdate
```

### npm安装  

node安装 ，下载地址:    
<https://nodejs.org/en/download/>    

国内下载地址:    
<http://nodejs.cn/download/>   

```shell
$tar xvJf node-v12.16.1-linux-x64.tar.xz
```

更新环境变量:   
```shell
$vi /etc/profile

// 在尾部添加
export PATH=/opt/node-v12.16.1-linux-x64/bin:$PATH
```

生效:    
`$source /etc/profile`

安装cnpm，使用国内镜像:   
```shell
$:npm install express --registry=https://registry.npm.taobao.org
$:npm install -g cnpm --registry=https://registry.npm.taobao.org
```

--- 

## 配置开发项目  

### clone 开发项目

`$git clone <开发项目地址>`  

### 项目的打包

```shell
composer install
cnpm install
npm run prod
```

### 配置nginx  

对于nginx的vhost中加入 `XXX.conf`文件，内容模板:   
```
server
     {
         listen 80;
         server_name api.speedmanager.com;
         index index.php index.html;
         root <项目目录>/public;
         if (!-e $request_filename){
           rewrite (.*) /index.php last;
         }
         location ~ [^/]\.php(/|$)
         {
             fastcgi_pass  unix:/tmp/php-cgi.sock;
             fastcgi_index index.php;
             fastcgi_split_path_info ^(.+\.php)(.*)$;
             fastcgi_param   PATH_INFO      $fastcgi_path_info;
             include fastcgi.conf;
             fastcgi_param PHP_ADMIN_VALUE "open_basedir=<项目的父目录>:/tmp/:/proc/";
         }

}

```

重新加载nginx:    
`nginx -s reload`    

将项目的`storage`和`storage/logs`和`storage/framework/sessions`以及`storage/framework/views`权限设置为777:    
```
chmod 777 storage
chmod 777 logs
chmod 777 sessions
chmod 777 views
```

执行命令:    
`php artisan key:generate`   

---- 

## 常见问题   
----

执行`composer install`报错:   
```
  [Symfony\Component\Process\Exception\RuntimeException]                                   
  The Process class relies on proc_open, which is not available on your PHP installation. 
  ```

  修改`/usr/local/php/etc/php.ini`文件的`disable_functions`配置，去掉`proc_open`项

---

执行`composer install`报错:   
```
  [ErrorException]                                          
  proc_get_status() has been disabled for security reasons  
  ```

  修改`/usr/local/php/etc/php.ini`文件的`disable_functions`配置，去掉`proc_get_status`项

  --- 

  请求目录显示`No input file specified`错误信息:   
  
  1. 对于nginx的*.conf文件中的root路径是否填写正确
  2. 对于nginx的*.conf文件中的open_basedir路径是否填写正确
  3. 默认首页文件不是index.php，修改默认首页文件，并去掉重写规则

  