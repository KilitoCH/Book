# Docker 操作笔记

## 关于创建、分享镜像

### 创建镜像

#### dockerfile

dockerfile notes
#### docker commit

Using `docker commit` command

### 分享镜像

[如何把本地镜像部署到其他计算机或服务器](https://blog.csdn.net/taochengwu123/article/details/100085890)
**核心**：
```
docker save -o [保存的文件名] [要保存的镜像名]
docker load --input [要导入的镜像文件]
docker load < [要导入的镜像文件]
```

## docker command in linux

### 暴露守护进程到tcp://0.0.0.0:2375的方法
配置文件地址：`/lib/systemd/system/docker.service`
添加以下内容：
`ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock`
然后执行：
```sh
systemctl daemon-reload
systemctl restart docker
```