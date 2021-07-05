---
title: json-server入门
tags: nodejs
categories: nodejs
keywords: json-server
description: json-server入门
cover: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg115.jpeg'
top_img: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg115.jpeg'
abbrlink: 3e8060c8
date: 2021-01-18 21:07:30
updated:
comments:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
swiper_index:
swiper_desc:
swiper_cover:
---
## json-server

这是一个npm 的第三方包，可以通过下载安装； json-server 模拟了一个简单的数据库， 可以进行基础的接口数据测试

### 安装json-server

```
npm install -g json-server
```

### 创建 db.json 文件

db.json 文件 作为数据库存储数据使用； 是一个对象； 对象中的每个字段相当于数据库中的每个数据表， 字段对应的值 是数据表中的数据

```
{
 "student": [
   {
     "name": "张三",
     "age": 18,
     "book": "假如给我三天光明",
     "id": 1
   },
   {
     "name": "李四",
     "age": 50,
     "book": "水浒传",
     "id": 2
   },
   {
     "name": "李四",
     "age": 20,
     "book": "水浒传",
     "id": 3
   }
 ],
 "list": [
   {
     "title": "信息",
     "id": 1
   }
 ]
}
```

### 启动 json-server 服务

```
json-server --watch db.json 
```


成功开启后，会生成接口请求地址 开启成功的显示

```
  Read error has been fixed :)
  db.json has changed, reloading...

  Loading db.json
  Done

  Resources
  http://localhost:3000/student
  http://localhost:3000/list

  Home
  http://localhost:3000
```

结果解析
// 这就是生成的请求接口地址
 http://localhost:3000/student
 http://localhost:3000/list
通过 psotman 进行模拟数据的请求操作

```
// get 请求
localhost:3000/student  全部信息
localhost:3000/student/id  单一一个信息

// post请求
localhost:3000/student
// 添加body参数

// put请求 更新全部数据(覆盖)
localhost:3000/student/:id
// 添加body参数

// patch请求 更新局部数据(更新具体的某个字段)
localhost:3000/student/:id
// 添加body参数

// delete请求
localhost:3000/student/:id
```

### 其他高级用法

json-server本身就是依赖express开发而来，可以进行深度定制。细节就不展开，具体详情请参考官网。

#### 自定义路由

```
const jsonServer = require('json-server')
const server = jsonServer.create()
const router = jsonServer.router('db.json')
const middlewares = jsonServer.defaults()

server.use(middlewares)

server.get('/echo', (req, res) => {
  res.jsonp(req.query)
})

server.use(jsonServer.bodyParser)
server.use((req, res, next) => {
  if (req.method === 'POST') {
    req.body.createdAt = Date.now()
  }
  next()
})

server.use(router)
server.listen(3000, () => {
  console.log('JSON Server is running')
})
自定义输出内容
router.render = (req, res) => {
  res.jsonp({
    body: res.locals.data
  })
}
```

 自定义用户校验 

```
const jsonServer = require('json-server')
const server = jsonServer.create()
const router = jsonServer.router('db.json')
const middlewares = jsonServer.defaults()

server.use(middlewares)
server.use((req, res, next) => {
 if (isAuthorized(req)) { // add your authorization logic here
   next() // continue to JSON Server router
 } else {
   res.sendStatus(401)
 }
})
server.use(router)
server.listen(3000, () => {
  console.log('JSON Server is running')
})
```

