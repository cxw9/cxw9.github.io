---
title: CDH安装
tags:
  - CDH
  - 安装脚本
categories: 大数据
keywords: CDH安装脚本
cover: lab/img/cover1.webp
top_img: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg101.jpeg
abbrlink: 8708
date: 2020-03-11 15:20:03
updated:
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
# CDH安装脚本
- [脚本来源](https://gitee.com/hcsystem/cdh_install)


#### 介绍

- CDH安装 集群/单机 安装脚本
- 系统： CentOS-7.7 最小化安装
- 脚本依赖软件包 perl, expect psmisc(需要联网安装或挂载完整光盘镜像配置本地安装源)
- JDK MySQL 为二进制方式安装

#### 单机安装教程

1.配置主机信息 host:主机名 ip:安装集群节点IP 一一对应

    host=node01
    ip=192.168.0.71

2.配置 hosts 解析

    echo "$ip    $host"  >> /etc/hosts

3.更改主机名

    hostnamectl set-hostname $host

4.配置秘钥登录(替换 $root_pass 为节点root密码)

    bash <(curl -sSL https://gitee.com/hcsystem/cdh_install/raw/master/ssh_key_copy.sh) "$ip" root $root_pass

5.安装

    bash <(curl -sSL https://gitee.com/hcsystem/cdh_install/raw/master/install_cdh.sh) server

#### 集群安装教程

- 步骤 1, 2, 3, 4, 在所有节点执行
- 步骤 5 在 server 节点执行
- 步骤 6 在 agent 节点执行 

1.配置主机信息 host:主机名 ip:安装集群节点IP 一一对应

    ip=(192.168.0.71 192.168.0.72 192.168.0.73)
    host=(node01 node02 node03)

2.配置 hosts 解析

    # 获取本机IP
    host_if=$(ip route | grep default | cut -d' ' -f5)
    host_ip=$(ip a | grep "$host_if$" | awk '{print $2}' | cut -d'/' -f1)
    
    # 配置集群 hosts 解析
    let SER_LEN=${#ip[@]}-1
    if [ "$(echo ${ip[@]} | grep $host_ip)" ]; then
        sed -i '3,$d' /etc/hosts
        echo -e "\n# cdh cluster" >> /etc/hosts
        for ((i=0;i<=$SER_LEN;i++)); do
            echo "${ip[i]}  ${host[i]}" >> /etc/hosts
        done
    fi

3.更改主机名

    for ((i=0;i<=$SER_LEN;i++)); do
        if [ "${ip[i]}" == "$host_ip" ]; then
            hostnamectl set-hostname ${host[i]}
        fi
    done

4.配置秘钥登录(替换 $root_pass 为节点root密码)

    SERVERS="${ip[@]}"
    bash <(curl -sSL https://gitee.com/hcsystem/cdh_install/raw/master/ssh_key_copy.sh) "$SERVERS" root $root_pass

5.server 节点安装

    bash <(curl -sSL https://gitee.com/hcsystem/cdh_install/raw/master/install_cdh.sh) server

6.agent 节点安装(192.168.0.71 为 server 节点IP)

    bash <(curl -sSL https://gitee.com/hcsystem/cdh_install/raw/master/install_cdh.sh) agent 192.168.0.71

#### 配置服务管理

> cloudera-scm-server

```shell
source /etc/profile
cat > /usr/lib/systemd/system/cloudera-scm-server.service  <<EOF
[Unit]
Description=cloudera-scm-server
After=network.target

[Service]
TimeoutSec=10
Type=forking
ExecStart=/opt/cloudera-manager/cm-5.16.1/etc/init.d/cloudera-scm-server start
Environment="JAVA_HOME=$JAVA_HOME" "JRE_HOME=$JRE_HOME"
ExecStop=/opt/cloudera-manager/cm-5.16.1/etc/init.d/cloudera-scm-server stop

[Install]
WantedBy=multi-user.target
EOF

# 跟随系统启动
systemctl daemon-reload
systemctl enable cloudera-scm-server.service
```

> cloudera-scm-agent

```shell
source /etc/profile
cat > /usr/lib/systemd/system/cloudera-scm-agent.service  <<EOF
[Unit]
Description=cloudera-scm-agent
After=network.target

[Service]
TimeoutSec=10
Type=forking
ExecStart=/opt/cloudera-manager/cm-5.16.1/etc/init.d/cloudera-scm-agent start
Environment="JAVA_HOME=$JAVA_HOME" "JRE_HOME=$JRE_HOME"
ExecStop=/opt/cloudera-manager/cm-5.16.1/etc/init.d/cloudera-scm-agent stop

[Install]
WantedBy=multi-user.target
EOF

# 跟随系统启动
systemctl daemon-reload
systemctl enable cloudera-scm-agent.service
```



- [CDH 安装](https://www.cnblogs.com/yy3b2007com/p/9962099.html)
- [Cloudera Management Service 各个角色迁移](https://www.cnblogs.com/gxc2015/p/9273301.html)
