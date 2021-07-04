---
title: pixiv代理
abbrlink: df1b4fb9
date: 2021-04-21 19:17:25
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
swiper_index: 6
swiper_desc: 
swiper_cover: 
---

# pixiv代理

## cloudfare 代理

地址：https://**i.pximg.net**替换为 https://pixiv.runrab.workers.dev

例如 https://**i.pximg.net**/img-original/img/2020/06/05/00/00/07/82092623_p0.jpg

换成

![demo](https://pixiv.runrab.workers.dev/img-original/img/2020/06/05/00/00/07/82092623_p0.jpg)





也可以用 https://i.pixiv.cat/img-original/img/2020/06/05/00/00/07/82092623_p0.jpg

来自：https://pixiv.cat/reverseproxy.html

nginx 代理：

```
proxy_cache_path /path/to/cache levels=1:2 keys_zone=pximg:10m max_size=10g inactive=7d use_temp_path=off;

server {
    listen 443 ssl http2;

    ssl_certificate /path/to/ssl_certificate.crt;
    ssl_certificate_key /path/to/ssl_certificate.key;

    server_name i.pixiv.cat;
    access_log off;

    location / {
    proxy_cache pximg;
    proxy_pass https://i.pximg.net;
    proxy_cache_revalidate on;
    proxy_cache_use_stale error timeout updating http_500 http_502 http_503 http_504;
    proxy_cache_lock on;
    add_header X-Cache-Status $upstream_cache_status;
    proxy_set_header Host i.pximg.net;
    proxy_set_header Referer "https://www.pixiv.net/";

    proxy_cache_valid 200 7d;
    proxy_cache_valid 404 5m;
 }
}
```

cf代理设置

```
addEventListener("fetch", event => {
  let url = new URL(event.request.url);
  url.hostname = "i.pximg.net";

  let request = new Request(url, event.request);
  event.respondWith(
    fetch(request, {
      headers: {
        'Referer': 'https://www.pixiv.net/',
        'User-Agent': 'Cloudflare Workers'
      }
    })
  );
});
```

