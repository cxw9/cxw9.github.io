---
title: onePointApi文档
cover: lab/img/cover6.webp
abbrlink: 16040
date: 2021-02-26 07:26:04
updated:
tags:
categories:
keywords:
description:
top_img:
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
---

## 官网地址：https://vercel.com/

### 1. 注册

注册很简单，一般直接 github 登录就好了，但是有一点问题是我github账户绑定***qq邮箱***的时候是注册侧边的的。
换成gmail就可以了。

### 2. 安装CLI

#### - 安装nodejs

Nodejs 官方地址：https://nodejs.org/en/download/
直接官网下exe安装即可，不多介绍了

#### - 安装nowcli

打开 cmd 或者 PowerShell 输入

```go
npm install -g now
复制代码
```

#### - 登录

安装完后再输入

```go
now login
复制代码
```

按提示输入邮箱（github绑定的邮箱）
然后会有一份邮件发到你邮箱，点击确认就行了。

### 3.安装onepoint

1. 下载源码：https://github.com/ukuq/onepoint/archive/master.zip   
2. github仓库 https://github.com/ukuq/onepoint 
3.  修改配置文件 
4.  原作者对配置文件的说明：https://www.onesrc.cn/p/details-of-onepoint-configjson-configuration.html  （说明已经过期但仍可用）

#### 4.报错

```
发布npm包
注册并在本机添加npm用户（已注册可忽略）
完成了上面的步骤之后，我们接下来要在www.npmjs.com注册一个账号，这个账号会被添加到npm本地的配置中，下面命令行将会使用到。
//前提已完成npm用户的注册
$ npm adduser
Username: your name
Password: your password
Email: yourmail@gmail.com
如果出现以下错误，可能是你的npm版本太低，通过sudo npm install -g npm升级一下。
npm WARN adduser Incorrect username or password
npm WARN adduser You can reset your account by visiting:
npm WARN adduser
npm WARN adduser     http://admin.npmjs.org/reset
npm WARN adduser
npm ERR! Error: forbidden may not mix password_sha and pbkdf2
npm ERR! You may need to upgrade your version of npm:
npm ERR!   npm install npm -g
npm ERR! Note that this may need to be run as root/admin (sudo, etc.)
成功之后，npm会把认证信息存储在~/.npmrc中，并且可以通过以下命令查看npm当前使用的用户：
$ npm whoami
以上完成之后，我们终于可以发布自己包了。
```

1.npm adduser报错解决

2.报错：Registry returned 409 for PUT on http://registry.npm.taobao.org/ -/user/org.couchdb.user

```
npm登录的时候，报错409.
原因：镜像源切到了淘宝源，需要将淘宝源切回到npm.
解决方法：nrm use npm.  (需要安装nrm) (实测不可用(当你使用淘宝镜像时))
或者： 
npm login --registry http://registry.npmjs.org (实测可用(当你使用淘宝镜像时))
npm publish --registry http://registry.npmjs.org
```

3.