---
title: python裁剪图片
abbrlink: dbc0c148
date: 2021-07-04 22:15:22
updated:
tags:
categories:
keywords:
description:
top_img: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg120.jpeg
comments:
cover: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg120.jpeg
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

# Python裁剪图片

## 个人适用版本

**800x400 裁剪后符合大小**

**1920x400 裁剪后符合比例**

**配合imgbot 自动压缩无需处理压缩**

**cdn by jsdeliver** 

#### **待实现链接自动注入到文章**

链接url 分别放在 max.txt mid.txt min.txt

文件夹 max（原图） mid（比例为1920x400）  min（大小为800x400）

代码：

```python
from PIL import Image
import os

# Mpath = os.getcwd()
# print(Mpath)

# 原来文件夹
source_dirs = './max'
# 目标文件夹
target_dirs = './mid'
# 目标文件夹2
target_dirs2 = './min'


# 得到图片的链接
def getListFiles(path):
    assert os.path.isdir(path), '%s not exist.' % path
    ret = []
    # 已经有的文件夹
    has_dirs = []
    # 目录创建
    # 暂时有一个文件夹下多文件 读取问题没 解决 dirs files均为列表  已经解决
    for root, dirs, files in os.walk(path):
        # print('%s, %s, %s' % (root, dirs, files))
        # print('%s, %s' % (dirs,files))
        s = ''.join(root) + '/' + ''.join(dirs)
        if s not in has_dirs:
            has_dirs.append(s)
        if path == source_dirs:
            create_dirs(has_dirs)
        for filesPath in files:
            ret.append(os.path.join(root, filesPath))
    # print(ret)
    return ret


# 创建不存在文件夹
def create_dirs(has_dirs):
    for i in has_dirs:
        i = i.replace(source_dirs, target_dirs)
        if not os.path.exists(i):
            os.makedirs(i)
    for i in has_dirs:
        i = i.replace(source_dirs, target_dirs2)
        if not os.path.exists(i):
            os.makedirs(i)


# 缩放
def scale(i):
    img = Image.open('' + i)
    # 目标地址
    bb = i.replace(source_dirs, target_dirs2)
    bb = bb.replace('\\', '/')
    width, height = img.size
    w_s = int(width / (width / 800))  # 长宽缩小两倍
    h_s = int(height / (height / 400))  # 长宽缩小两倍
    img = img.resize((w_s, h_s), Image.ANTIALIAS)
    blank = (w_s - h_s) / 2
    # region = img.crop((0, -blank, w_s, w_s - blank))
    region = img.crop((0, 0, w_s, h_s))
    region.save(bb)


# 裁剪
def resize(i):
    img = Image.open('' + i)
    # 目标地址
    bb = i.replace(source_dirs, target_dirs)
    bb = bb.replace('\\', '/')
    width, height = img.size
    he = (width * 400) / 1920
    wi = (height - he) / 2
    # print(he)
    # print(width,height)
    # 前两个坐标点是左上角坐标
    # 后两个坐标点是右下角坐标
    # width在前， height在后
    box = (0, wi, width, he + wi)
    region = img.crop(box)
    # cc=bb.replace('\\','')
    # if os.path.exists(cc):
    # os.makedirs(cc)
    # 因为保存裁剪后的文件要求文件夹要存在故单独处理
    region.save(bb)


# 拼接为链接
def join_url(utl_txt, lst):
    file = utl_txt
    for i in lst:
        i = i.replace('./', '/')
        i = i.replace('\\', '/')
        i1 = i.replace('max', 'mid')
        i2 = i.replace('max', 'min')
        with open(file, 'a+') as f:
            with open(file, 'r') as f1:
                url = 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img' + i + '\n'
                if url not in f1.readlines():
                    f.write(url)
        with open(r"mid.txt", 'a+') as f:
            with open(r"mid.txt", 'r') as f1:
                url = 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img' + i2 + '\n'
                if url not in f1.readlines():
                    f.write(url)
        with open(r"min.txt", 'a+') as f:
            with open(r"min.txt", 'r') as f1:
                url = 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img' + i2 + '\n'
                if url not in f1.readlines():
                    f.write(url)


# 处理
def declImg():
    a = getListFiles(source_dirs)
    b = getListFiles(target_dirs)
    c = getListFiles(target_dirs2)
    for i in a:
        if i not in b:
            b.append(i)
            resize(i)
        if i not in c:
            c.append(i)
            scale(i)
    join_url(r"max.txt", a)


declImg()

'''
#导出requirements.txt
'''

```

