---
title: Node 集成Swagger 生成接口文档
date: 2018-07-29 16:56:02
tags: Swagger, Node
---

本文记录express 集成Swagger 的步骤 [点击查看Demo](http://lichengbo.cn:3001/api-docs/)

## 相关环境
- express 4.16.0
- swagger-ui-express 3.0.10
- swagger-jsdoc 1.10.3

<!-- more -->

## 配置
> 将下面代码放到app.js 中，且必须放到var app = express(); 下面一行。我一开始放到底部没有生效。


```JavaScript
// swagger
var swaggerUi = require('swagger-ui-express');
var swaggerJSDoc = require('swagger-jsdoc');

var swaggerDefinition = {
  info: {
    title: 'Node Swagger API',
    version: '1.0.0',
    description: 'Swagger 接口文档',
  },
  host: 'localhost:3000',
  basePath: '/',
};

// options for the swagger docs
var options = {
  // import swaggerDefinitions
  swaggerDefinition: swaggerDefinition,
  // path to the API docs
  apis: ['./routes/*.js'],
};

// initialize swagger-jsdoc
var swaggerSpec = swaggerJSDoc(options);

// serve swagger
app.get('/swagger.json', function(req, res) {
  res.setHeader('Content-Type', 'application/json');
  res.send(swaggerSpec);
});

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));
```
## 定义路由接口注释
```Java
/**
 * @swagger
 * definitions:
 *   Puppy:
 *     properties:
 *       name:
 *         type: string
 *       breed:
 *         type: string
 *       age:
 *         type: integer
 *       sex:
 *         type: string
 */
```
更多示例参考 [Swagger Specification](http://swagger.io/specification/)

参考文档

[Swagger and NodeJS](https://mherman.org/blog/2016/05/26/swagger-and-nodejs/)
