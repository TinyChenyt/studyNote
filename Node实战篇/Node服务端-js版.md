# 从零开始搭建一个简易的本地Node服务端

## 前言
本次Node环境搭建主要是搭建一个Node+Express+Mongodb的服务端，下面所用到代码演示中，node版本为@15.14.0。
请确认自身电脑的是否安装了node环境和mongodb数据库以及注意node的版本

## 初始化
首先新建一个文件夹node-notes，在VScode中打开终端，运行

```shell
npm init -y
```
进行初始化，可以根据需要换成yarn，本文主要使用npm。

初始化完成之后，我们会获得一个package.json文件，如下图所示

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08fdd307e0884a618c900ae4241c7429~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=460&h=252&s=13488&e=png&b=282c34)

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/52fd9f0c8981454191b0ce8e55448974~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=934&h=435&s=29646&e=png&b=262a31)

下面我们先来安装本次服务端需要用到的一些依赖
- nodemon:自动重启服务
- express：服务端框架
- bcryptjs:密码加密
- cors：解决跨域问题
- jsonwebtoken:生成token
- express-jwt:拦截请求验证token
- mongoose:数据库

安装依赖：`npm install bcryptjs cors express express-jwt@5.3.3 jsonwebtoken mongoose nodemon `
安装完成之后，就可以在package.json文件看到对应的依赖

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/590ecf19fb894b5b9ff9bdb838134c20~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=554&h=494&s=29670&e=png&b=282c34)

接下来，我们就需要对package.json文件进行一些修改，因为我们安装了nodemon，因此我们需要在package.json中进行使用。

```json
  "scripts": {
    "dev": "nodemon index.js"
  },
```
修改script，确保我们在运行项目之后启动nodemon的自动重启服务。
到这一步，我们可以看到package.json文件中，main和dev的运行中都有一个index.js文件，但是在我们的项目主目录下并不存在index.js文件，因此我们新建一个index.js文件，并且我们需要建立一些项目所需的文件夹，确保项目的目录结构如下图所示



![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5dac3352b1b44b3397475aea3fcfc607~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=326&h=259&s=8175&e=png&b=22262c)



- config：数据库配置
- controllers: 控制器
- models：数据库模型
- routes: 路由
- utils：中间件/公共方法
- index.js: 项目入库

到这里，项目的基本依赖和目录已经完成。

## 数据库配置
本文用的数据库为mongodb，因此在配置的时候与常用的mysql可能有一些不同。

在config文件夹下新建一个mongodb.js文件，文件的主要内容如下：


```js
// 连接数据库
const mongoose = require('mongoose')

exports.mongoose = mongoose
exports.connectDB = async() => {
    await mongoose.connect('mongodb://你的数据库的地址').then(() => {
        console.log('数据库连接成功')
    }).catch((err) => {
        console.log('数据库连接失败');
    })

    return mongoose
}
```
数据库配置完成之后，我们需要在index.js中导入进行使用。

## index.js

```js
// 导入express
const express = require('express');
const app = express();
// 导入数据库配置
const mongodb = require('./config/mongodb');
// 导入解决跨域的库
const cors = require('cors');

// json解析
app.use(express.json());
// 解决跨域
app.use(cors());

// 连接数据库
mongodb.connectDB()

// 设置服务端的监听端口

app.listen(9999, () => {
    console.log('服务端启动成功')
})
```
基本导入完成之后，我们可以在终端运行`npm run dev`,服务端启动成功

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5b74d6a0b7c489f90961586796ed8de~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=430&h=290&s=15718&e=png&b=282c34)

## 接口开发
在服务端启动成功之后，基本的配置已经完成，这说明我们可以开始功能的开发。接口开发的流程主要分为四步
1. 建立模型
2. 初始化控制器
3. 初始化路由
4. 将路由导出，然后在主入口挂载

下面我们先简单开发一个获取标签列表的接口

### 标签模型的建立
**模型名称需要以双驼峰的方式命名**
我们在models文件夹下新建一个Tags.js的文件，在Tags.js中建立Tags的模型
```js
const { mongoose } = require('../config/mongodb.js');

const TagsSchema = new mongoose.Schema({
    /**
 * type: 类型
 * required： 是否为必填
 * default： 默认值
 * unique: 建立单字段唯一索引
 */
    name: {
        type: String,
        required: true
    },
    logo_url: {
        type: String,
    }
})

const Tags = mongoose.model('Tags', TagsSchema)
module.exports = { Tags }
```
tags具有name和logo_url两个字段。
### 初始化控制器
在controllers文件夹下新建一个tagsController.js文件

```js
const { Tags } = require('../models/Tags')
async function addTags(req, res) {

}
async function getTags(req, res) {
    const tags = await Tags.find();
    // 返回给前端的内容，可以自定义
    res.send({
        code: 200,
        msg: '获取成功',
        data: tags
    })

}
async function updateTags(req, res) {

}
async function deleteTags(req, res) {

}

module.exports = { addTags, getTags, updateTags, deleteTags }
```
### 初始化路由

