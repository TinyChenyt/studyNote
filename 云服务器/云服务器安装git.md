# 云服务器安装git
**以阿里云 CentOS7 为例**

## 安装git
```shell
sudo yum update
sudo yum install git
```
![20241023162731](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20241023162731.png)

安装完成，通过`git --version`查看git是否安装成功
![20241023162848](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20241023162848.png)

## 创建git仓库
首先通过命令`cd /`回到根目录下
![20241023163110](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20241023163110.png)

## 配置git服务器
配置服务器，将服务器设置为公开
git config --global http.sslVerify false

git config --global user.name "Your Name"
git config --global user.name "tiny"

git config --global user.email "your@email.com"
git config --global user.email "2454046178@qq.com"