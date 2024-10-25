# node配置swagger

## 前言
环境版本与项目目录参考笔记《node服务端-js版》
- 安装swagger-jsdoc、swagger-ui-express
- 在utils目录下新建swagger.js文件，用于swagger配置、生成文档
- 在index.js中引入并配置swagger
- swagger版本一般3.0以上，请注意版本，配置可能会不一样

**详情参考[官网](https://swagger.io/docs/specification/v3_0/about/)**


## swagger配置

```js
const path = require('path');
const express = require('express');
const swaggerUI = require('swagger-ui-express');
const swaggerJsDoc = require('swagger-jsdoc');


const options = {
    definition: {
        openapi: '3.0.0',
        info: {
            title: 'tiny test node-server',
            version: '1.0.0',
            description: 'A simple CRUD API'
        }
    },
    // 读取该路径下的所有路由文件的swagger注释
    apis: [path.join(__dirname, '../routes/*.js')]
};

const swaggerSpec = swaggerJsDoc(options);

const swaggerJson = (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    res.send(swaggerSpec);
};

const swaggerInstall = (app) => {
    if(!app) {
        app = express();
    }
     
    // 由于项目在之前添加了token验证，只允许user/路径下的接口不需要token，因此将swagger文档放在user路径下
    // 也可以在jwt.js文件下开放swagger/路径的接口
 
    app.get('/user/swagger.json', swaggerJson);

    app.use('/user/swagger', swaggerUI.serve, swaggerUI.setup(swaggerSpec));
};

module.exports = swaggerInstall;
```

## 启动文件中导入swagger配置
**参考之前的笔记，即在index.js中引入swagger**
```js
const swaggerInstall = require('./utils/swagger');

// 路由挂载
app.use('xxx', xxxRouter);
...

swaggerInstall(app);
```

## swagger注释
**重点：swagger通过注释来生成文档，所以每个接口都要有注释，否则无法生成文档**

在路由文件中添加注释

下面以登录的接口为例，
```js
/**
 * @swagger
 * /user/login:
 *   post:
 *     tags:
 *       - User
 *     summary: 用户登录
 *     description: 用户登录
 *     operationId: loginUser
 *     consumes: ["application/json"]
 *     requestBody:
 *       description: 用户登录
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             properties:
 *               username:
 *                 type: string
 *               password:
 *                 type: string
 *     responses:
 *       '200':
 *         description: Successful operation
 *       '400':
 *         description: Invalid status value
 */
router.post('/login', userController.login);
```

## 统一头部token
由于除了user/的其他接口都需要token验证，因此需要为swagger配置统一token，以实现其他接口的访问

```js
const path = require('path');
const express = require('express');
const swaggerUI = require('swagger-ui-express');
const swaggerJsDoc = require('swagger-jsdoc');


const options = {
    definition: {
        openapi: '3.0.0',
        info: {
            title: 'tiny test node-server',
            version: '1.0.0',
            description: 'A simple CRUD API'
        },
        components: {
            securitySchemes: {
                Authorization: {
                    type: "http",
                    scheme: "bearer",
                    bearerFormat: "JWT",
                    value: "Bearer <JWT token here>"
                }
            }
        }
    },
    apis: [path.join(__dirname, '../routes/*.js')]
};

const swaggerSpec = swaggerJsDoc(options);

const swaggerJson = (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    res.send(swaggerSpec);
};

const swaggerInstall = (app) => {
    if(!app) {
        app = express();
    }

    app.get('/user/swagger.json', swaggerJson);

    app.use('/user/swagger', swaggerUI.serve, swaggerUI.setup(swaggerSpec));
};

module.exports = swaggerInstall;
```
**注意：只有在3.0及以上的版本中，才是在components下使用securitySchemes定义的写法**

重启服务，访问：http:/路径/user/swagger/

![20241023161637](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20241023161637.png)