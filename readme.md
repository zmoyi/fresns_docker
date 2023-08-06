# fresns 基础docker

> 此docker compose只集成了nginx, mysql, redis
> 如需集成其他镜像如mongoDB，请参考[**Laradock**](https://laradock.io/)
## 使用

```shell
git clone https://github.com/zmoyi/fresns_docker.git

cp .env.example .env
```
## .env 配置文件
```
# 卷驱动
VOLUMES_DRIVER=local

# 为所有存储系统选择您机器上的存储路径
DATA_PATH_HOST=./fresns_data

# 本地文件地址(开发使用)
# LOCAL_FILE_PATH=./app_fresns
LOCAL_FILE_PATH=app

# 工作目录
APP_PATH=/www/app/

# 工作时区
WORKSPACE_TIMEZONE=UTC-8

# mysql
MYSQL_DATABASE=default
MYSQL_USER=default
MYSQL_PASSWORD=secret
MYSQL_PORT=3306
MYSQL_ROOT_PASSWORD=root
MYSQL_ENTRYPOINT_INITDB=./mysql/docker-entrypoint-initdb.d

# redis
REDIS_PORT=6379
REDIS_PASSWORD=secret_redis

# nginx
NGINX_HOST_HTTP_PORT=80
NGINX_HOST_HTTPS_PORT=443
NGINX_HOST_LOG_PATH=./logs/nginx/
NGINX_SITES_PATH=./nginx/sites/
NGINX_PHP_UPSTREAM_CONTAINER=fresns
NGINX_PHP_UPSTREAM_PORT=9000
NGINX_SSL_PATH=./nginx/ssl/

# 指向主机上应用程序代码的路径
# APP_CODE_PATH_HOST=../

# 指向APP_CODE_PATH_HOST在容器中的位置
APP_CODE_PATH_CONTAINER=$APP_PATH


```

扩展可参考:[**Laradock**](https://laradock.io/)

## docker compose
```shell
# 打包
docker compose build fresns
docker compose build nginx
docker compose build db
docker compose build redis

# 运行容器
docker compose up -d

# 关闭所有正在运行的容器
docker-compose stop

#删除所有现有容器
docker-compose down
```
详参: [**laradock文档**](https://laradock.io/documentation/)

## 已装扩展

[PHP Modules]

bcmath

Core

ctype

curl

date

dom

exif

fileinfo

filter

ftp

gd

gettext

hash

iconv

json

libxml

mbstring

mysqli

mysqlnd

openssl

pcre

PDO

pdo_mysql

pdo_sqlite

Phar

posix

random

readline

redis

Reflection

session

SimpleXML

sockets

sodium

SPL

sqlite3

standard

tokenizer

xml

xmlreader

xmlwriter

Zend OPcache

zlib

[Zend Modules]

### 需要自行安装扩展请参考官网：[docker-php](https://hub.docker.com/_/php)
 