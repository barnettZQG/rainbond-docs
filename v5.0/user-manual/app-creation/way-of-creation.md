---
title: 创建方式
summary: 。
toc: true
---

这篇文章将会为你介绍 Rainbond 的应用的创建方式.

在前一篇文章 [应用的定义](./app-definition.html) 中已经提到, 应用是由各个不同的服务组件构成, 那么应用的创建就离不开服务组件的创建. 服务组件创建的方式有3种, 分别是: 源码创建, 从 Docker 镜像创建, 从 [应用市场](../app-store/app-market.html) 安装.

<img src="https://static.goodrain.com/images/docs/3.7/user-manual/create-app-3.7.png" width="100%" />

## 1. 从源码创建

Rainbond 支持多种流行的编程语言的源码创建, 同时也支持通过Dockerfile进行创建. Rainbond 目前支持的语言有:

- Java
- PHP
- Python
- Node.js
- Ruby
- Golang
- Html
- Dockerfile

通过源码的方式创建服务组件, 需要把源码托管在版本控制系统上, Rainbond 目前支持的版本控制系统有 `Git 和 SVN`, 也是目前大家常用的版本控制系统.

对于一些聚合工程, 我们想要构建应用所需的源码, 可能位于仓库下的某一个子目录下. 获取对应子目录下的源码的方式如下：

- Git: 源码仓库地址为: https://github.com/demo/demo.git,  所需源码位于子目录 /subdir1/subdir2 下，则构建应用使用的仓库地址为: https://github.com/demo/demo.git?dir=subdir1/subdir2.
> 我们不推荐使用子目录的方式对项目进行区分, 应该尽可能地给每个项目建立独立的 Git 仓库. 这样可以使代码的结构更加地清晰, 不至于太臃肿, 方便管理.

- SVN: 源码仓库地址为: http://svn.demo.net/trunk/subdir,  则构建应用使用仓库地址为: http://svn.demo.net 分支选择为子目录路径: trunk/subdir
> 对于 SVN 这种用子目录来对项目进行区分的方式, 我们是先把整个仓库的代码都拉下来, 然后再找到相对应目录的代码, 所以, 拉代码的这个过程相对地会长一些.

## 2. 从 Docker 镜像创建

从 Docker 镜像创建又分为: 指定镜像, Docker Run 命令和 Docker Compose.

### 2.1 指定镜像

Rainbond可以通过直接拉取 Docker 官方或者第三方 Docker 镜像的方式创建应用, 但需要注意的是, 第三方 Docker 仓库一定要支持 HTTPS 协议, 否则需要就修改管理节点的 Docker 配置, 使其支持非 HTTPS 的 Docker 仓库.

### 2.2 Docker Run 命令

Docker Run 命令时, Rainbond 会解析出 Docker Run 命令中的镜像, 端口, 环境变量和存储信息, 然后生成`应用（服务）抽象`, 最后再被调度到 Kubernetes 上运行起来.

> Rainbond 支关心镜像, 端口, 环境变量和存储这四个信息, 其它信息将会被忽略.

### 2.1 Docker Compose

如果你习惯用 Docker Compose来进行容器的编排, 那么可以选择 DockerCompose, 并提供 docker-compose.yml. 跟 Docker Run 命令一样, Rainbond 会解析出 docker-compose.yml 中的`镜像, 端口, 环境变量和存储`这四个信息, 然后生成`应用（服务）抽象`, 最后再被调度到 Kubernetes 上运行起来.

## 3. 从应用市场安装

除了从源码创建和从 Docker 镜像这两种创建应用的方法外，rainbond还提供了应用市场的应用一键部署，应用市场是好雨提供的一项公有云服务，提供了常用的开发应用及工具.

关于应用市场的更多信息, 请前往: [应用市场](../app-store/app-market-define.html)