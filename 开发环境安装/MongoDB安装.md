# MongoDB安装

[官网](https://www.mongodb.com/try/download/community)

![20240906142745](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20240906142745.png)

1、点击进行下载，双击下载后的安装包进行安装

![20240906143020](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20240906143020.png)

2、点击custom修改安装路径，记住安装路径

3、在MongoDB的安装目录下，找到bin目录，将bin目录添加到环境变量中

4、在MongoDB文件中data文件夹下新建DB文件（存放数据库）和log文件（存放日志）
![20240906144346](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20240906144346.png)

5、在bin目录下新建config文件，内容如下：
```
dbpath=db文件夹的绝对路径
logpath=db文件夹的绝对路径/log/mongo.log
```
6、在db文件夹下打开cmd，输入mongod运行数据库

7、访问127.0.0.1:27017
![20240906144545](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20240906144545.png)
