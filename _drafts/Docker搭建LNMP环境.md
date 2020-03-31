# Docker搭建LNMP环境
---

## 拉取相关镜像

- nginx镜像   
`docker pull nginx:1.10.3`    

- mysql镜像   
`docker pull mysql:5.6`    

- PHP镜像   
`docker pull php:7.0-fpm`    

---

## 配置启动相关镜像    

### 启动mysql
`docker run -d -p 3307:3306 -e MYSQL_ROOT_PASSWORD=xy123456 --name xy_mysql mysql:5.6`    

**参数说明**:
* -d 让容器在后台运行    
* -p 添加主机到容器的端口映射   
* -e 设置环境变量，这里是设置mysql的root用户的初始密码，这个必须设置    
* –name 容器的名字，随便取，但是必须唯一    

### 启动PHP
`docker run -d -v /var/nginx/www/html:/var/www/html -p 9000:9000 --link xy_mysql:mysql --name xy_phpfpm php:7.0-fpm `    

**参数说明**:
* -d 让容器在后台运行    
* -p 添加主机到容器的端口映射    
* -v 添加目录映射，即主机上的/var/nginx/www/html和容器中/var/www/html目录是同步的    
* –name 容器的名字    
* –link 与另外一个容器建立起联系，这样我们就可以在当前容器中去使用另一个容器里的服务。    

**安装PHP模块**:     
进入PHP容器执行：`docker exec -it <容器ID> /bin/bash `       
安装mysql模块: `docker-php-ext-install pdo_mysql`       

**查看PHP拓展模块**:    
`php  -m`    


### 启动nginx

```shell
docker run -d -p 80:80 --name xy_nginx\ 
-v /var/nginx/www/html:/var/www/html\
--link xy_phpfpm:phpfpm --name xy_nginx nginx:1.10.3
```

**参数说明**:

* -d 让容器在后台运行    
* -p 添加主机到容器的端口映射    
* -v 添加目录映射,这里最好nginx容器的根目录最好 写成和php容器中根目录一样。但是不一点非要一模一样,如果不一样在配置nginx的时候需要注意    
* –name 容器的名字    
* –link 与另外一个容器建立起联系    

**配置PHP**:    
`docker exec -ti xy_nginx /bin/bash`    

在/etc/nginx目录下修改php配置文件：    
```
location ~ \.php$ {
        root           /var/www/html;
        fastcgi_index  index.php;
        fastcgi_pass   phpfpm:9000;//这里改成我们之前--link进来的容器，也可以直接用php容器的ip
	    fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;//如果你的根目录和php容器的根目录不一样，这里的$document_root需要换成你php下的根目录，不然php就找不到文件了
        include        fastcgi_params;                               
    }
```

----
> 参考资料：<https://blog.csdn.net/xy752068432/article/details/75975065>   
<https://learnku.com/articles/25412>