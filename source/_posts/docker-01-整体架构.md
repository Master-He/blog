---
title: docker-01-整体架构
date: 2018-05-07 08:09:19
tags: docker
category: 后端
---





[TOC]



# docker 架构

docker使用 `Go语言` 开发

基于 Linux 内核的 `cgroup`，`namespace`，以及 AUFS 类的 `Union FS` 等技术

对`进程`进行封装隔离，属于 操作系统层面的虚拟化技术

由于`隔离的进程`独立于宿主和其它的隔离的进程，因此docker也称其为容器



docker 架构图



![image-20191207081450908](/Users/hwj/Library/Application Support/typora-user-images/image-20191207081450908.png)

`runc` 是一个 Linux 命令行工具，用于创建和运行容器。

`containerd` 是一个守护程序，它管理容器生命周期，提供了在一个节点上执行容器和管理镜像的最小功能集。



#docker  Vs  传统虚拟化技术



`传统虚拟机技术`是虚拟出一套`硬件`后，在其上运行一个`完整操作系统`，在该系统上再运行所需应用进程

![image-20191207082712381](/Users/hwj/Library/Application Support/typora-user-images/image-20191207082712381.png)





容器内的应用进程`直接运行于宿主的内核`.

容器内没有自己的内核，而且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便。

容器就是把代码和代码运行的环境打包一起，只需要一次创建或配置，可以在任意地方正常运行

![image-20191207082721822](/Users/hwj/Library/Application Support/typora-user-images/image-20191207082721822.png)

