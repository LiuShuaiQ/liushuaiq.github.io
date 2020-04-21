# PHP常见问题  

## laravel new <项目名> 报错
```
[ErrorException]                               
  exec() has been disabled for security reasons 
```

解决方案:  打开`php.ini`，搜索`disable_functions`，删掉exec即可，其他类似错误可以一样解决。

## composer install报错

```shell
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover

In ProviderRepository.php line 208:
                                                          
  Class 'SwooleTW\Http\LaravelServiceProvider' not found  
                                                          

Script @php artisan package:discover handling the post-autoload-dump event returned with error code 1
```

**原因**: php模块缺少 laravel-swoole

检查php是否安装swoole模块: 

`php -m | grep swoole`

**解决方案**: 

安装 laravel-swoole    
`composer require swooletw/laravel-swoole`


## composer install报错   

```shell
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover

In EncryptionServiceProvider.php line 44:
                                                     
  No application encryption key has been specified.  
                                                     

Script @php artisan package:discover handling the post-autoload-dump event returned with error code 1
```

**原因**: 项目文件夹下没有.env文件

**解决**: 
1. .env.example 改名使用命令 copy 修改为 .env

2. 使用命令 php artisan key:generate  获取密码，自动保存到 .env

3. 将密码复制到config/app.php 中的key里面