# PHP FPM 镜像 For Laravel and Lumen

## 更新记录

2016.03.09

- php版本升级到5.6.19
- 增加mysql扩展（有些变态的框架还在用这个扩展）

2016.02.26

更改composer的安装方式，去掉packagist的国内镜像（可能用到国外服务器，而且也不稳定）

2016.02.26

php版本更新到5.6.18

2016.01.22

php版本更新到5.6.17

## 基础说明

该镜像主要为满足 `laravel5` 框架而制作，并附加了 `redis`, `mongo`, `msgpack`, `imagick`等扩展。

说明：

- 基础镜像：[php-fpm](https://hub.docker.com/_/php)
- 如果需要phpunit，xdebug，pman等测试及开发工具，请使用`ibbd/php-fpm-dev`镜像，对应的dockerfile在目录`php-fpm-dev`下。
- 如果只是使用php的命令行，可以使用对应的cli镜像（含swoole）：`ibbd/php-cli`和`ibbd-cli-dev`

## PHP扩展 

- gd
- iconv 
- mcrypt
- pdo
- tokenizer 
- mbstring 
- gd 
- redis
- mongo
- msgpack 
- zip
- mysqli
- imagick

附加安装

- composer（全局安装）
- Laravel Installer: 文档https://laravel.com/docs/
- Lumen Installer: 文档https://lumen.laravel.com/docs/

## 安装 

- Dockerfile: `sudo ./build.sh`
- Pull: `sudo docker pull ibbd/php-fpm`

## 使用

```sh
# 代码目录
code_path=/var/www

# 日志目录
logs_path=/var/log/php

current_path=$(pwd)
docker run --name=ibbd-php-fpm -d \
    -p 9000:9000 \
    -v $code_path:/var/www \
    -v $logs_path:/var/log/php \
    -v $current_path/conf/php.ini:/usr/local/etc/php/php.ini:ro \
    -v $current_path/conf/php-fpm.conf:/usr/local/etc/php-fpm.conf:ro \
    ibbd/php-fpm \
    php-fpm -c /usr/local/etc/php/php.ini -y /usr/local/etc/php-fpm.conf
```

说明：完整的应用见 `./run.sh.example`

