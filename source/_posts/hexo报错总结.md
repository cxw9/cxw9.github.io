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

