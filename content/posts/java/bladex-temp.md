

+++

title = "BladeX 知识点"
description = "BladeX 知识点"
author = "adeng"
tags = [
    "bladex"
]
date = "2021-04-12"
categories = [
    "Java",
]
menu = "main"

mermaid = true

+++





# 安装



```

# db使用mysql，本机安装版本

docker run -d --name postgresql -e POSTGRESQL_ADMIN_PASSWORD=123456 -v ~/Docker/
  data/postgresql:/var/lib/pgsql/data -p 5432:5432 postgres:11.1

docker run --name mysql -d -p 3306:3306 -v ~/Docker/data/mysql/data:/var/lib/my
  sql -v ~/Docker/data/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=root --
  privileged=true  mysql:5.7.23


# redis
docker run --name bladex_redis -d -p 6379:6379 redis:5.0.3


# sentinel
docker run --name bladex_sentinel -d -p 8858:8858 -d bladex/sentinel-dashboard:1.7.1




```



## nacos



https://nacos.io/zh-cn/docs/quick-start-docker.html





docker-compose -f standalone-derby.yaml up --detach



http://127.0.0.1:3000/login



# 配置



http://localhost:8848/nacos

nacos / nacos



blade.yaml

blade-dev.yaml

blade-flow-dev.yaml ??



http://localhost:8858

sentinel / sentinel













# 问题记录



## 1 nacos无法读取配置

nacos包下载出问题，在project structure里能看到problems，删除本地.m2缓存文件夹解决。









