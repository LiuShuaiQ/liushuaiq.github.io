# PHP常见问题  

## laravel new <项目名> 报错
```
[ErrorException]                               
  exec() has been disabled for security reasons 
```

解决方案:  打开`php.ini`，搜索`disable_functions`，删掉exec即可，其他类似错误可以一样解决。