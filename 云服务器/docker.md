# Docker

## Docker安装

> 安装命令：yum -y install docker

![image-20240426113037584](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261130669.png)

## 启动Docker后台服务

> 启动命令：service docker start

![image-20240426113327864](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261133882.png)

## 检查是否安装成功

> 检查docker版本命令：docker version

![image-20240426113900382](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261139407.png)

## 镜像下载

> 下载命令：docker pull 镜像名称
>
> 默认下载最新版：docker pull mysql
>
> 下载指定版本：docker pull mysql:5.7

![image-20240426115914670](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261159693.png)

## 删除镜像

> 删除指定镜像：docker rmi -f 镜像ID
>
> 删除多个镜像：docker rmi -f 镜像ID 镜像ID
>
> 删除全部镜像：docker rmi -f $(docker images -aq)

![image-20240426120639182](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261206207.png)

## 运行并退出容器

![image-20240426121142117](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261211139.png)

## 删除容器

> 删除容器，不能删除运行状态的容器：docker rm 容器ID
>
> 删除容器，无视运行状态：docker rm -f 容器ID
>
> docker rm -f $(docker ps -aq)

![image-20240426142008702](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404261420727.png)

## yum install docker命令的话，下载下来的docker版本为旧版本

解决方法：https://blog.csdn.net/Single_for_life/article/details/133653113