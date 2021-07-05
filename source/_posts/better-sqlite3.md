---
title: better-sqlite3
tags: nodejs
categories: nodejs
keywords: nodejs better-sqlite3
cover: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg1.jpeg'
top_img: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg1.jpeg'
abbrlink: be3b9b7b
date: 2020-03-03 19:16:14
updated:
description:
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





# better-sqlite3

### 官方介绍

Node.js 中最快、最简单的 SQLite3 库。

- 全面的交易支持

- 高性能、高效率和安全

- 易于使用的同步 API *（比异步 API 更好的并发性......是的，你没看错）*

- 支持用户定义的函数、聚合、虚拟表和扩展

- 64 位整数*（在需要之前不可见）*

- 工作线程支持*（用于大/慢查询）*

  

### 安装 

不要升级npm7.x(虽然不影响 注意npm i 和 npm install 的区别)

```
npm install better-sqlite3
```

注意 全局安装命令 

```
npm install better-sqlite3
```

项目中安装

```
npm install better-sqlite3 --save
```

### 用法

```
const db = require('better-sqlite3')('foobar.db', options);
const row = db.prepare('SELECT * FROM users WHERE id = ?').get(userId);
console.log(row.firstName, row.lastName, row.email);
```

官网给的例子并不好懂

官方github https://github.com/JoshuaWise/better-sqlite3

api文档：https://github.com/JoshuaWise/better-sqlite3/blob/master/docs/api.md



### 来点机器中文翻译

没找到中文文档:看着不是特别方便，就自己留一份吧

### new Database(*path*, [*options*])

创建新的数据库连接。如果数据库文件不存在，则创建该文件。这是同步发生的，这意味着您可以立即开始执行查询。你可以通过传递: memory: 作为第一个参数来创建一个内存数据库。您可以通过传递一个空字符串(或者省略所有参数)来创建临时数据库。

```
内存中的数据库也可以通过传递 .Serialize () ，而不是将字符串作为第一个参数传递。
```

- `options.readonly`: 

  Readonly: 以 readonly 模式打开数据库连接(默认值: false)。

- `options.fileMustExist`:

  如果数据库不存在，将抛出一个 Error，而不是创建一个新文件。对于内存中、临时或只读数据库连接，忽略此选项(默认值为 false)。

- `options.timeout`: 

  Timeout: 在抛出 SQLITE _ busy 错误(默认值: 5000)之前，在锁定的数据库上执行查询时等待的毫秒数。

- `options.verbose`:

  Verbose: 提供一个函数，该函数在数据库连接执行每个 SQL 字符串时调用(默认值: null)。

#### 不用翻译了，太难受还是直接看英文文档合适

