---
layout: post
title:  "Docker进阶知识 -- Docker Composer"
date:   2020-03-23 22:24:19 +0800
categories: Docker
---
# Docker Composer 

----
## 定义

Compose 是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务。

----
## 安装

Linux 上我们可以从 Github 上下载它的二进制包来使用，最新发行的版本地址：https://github.com/docker/compose/releases。

```shell
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

测试是否安装成功:  

```shell
$ docker-compose --version
cker-compose version 1.24.1, build 4667896b
```

----
## 使用

**使用步骤**:  
- 使用 Dockerfile 定义应用程序的环境。
- 使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。
- 最后，执行 docker-compose up 命令来启动并运行整个应用程序。

### 准备环境
创建测试目录： 
```shell
$ mkdir composetest
$ cd composetest
```

在测试目录中创建一个名为 app.py 的文件，并复制粘贴以下内容：
```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)


def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)


@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

在此示例中，redis 是应用程序网络上的 redis 容器的主机名，该主机使用的端口为 6379。

在 composetest 目录中创建另一个名为 requirements.txt 的文件，内容如下：

```txt
flask
redis
```

### 创建Dockerfile
在 composetest 目录中，创建一个名为的文件 Dockerfile，内容如下：

```shell
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
CMD ["flask", "run"]
```

### 创建docker-compose.yml
在测试目录中创建一个名为 docker-compose.yml 的文件，然后粘贴以下内容：

```yml
# yaml 配置
version: '3'
services:
  web:
    build: .
    ports:
     - "5000:5000"
  redis:
    image: "redis:alpine"
```

### 使用 Compose 命令构建和运行您的应用

在测试目录中，执行以下命令来启动应用程序：

```shell
docker-compose up
```

该 Compose 文件定义了两个服务：web 和 redis。

- web：该 web 服务使用从 Dockerfile 当前目录中构建的镜像。然后，它将容器和主机绑定到暴露的端口 5000。此示例服务使用 Flask Web 服务器的默认端口 5000 。
- redis：该 redis 服务使用 Docker Hub 的公共 Redis 映像。

----
## yml指令

### version

指定本 yml 依从的 compose 哪个版本制定的。


### build

指定为构建镜像上下文路径：

例如 webapp 服务，指定为从上下文路径 ./dir/Dockerfile 所构建的镜像：

```yml
version: "3.7"
services:
  webapp:
    build: ./dir
```


**[更多指令参考](https://www.runoob.com/docker/docker-compose.html)**