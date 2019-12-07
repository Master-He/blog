---
title: docker-03-安装
date: 2018-05-07 08:09:19
tags: docker
category: 后端
---





[TOC]





#Ubuntu

~~~shell
# install docker
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
docker --version


# docker 免root登录
sudo groupadd docker     #添加docker用户组，（这一步可省略, 因为一般装dokcer都会自动创建用户组）
sudo gpasswd -a $USER docker     #将登陆用户加入到docker用户组中
newgrp docker     #更新用户组
docker ps  *#测试docker命令是否可以使用sudo正常使用*


# install docker-compose
# sudo su
curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
# remove docker-compose
# rm /usr/local/bin/docker-compose
~~~







# MacOS



安装有两种方法：

	1. 直接去官网下载安装
 	2. 用Homebrew 的 Cask 安装 ： brew cask install docker



默认安装了docker-compose， 不需要再单独安装