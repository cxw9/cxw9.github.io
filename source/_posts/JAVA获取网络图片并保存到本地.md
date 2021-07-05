---
title: JAVA获取网络图片并保存到本地
tags: Java
categories: Java
keywords: JAVA获取网络图片并保存到本地
description: JAVA获取网络图片并保存到本地
cover: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg113.jpeg'
top_img: 'https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg113.jpeg'
abbrlink: cdcb5006
date: 2020-09-22 21:00:47
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

# JAVA获取网络图片并保存到本地

## 初代代码

```
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.URL;
import javax.net.ssl.HttpsURLConnection;

public class FirstTest {

​    public static void main(String[] args) throws Exception {
​        // TODO 自动生成的方法存根

​        long start=System.currentTimeMillis();
​        System.out.println("开始");

​        for(int i=1;i<=100;i++) {
//            double r=(0+Math.random()*10000);
//            System.out.println(r);
​            String url="https://source.unsplash.com/random";//一个随机图片接口
//            +(0+Math.random()*10000);可以在random后面加入一个随机数避免图片重复
​            getImg(url,i);
​            System.out.println("完成"+i);
​        }
​        long end=System.currentTimeMillis();
​        System.out.println("运行时间:"+(end-start)/1000+"秒");


​    }
​    private static void getImg(String u,int i){
​        URL url;
​        try {
​            url = new URL(u);
​            HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
​            conn.setRequestMethod("GET");
​            conn.setConnectTimeout(5*1000);
​            InputStream in = conn.getInputStream();
​            byte[] data = readInputStream(in);
​            File f = new File("C:\\Users\\Administrator\\Desktop\\img\\"+i+".jpg");
​            FileOutputStream out = new FileOutputStream(f);
​            out.write(data);
​            out.close();
​        } catch (IOException e) {
​            // TODO 自动生成的 catch 块
​            e.printStackTrace();
​        }

​    }

​    private static byte[] readInputStream(InputStream ins) throws IOException {
​        // TODO 自动生成的方法存根
​        ByteArrayOutputStream out = new ByteArrayOutputStream();
​        byte[] buffer = new byte[1024];
​        int len = 0;
​        while ((len = ins.read(buffer)) != -1) {
​            out.write(buffer, 0, len);

​        }
​        ins.close();

​        return out.toByteArray();
​    }

}


```