```js
const express = require('express');
const router = express.Router();

const tagsController = require('../controllers/tagsController');

router.get('/list', tagsController.getTags);

module.exports = router;
```
### 主入口挂载路由

```js
// 导入express
const express = require('express');
const app = express();
// 导入数据库配置
const mongodb = require('./config/mongodb');
// 导入解决跨域的库
const cors = require('cors');

const tagsRoutes = require('./routes/tags');

// json解析
app.use(express.json());
// 解决跨域
app.use(cors());

// 连接数据库
mongodb.connectDB()

// 路由
app.use('/tags', tagsRoutes);

// 设置服务端的监听端口
app.listen(9999, () => {
    console.log('服务端启动成功')
})
```
### 请求接口
使用postman或者直接浏览器访问接口，即可获得tags的列表数据

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cb15ee13e0a3473b9f82101ee0b276cb~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=662&h=232&s=24635&e=png&b=ffffff)

基础的接口流程到这来就完成了。

下面我们了解一些完整的项目开发中需要用到的功能。
## token验证
token令牌是一个完整的项目开发中必不可少的功能，token既可以帮助服务端过滤不合理的接口请求，也可以帮助前端进行路由导航守卫，拦截不合理的页面访问。

在本文的服务端搭建中，我们的服务端token生成和验证主要使用jsonwebtoken，express-jwt和crypto，前面两个依赖我们在最开始的安装依赖中已经说过，后面一个主要是用于生成密钥，用于配合jsonwebtoken使用。

我们首先安装一下crypto `npm install crypto`

然后在utils文件夹下面新建jwt.js和salt.js文件，jwt主要用于生成token以及拦截请求进行token校验，salt主要用于生成密钥。


```js
// 密钥文件 salt.js
const crypto = require('crypto');
module.exports = {
    MD5_SUFFIX: "tiny",
    md5: pwd => {
        let md5 = crypto.createHash("md5");
        return md5.update(pwd).digest("hex");
    },
    secretKey: "token"
}
```

```js
// token验证 jwt.js
const jwt = require("jsonwebtoken");
// const expressJwt = require("express-jwt");
const expressJwt = require("express-jwt");
const { secretKey } = require("./salt")

// 创建token
const createToken = payload =>
    jwt.sign(payload, secretKey, {
        expiresIn: 60 * 60 * 240
    });
// 拦截请求验证token path为不需要拦截的路径
const ExpressJwt = expressJwt({
    secret: secretKey,
    algorithms: ["HS256"],
    credentialsRequired: true
}).unless({
    path: [/^\/user\//]
});

module.exports = {
    createToken,
    ExpressJwt
}
```
在jwt文件中设置path，来设置需要拦截的接口，本文中path为`path: [/^\/user\//]`，意思为除了/user的请求接口外，其余的接口都需要进行token校验。jwt最终导出两个方法，分别为createToken和ExpressJwt。
createToken会在登录请求之后生成，而ExpressJwt会在主入口文件进行挂载以实现接口请求的拦截。

```js
// 导入express
const express = require('express');
const app = express();
// 导入数据库配置
const mongodb = require('./config/mongodb');
// 导入解决跨域的库
const cors = require('cors');

const tagsRoutes = require('./routes/tags');
// token文件
let { ExpressJwt } = require('./utils/jwt')

// json解析
app.use(express.json());
// 解决跨域
app.use(cors());

// 连接数据库
mongodb.connectDB()

app.use(ExpressJwt);

// 路由
app.use('/tags', tagsRoutes);

// 设置服务端的监听端口
app.listen(9999, () => {
    console.log('服务端启动成功')
})
```
这时候，我们再去在浏览器上直接访问获取tags列表的接口，因为tags列表的接口不是user开头的，所以就会报错提示我们没有令牌，没有找到token

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b2d03d08135746f586e343ddcf13023f~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=850&h=293&s=30953&e=png&b=ffffff)

因此我们需要在最开始的某一个接口中（一般都是登录的接口），调用createToken方法生成token，并且将这个token返回给前端，前端进行保存，并且在之后的非/user开头的接口中都需要设置请求头携带token进行请求才能成功访问到数据。
## 账号密码加密
在一个项目中，信息安全是非常重要的，token验证，密码加密本质上都是为了信息安全。为了个人信息的安全，很多时候我们会对一些重要的信息进行加密或掩盖，对于账号密码，我们也不可能直接明文保存在数据库当中，在这个项目中，我们使用bcrypt来对账号密码进行加密。

在建立用户模型时，我们可以对密码这一字段使用bcrypt，确保存入数据库的密码字段是进行加密的

```js
const { mongoose } = require('../config/mongodb.js');
const bcrypt = require('bcryptjs');

// 建立用户表
const UserSchema = new mongoose.Schema({
    username: {
        type: String,
        unique: true
    },
    password: {
        type: String,
        set(val){
            return bcrypt.hashSync(val, 10)
        },
    },
    sex: {
        type: String,
        default: ''
    },
    imgUrl: {
        type: String,
        default: ''
    },
    imgKey: {
        type: String,
        default: ''
    }
})

// 建立用户数据库模型
const User = mongoose.model('User', UserSchema)
module.exports = { User }
```

