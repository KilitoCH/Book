# Docker 操作笔记

## 关于创建、分享镜像

### 创建镜像

#### dockerfile
#### docker commit

### 分享镜像

[如何把本地镜像部署到其他计算机或服务器](https://blog.csdn.net/taochengwu123/article/details/100085890)
**核心**：
```
docker save -o [保存的文件名] [要保存的镜像名]
docker load --input [要导入的镜像文件]
docker load < [要导入的镜像文件]
```