---
title: cloudfare解决没有ipv4或ipv6
abbrlink: ba3f934f
date: 2021-04-03 19:16:28
updated:
tags:
categories:
keywords:
description:
top_img: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg102.jpeg
comments:
cover: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/min/acg/acg102.jpeg
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

cloudfare简介:

> Cloudflare是一家美国的跨国科技企业，总部位于旧金山，在英国伦敦亦设有办事处。Cloudflare以向客户提供网站安全管理、性能优化及相关的技术支持为主要业务。通过基于反向代理的内容分发网络(CDN, Content Delivery Network)、任播(Anycast)技术 [1] 、基于nginx+lua架构的Web应用防火墙(WAF, Web Application Firewall) [2] 及分布式域名解析服务(Distributed Domain Name Server)等技术，Cloudflare可以帮助受保护站点抵御包括分布式拒绝服务攻击(DDoS, Distributed Denial of Service)在内的大多数网络攻击，确保该网站长期在线，同时提升网站的性能、访问速度以改善访客体验。--百度百科

简单来说就是cdn提供商

用到方法;三种 

一：cname方式

直接canme到域名

二：AAAA到ipv6地址 

三：Argo Tunnel

正在更新 但是实测速度并不怎末样 我是用来nas ipv4访问的
