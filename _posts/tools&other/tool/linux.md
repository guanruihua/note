---
title: linux
date: 2020-10-19 19:34:15
tags:
- linux
- tool
---

# linux 常用功能命令

## 系统服务管理

### systemctl

- 输出系统中各个服务的状态：

```bash
systemctl list-units --type=service
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162a4584ba2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 查看服务的运行状态：

```basic
systemctl status firewalld
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162a7cea49d?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 关闭服务：

```basic
systemctl stop firewalld
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162a5b0b6cd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 启动服务：

```
systemctl start firewalld
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162a5d6dd12?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 重新启动服务（不管当前服务是启动还是关闭）：

```
systemctl restart firewalld
```

- 重新载入配置信息而不中断服务：

```
systemctl reload firewalld
```

- 禁止服务开机自启动：

```
systemctl disable firewalld
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162a7e369bb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 设置服务开机自启动：

```
systemctl enable firewalld
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162ab9b13c0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



## 文件管理

### ls

列出当前目录(/)下的所有文件：

```
ls -l /
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162dbec17e3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### pwd

获取目前所在工作目录的绝对路径



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162eeb30919?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### cd

改变当前工作目录：

```
cd /usr/local
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162dbdb0ab7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### date

显示或修改系统时间与日期；

```
date '+%Y-%m-%d %H:%M:%S'
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162dfe5b742?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### passwd

用于设置用户密码：

```
passwd root
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162e338f464?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### su

改变用户身份（切换到超级用户）：

```
su -
```

### clear

用于清除屏幕信息

### man

显示指定命令的帮助信息：

```
man ls
```

### who

- 查询系统处于什么运行级别：

```
who -r
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51162e698c013?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 显示目前登录到系统的用户：

```
who -buT
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b511630bc1f624?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### free

显示系统内存状态（单位MB）：

```
free -m
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b511630cd0f6ac?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### ps

显示系统进程运行动态：

```
ps -ef
```

查看sshd进程的运行动态：

```
ps -ef | grep sshd
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116311345b24?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### top

查看即时活跃的进程，类似Windows的任务管理器



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116320add416?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### mkdir

创建目录



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b511631b5afd83?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### more

用于文件过长时分页查看文件内容 每页10行查看boot.log文件

```
more -c -10 /var/log/boot.log
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b511632ca209ea?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### cat

查看Linux启动日志文件文件，并标明行号：

```
cat -Ab /var/log/boot.log
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51163327dc58f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### touch

创建text.txt文件：

```
touch text.txt
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b511632fd15d48?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### rm

- 删除文件：

```
rm text.txt
```

- 强制删除某个目录及其子目录：

```
rm -rf testdir/
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116348d0372b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### cp

将test1目录复制到test2目录

```
cp -r /mydata/tes1 /mydata/test2
```

### mv

移动或覆盖文件：

```
mv text.txt text2.txt
```

## 压缩与解压

### tar

- 将/etc文件夹中的文件归档到文件etc.tar（并不会进行压缩）：

```
tar -cvf /mydata/etc.tar /etc
```

- 用gzip压缩文件夹/etc中的文件到文件etc.tar.gz：

```
tar -zcvf /mydata/etc.tar.gz /etc
```

- 用bzip2压缩文件夹/etc到文件/etc.tar.bz2：

```
tar -jcvf /mydata/etc.tar.bz2 /etc
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116348c92218?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 分页查看压缩包中内容（gzip）：

```
tar -ztvf /mydata/etc.tar.gz |more -c -10
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51163516fe371?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 解压文件到当前目录（gzip）：

```
tar -zxvf /mydata/etc.tar.gz
```

## 磁盘和网络管理

### df

查看磁盘空间占用情况：

```
df -hT
```

### dh

查看当前目录下的文件及文件夹所占大小：

```
du -h --max-depth=1 ./*
```

### ifconfig

显示当前网络接口状态



### netstat

- 查看当前路由信息：

```
netstat -rn
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116371dfc6d7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 查看所有有效TCP连接：

```
netstat -an
```

- 查看系统中启动的监听服务：

```
netstat -tulnp
```



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b51163683161fe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- 查看处于连接状态的系统资源信息：

```
netstat -atunp
```

### wget

从网络上下载文件



![展示图片](https://user-gold-cdn.xitu.io/2019/6/13/16b5116376d3a399?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



## 软件的安装与管理

### rpm

- 安装软件包：rpm -ivh nginx-1.12.2-2.el7.x86_64.rpm
- 模糊搜索软件包：rpm -qa | grep nginx
- 精确查找软件包：rpm -qa nginx
- 查询软件包的安装路径：rpm -ql nginx-1.12.2-2.el7.x86_64
- 查看软件包的概要信息：rpm -qi nginx-1.12.2-2.el7.x86_64
- 验证软件包内容和安装文件是否一致：rpm -V nginx-1.12.2-2.el7.x86_64
- 更新软件包：rpm -Uvh nginx-1.12.2-2.el7.x86_64
- 删除软件包：rpm -e nginx-1.12.2-2.el7.x86_64

### yum

- 安装软件包： yum install nginx
- 检查可以更新的软件包：yum check-update
- 更新指定的软件包：yum update nginx
- 在资源库中查找软件包信息：yum info nginx*
- 列出已经安装的所有软件包：yum info installed
- 列出软件包名称：yum list nginx*
- 模糊搜索软件包：yum search nginx