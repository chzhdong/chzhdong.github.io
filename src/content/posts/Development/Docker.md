---
title: Docker
published: 2025-01-08
description: 'Docker'
image: ''
tags: ["Docker"]
category: 'Tool'
draft: false 
lang: 'zh_CN'
---

## 概述

Docker 是一个开源的应用容器引擎，基于 [Go 语言](https://www.runoob.com/go/go-tutorial.html) 并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

## 安装

### 配置环境

```bash
#安装前先卸载操作系统默认安装的docker，
sudo apt-get remove docker docker-engine docker.io containerd runc
#安装必要支持
sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release
# 阿里源（推荐使用阿里的gpg KEY）
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
#阿里apt源
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
#更新源
sudo apt update
sudo apt-get update
```

### Docker 安装

```bash
#安装最新版本的Docker
sudo apt install docker-ce docker-ce-cli containerd.io
#等待安装完成

#查看Docker版本
sudo docker version

#查看Docker运行状态
sudo systemctl status docker
```

### 非root用户运行Docker

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgr#查看所有容器
docker ps -a
# 在~/.bashrc文件中添加以下代码
groupadd -f docker
```

## Docker指令

```bash
# 拉取镜像
docker pull nacos/nacos-server:1.2.0
# 创建容器
docker run --env MODE=standalone --env JVM_XMS=256m --env JVM_XMX=256m --name nacos --restart=always -d -p 8848:8848 nacos/nacos-server:1.2.0
## 删除容器
docker rm -f nacos
## 运行容器
docker start nacos
## 停止容器
docker stop nacos
```

## 注意事项

### Docker在拉取镜像时，输出“Error Get https://registry-1.docker.io/v2/:环境报错问题”

该问题是由于无法访问docker.com的相关信息，进行下载所导致，需配置docker使用国内镜像源即可。

```bash
# 创建文件
vim /etc/docker/daemon.json
# 写入相关的配置信息
{
　　"registry-mirrors":
　　　　[
　　　　　　"https://docker.m.daocloud.io/",
　　　　　　"https://huecker.io/",
　　　　　　"https://dockerhub.timeweb.cloud",
　　　　　　"https://noohub.ru/",
　　　　　　"https://dockerproxy.com",
　　　　　　"https://docker.mirrors.ustc.edu.cn",
　　　　　　"https://docker.nju.edu.cn",
　　　　　　"https://xx4bwyg2.mirror.aliyuncs.com",
　　　　　　"http://f1361db2.m.daocloud.io",
　　　　　　"https://registry.docker-cn.com",
　　　　　　"http://hub-mirror.c.163.com",
　　　　　　"https://docker.mirrors.ustc.edu.cn"
　　　　]
}
# 重启docker服务以使其生效
sudo systemctl restart docker
```

### 无法访问阿里云服务器相关端口

该问题主要是用于阿里云的端口访问管理权限需要在阿里云的控制台进行统一的配置，而不是可以直接通过公网IP进行访问。

配置位置：控制台 - 云服务器 - 安全组 - 管理规则 - 入方向