那既然对密码进行了加密，数据库中的也是密文，所以当我们进行登录的时候，我们进行密码的比对也不能单纯的使用===来进行比较，而需要使用bcrypt

```js
// 第一个参数为传入的密码，第二个参数为数据库中的密码 结果为true则代表两个值相等
bcrypt.compareSync(req.body.password, user.password)
```
## 分页查询
对于列表，我们一般都会进行一个分页获取而不是一下子返回全部数据，在前面的tags列表请求中，我们就是一下子返回了全部数据给前端，因此我们需要对这个getTags方法进行分页优化：

```js
async function getTags(req, res) {
    const page = parseInt(req.query.page, 10);
    const pageSize = parseInt(req.query.pageSize, 10);
    const tags = await Tags.find().skip((page - 1) * pageSize).limit(pageSize);
    res.send({
        code: 200,
        msg: '获取成功',
        data: tags
    })
}
```
前端只需要在发生get请求时携带{ page: page, pageSize:pageSize } 即可。

## 请求方法与参数补充
### get请求
get请求一般用于信息的获取，主要是列表，详情，搜索等接口进行使用，前端传递的参数主要是使用req.query来获取

示例：

```js
// 分页获取文章列表
router.get('/list', async (req, res, next) => {
    const page = parseInt(req.query.page, 10);
    const pageSize = parseInt(req.query.pageSize, 10);
    const article = await Article.find().skip((page - 1) * pageSize).limit(pageSize)
    res.send({
        code: 200,
        msg: '获取成功',
        data: article
    })
})
// 获取文章详情
router.get('/detail', async (req, res, next) => {
    const article = await Article.findOne({
        _id: req.query.article_id
    })
    res.send({
        code: 200,
        msg: '获取成功',
        data: article
    })
})
// 文章查询
router.get('/search', async (req, res, next) => {
    const page = parseInt(req.query.page, 10);
    const pageSize = parseInt(req.query.pageSize, 10);
    const keyword = req.query.keyword;
    // { $or[{ '查询的字段名': { $regex: 前端传递的参数, $option: 'i' } }] } $regex：正则匹配 $option: 'i'：不区分大小写
    const query = { $or: [{ title: { $regex: keyword, $options: 'i' } }, { abstract: { $regex: keyword, $options: 'i' } }, { keyword: { $regex: keyword } }] };
    const articles = await Article.find(query).skip((page - 1) * pageSize).limit(pageSize)
    res.send({
        code: 200,
        msg: '获取成功',
        data: articles
    })
})
```
### post请求
post请求一般是需要传递表单给服务端，主要用于各类新增，前端传递的参数主要用req.body来获取

示例：

```js
// 添加文章
router.post('/add', async (req, res, next) => {
    if(req.body.title === '') {
        req.body.title = '无标题'
    }
    const article = new Article({
        title: req.body.title,
        content: req.body.content,
        html: req.body.html,
        keyword: req.body.keyword,
        author_id: req.body.author_id,
        author_name: req.body.author_name,
        abstract: req.body.abstract,
        title_img_url: req.body.title_img_url || '',
    })
    const result = await article.save()
    res.send({
        code: 200,
        msg: '添加成功',
        data: result
    })
})
```
### put请求
put请求与post相似，主要用于各类修改

示例：

```js
// 修改文章
router.put('/update', async (req, res, next) => {
    const updateArticle = await Article.findOne({
        _id: req.body._id
    })
    if (updateArticle.author_id !== req.body.author_id) {
        res.send({
            code: 400,
            msg: '修改失败,没有修改该文章的权限',
            data: updateArticle
        })
    } else {
        const result = await Article.updateOne({
            _id: req.body._id
        }, {
            title: req.body.title,
            content: req.body.content,
            html: req.body.html,
            keyword: req.body.keyword,
            author_id: req.body.author_id,
            author_name: req.body.author_name,
            abstract: req.body.abstract,
            title_img_url: req.body.title_img_url || ''
        })
        res.send({
            code: 200,
            msg: '修改成功',
            data: result
        })
    }
})
```
### delete请求
delete请求主要用于各类删除，前端传递的参数使用req.body接收

示例：

```js
// 删除文章
router.delete('/delete', async (req, res, next) => {
    const deleteArticle = await Article.findOne({
        _id: req.body.article_id
    })
    if (deleteArticle.author_id !== req.body.author_id) {
        res.send({
            code: 400,
            msg: '删除失败,没有删除该文章的权限',
            data: deleteArticle
        })
    } else {
        const result = await Article.deleteOne({
            _id: req.body.article_id
        })
        res.send({
            code: 200,
            msg: '删除成功',
            data: result
        })
    }
})
```

到这里，一个简单的本地node服务端就搭建完成了。

## 参考文章
https://juejin.cn/post/7240342069997715511?searchId=202311021538392E683012F7468309DBF0
https://juejin.cn/post/6931253375195414535