---
title: docker-04-命令
date: 2018-05-07 08:09:19
tags: docker
category: 后端

---



[TOC]



# 镜像命令



#### docker pull

~~~bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
~~~

这里的仓库名是两段式名称，即 `<用户名>/<软件名>`。对于 Docker Hub，如果不给出用户名，则默认为 `library`，也就是官方镜像。

如果没有给出 Docker 镜像仓库地址，因此将会从 Docker Hub 获取镜像。而镜像名称是 `ubuntu:18.04`，因此将会获取官方镜像 `library/ubuntu` 仓库中标签为 `18.04` 的镜像。





#### docker images / docker image ls

`docker images` 列表中的镜像体积总和并非是所有镜像实际硬盘消耗。由于 Docker 镜像是多层存储结构，并且可以继承、复用，因此`不同镜像`可能会因为使用`相同的基础镜像`，从而拥有共同的层。由于 Docker 使用 Union FS，`相同的层只需要保存一份即可`，因此实际镜像硬盘占用空间很可能要比这个列表镜像大小的总和要小的多。



中间层镜像

```bash
docker image ls -a
```



列出某个仓库镜像

~~~bash
docker image ls ubuntu
~~~



过滤镜像

```bash
docker image ls -f since=mongo:3.2
docker image ls -f before=mongo:3.2
```



只展示镜像id

~~~
docker image ls -q
~~~



[Go 的模板语法](https://gohugo.io/templates/go-templates/)

按照格式列出结果

~~~
docker image ls --format "{{.ID}}: {{.Repository}}"
docker image ls --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
~~~







#### docker rmi / docker image rm

并非所有的 `docker image rm` 都会产生删除镜像的行为，有可能仅仅是取消了某个标签而已。

因为一个镜像可能会有多个标签



删除所有仓库名为 `redis` 的镜像

~~~bash
docker image rm $(docker image ls -q redis)
~~~

删除所有在 `mongo:3.2` 之前的镜像

~~~
docker image rm $(docker image ls -q -f before=mongo:3.2)
~~~



#### docker image prune

​	删除`虚悬镜像(dangling image)`

​	虚晃镜像就是`docker images 下显示的,既没有仓库名，也没有标签，均为none `的镜像



#### docker commit

当我们运行一个容器的时候（如果不使用卷的话），我们做的任何文件修改都会被记录于容器存储层里。而 Docker 提供了一个 `docker commit` 命令，可以将容器的存储层保存下来成为镜像。换句话说，就是在原有镜像的基础上，再叠加上容器的存储层，并构成新的镜像。以后我们运行这个新镜像的时候，就会拥有原有容器最后的文件变化。

使用docker commit 得到的镜像叫黑箱镜像

慎用 docker commit, 因为会加入很多无关的内容， 可能会导致镜像过于臃肿



#### docker diff

我们修改了容器的文件，也就是改动了容器的存储层。我们可以通过 `docker diff` 命令看到具体的改动



#### docker history

可以用 `docker history` 具体查看镜像内的历史记录

~~~
docker history nginx:v2
~~~





# 容器命令



#### docker run 

```bash
docker run -dit --rm ubuntu:18.04 bash
docker run --name webserver -d -p 80:80 nginx # -p <宿主端口>:<容器端口>
```





#### docker exec

~~~
docker exec -it 容器-id bash
~~~





# docker 系统命令



#### docker system ls 

查看镜像、容器、数据卷所占用的空间。



