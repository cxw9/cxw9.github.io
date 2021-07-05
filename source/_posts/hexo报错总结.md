---
title: hexo报错总结
date: '2020-010-03 19:48:11'
tags: hexo
categories: hexo
keywords: hexo报错总结
description: hexo报错总结
cover: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg130.jpeg'
top_img: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg130.jpeg'
abbrlink: 646f4601
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

## 1hexo版本更新报错：INFO Validating config WARN Deprecated config detected: “external_link“ with a Boolean

```
报错：
Deprecated config detected: "external_link" with a Boolean value is deprecated. See https://hexo.io/docs/configuration for more details.
```

将

```
external_link: true
```

改为

```
external_link:
  enable: true # Open external links in new tab
  field: site # Apply to the whole site
  exclude: ''
```

###### 百度推送插件配置:

```
# 百度主动推送
baidu_url_submit:
  count: 100 ## 提交最新的1个链接
  host: www.runrab.com ## 百度站长平台中注册的域名
  token: '' ## 准入秘钥
  path: baidu_urls.txt ## 文本文档的地址， 新链接会保存在此文本文档里
```

###### deoloy配置

```
deploy:
- type: git
  repo:
    coding: git@git.coding.net:你的coding/你的coding.coding.me.git #coding地址
    github: git@github.com:你的Github用户名/你的Github用户名.github.io.git  # Github pages地址
  branch: master
- type: baidu_url_submitter #百度主动推送
```



```
baidu_url_submit:
  count: 100 ## 提交最新的一个链接
  host: www.runrab.com ## 在百度站长平台中注册的域名
  token: xxxxx ## 请注意这是您的秘钥， 所以请不要把博客源代码发布在公众仓库里!
  path: baidu_urls.txt ## 文本文档的地址， 新链接会保存在此文本文档里
  xz_appid: 'xxxxxx' ## 你的熊掌号 appid
  xz_token: 'xxxxxx' ## 你的熊掌号 token
  xz_count: 10 ## 从所有的提交的数据当中选取最新的10条,该数量跟你的熊掌号而定
的话 加上
```

### deploy 配置中加上

```
- type: baidu_xz_url_submitter #百度熊掌号
```

