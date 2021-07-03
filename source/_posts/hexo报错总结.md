---
title: hexo报错总结
abbrlink: 646f4601
date: 2021-07-03 19:48:11
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
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

