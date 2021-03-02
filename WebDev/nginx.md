# Nginx使用与解析

## nginx代理部署项目
[nginx代理部署Vue与React项目](https://www.cnblogs.com/jackson-yqj/p/10273352.html)

**注意！！！**
在nginx的配置文件中配置内容路径时一定要写`/`而不是`\`。否则无法访问相应路径。

## nginx-docker

[官方文档](https://hub.docker.com/_/nginx?tab=description&page=1&ordering=last_updated)
### 相关配置文件地址

在容器中相关位置分别是：
日志位置：/var/log/nginx/
配置文件位置：/etc/nginx/
项目位置：/usr/share/nginx/html

**推荐配置方式**
从本地挂载到容器，修改本地配置文件之后直接进到容器中`nginx -s reload`就可以。