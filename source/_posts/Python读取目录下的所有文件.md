---
title: Python读取目录下的所有文件
categories: Python
cover: lab/img/cover5.webp
abbrlink: 44413
date: 2020-10-22 21:04:38
updated:
tags:
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
---

# Python读取目录下的所有文件

## 代码：

```
import os
path = "D:/DATA" #文件夹目录
files= os.listdir(path) #得到文件夹下的所有文件名称
s = []
for file in files: #遍历文件夹
    if not os.path.isdir(file): #判断是否是文件夹，不是文件夹才打开
        f = open(path+"/"+file); #打开文件
        iter_f = iter(f); #创建迭代器
        str = ""
        for line in iter_f: #遍历文件，一行行遍历，读取文本
            str = str + line
        s.append(str) #每个文件的文本存到list中
print(s) #打印结果
```

]()

