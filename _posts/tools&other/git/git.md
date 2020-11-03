---
title: git
date: 2020-09-08 20:51:24
tags:
	- git
---

# git

## 前言

> 工具:  [TortoiseGit](https://gitee.com/enterprises?utm_source=baidu&utm_medium=sem&utm_term=110206&utm_campaign=enterprise&bd_vid=8015310045877046198)

## git常用指令

```git
git init
git add .
git commit -m 'message'
git remote add origin 远程库地址
git push -u origin main
```



```bash
echo "# note" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:guanruihua/note.git
git push -u origin main
                
```







```bash
git remote add origin git@github.com:guanruihua/note.git
git branch -M main
git push -u origin main
```







## 一台电脑同时使用gitee和github

### 创建ssh key

```git
# 进入用户目录下的 .ssh 文件夹下，路径会因你使用的操作系统不同而略有差异
# 没有这个文件夹也无所谓，直接运行下一句命令也可以
cd ~/.ssh

# 生成 key，将邮件地址替换为你 Gitee 或者 Github 使用的邮件地址
ssh-keygen -t rsa -C "xxx@xxx.com"

# gitee
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/your_user_name/.ssh/id_rsa): id_rsa_gitee
Enter passphrase (empty for no passphrase)://这里直接回车
Enter same passphrase again://这里直接回车
# github
重复上过程,吧id_rsa_gitee 改成 id_rsa_github
```

### 在gitee和github添加public key

```git
cd ~/.ssh
cat id_rsa_gitee.pub
//这里 gitee 的public key
cat id_rsa_github.pub
//这里 github 的public key
```

然后再分别添加到github 和 gitee 的 SSH

### 创建配置文件

在.ssh文件夹创建config文件, 添加内容 区分 两个 ssh key

```git
# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_gitee

# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_github
```

### 测试连接是否正常

```git
ssh -T git@github.com

Hi guanruihua! You've successfully authenticated, but GitHub does not provide shell access.


ssh -T git@gitee.com

Hi grh-gitee! You've successfully authenticated, but GITEE.COM does not provide shell access.


```

