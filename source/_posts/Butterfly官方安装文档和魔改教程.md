---
title: Butterfly官方安装文档和魔改教程
tags:
  - hexo
categories: 教程
cover: lab/img/cover2.webp
abbrlink: 29818
date: 2020-04-18 17:45:24
updated:
keywords:
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
swiper_index: 2
swiper_desc: 
swiper_cover: 
---
# 魔改教程

### 基于Butterfly主题的分类磁贴（未用）

https://akilar.top/posts/a9131002/

### 给博客添加B站同款动态banner（放弃版本兼容性不好）

https://akilar.top/posts/780a2cea/

### 基于swiper的首页置顶轮播图 hexo-butterfly-swiper

https://akilar.top/posts/8e1264d1/

## 乐特无源码修改 （使用）

https://butterfly.lete114.top/article/Butterfly-config.html

### Hexo引入阿里矢量图标库（未做）

https://akilar.top/posts/d2ebecef/

# hexo 插件



























#### 官方文档链接：

https://butterfly.js.org/posts/21cfbf15/#%E5%AE%89%E8%A3%9D

#### 魔改教程链接：

https://www.antmoe.com/posts/a811d614/index.html

#### live2d看板娘：

https://blog.csdn.net/qq_36239569/article/details/104104894

#### 注意问题

1.安装douban(豆瓣)插件的话，hexo d 不能用来发布，应该用hexo deploy(deploy 和douban重复了)
2.常见hexo s报错很可能是yml语法不和规矩。可以通过YAML，YML在线编辑（校验）器 http://www.bejson.com/validators/yaml_editor/ 检查一下
3。导航栏图标显示不全 对于Font Awesome 可以搜索inject: 在bottom: 下添加
    Font Awesome图标库引入js

    - <link rel="stylesheet" href="https://cdn.staticfile.org/font-awesome/4.7.0/css/font-awesome.css">
原因：fa前缀在5.x版本中已弃用。新的默认设置是实心的fas样式和品牌的fab样式。
官网：https://fontawesome.dashgame.com/

​    