---
layout: post
title:  "GitHub 安装"
date:   2018-07-05 17:50:58 +0800
categories: A2
---

# 能力

```
GitLab includes Git repository management, issue tracking, code review, an IDE, activity streams, wikis, and more.
```


# 相关链接
```

https://about.gitlab.com/downloads/#centos7

http://www.cnblogs.com/moxiaoan/p/5683743.html

http://www.centoscn.com/image-text/install/2015/0320/4929.html
```

# 安装gitlab
为了提高软件安装速度，将yum源设置为阿里云开源镜像

```
cd /etc/yum.repos.d
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```
安装依赖软件

```
yum -y install libicu-devel patch gcc-c++ readline-devel zlib-devel libffi-devel openssl-devel make autoconf automake libtool bison libxml2-devel libxslt-devel libyaml-devel zlib-devel openssl-devel cpio expat-devel gettext-devel curl-devel perl-ExtUtils-CBuilder perl-ExtUtils-MakeMaker
```
打开HTTP SSH的 系统防火墙

```
sudo yum -y install curl policycoreutils openssh-server openssh-clients
sudo systemctl enable sshd
sudo systemctl start sshd
sudo yum -y install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
```
 Add the GitLab package server and install the package

```
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
sudo yum -y install gitlab-ce
```

# 问题与解决

---
## 将项目路径的localhost改为IP

```
cd /opt/gitlab/embedded/service/gitlab-rails/config    

vim gitlab.yml

gitlab-ctl restart
```
## 用户配置

```
git config --global user.name "lubin"   
git config --global user.email lubin.z@gmail.com  
```
