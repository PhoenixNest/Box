> Author: 罗永升
>
> Version: 0.1(20201029)

[TOC]

# 1、简介

Ubuntu是一款基于 Debian Linux 的以桌面应用为主的操作系统，内容涵盖文字处理、电子邮件、软件开发工具和 Web 服务等，可供用户免费下载、使用和分享。一般分为：desktop和server版。

## 1.1 安装包下载

1、中科大 http://mirrors.aliyun.com/ubuntu-releases/     2、阿里云 http://mirrors.aliyun.com/ubuntu-releases/

## 1.2 安装完需要做的事

http://centos.ustc.edu.cn/help/ubuntu.html

# 2、修改镜像源

先备份sources.list 文件：

```shell
sudo mv  /etc/apt/sources.list /etc/apt/sources.list.old
```

可以直接编辑 /etc/apt/sources.list 文件（需要使用 sudo）。以下是 Ubuntu 16.04 参考配置内容：

```shell
sudo vi /etc/apt/sources.list
# ggdG清空所有内容，再按i插入
```

![image-20201029122528499](Typora_images\image-20201029122528499.png)

```shell
# 添加阿里云镜像
deb http://mirrors.aliyun.com/ubuntu/ xenial main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main

deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main

deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe

deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe

```

```shell
# 默认注释了源码仓库，如有需要可自行取消注释
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse

```

更改完 `sources.list` 文件后保存文件，按Esc,输入:wq 回车Enter保存退出。

因为使用阿里去镜像，加多个DNS，加快速度。

```shell
sudo vi /etc/resolv.conf
```

打开后添加

```shell
#阿里的dns  因为我用的是阿里的源哦 这里要根据你使用的源修改
nameserver 223.5.5.5
```

接下来 重启网络服务

```shell
/etc/init.d/networking restart
```

再运行 `sudo apt-get update` 更新索引以生效。

# 3、附错误处理

> 因为Ubuntu16.04版本有点旧。在`apt-get update`时可能会出现一些错误。
>
> N: 无法认证来自该源的数据，所以使用它会带来潜在风险。
>
> N: 无法安全地用该源进行更新，所以默认禁用该源。
>
> ##### 1. 进入 sources.list.d 文件 命令如下：
>
> ```shell
> cd /etc/apt/sources.list.d
> ```
>
> ##### 2. 移动文件
>
> ```shell
> sudo mv fkrull-ubuntu-deadsnakes-artful.list fkrull-ubuntu-deadsnakes-artful.list.save
> ```
>
> ##### 3. 再次更新
>
> ```shell
> sudo apt-get update
> ```

# 4、Putty

下载安装地址：https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

运行 PuTTY 就可以看到下面这个界面，在这里输入服务器的 IP或主机名，选择好登录协议，还有协议的端口，如果希望把这次的输入保存起来，以后就不需要再重新输入了，就在第4步输入好会话保存的名称，比如：mail-server，或者干脆就是主机的地址，点击保存就可以了。

![img](Typora_images\05233810-f79a18779a7a48b5b8fd05ae82ef891b.png)

最后点下面的 Open 按钮，输入正确的用户名和口令，就可以登录服务器了。第一次登录时，会看到这个对话框

![img](Typora_images\05234157-d4169cd8acaa46d99803fc5eaee30f0b.png)

这是要告诉你登录的主机密钥指纹，点 Yes 就保存起来，以后就不会再弹出这个窗口，然后就正常登录。点 No 不保存，下次还是要提示你，然后也可以正常登录。如果一台主机我们只是临时登录一下，当然就是点 No 了。Cancel 就是取消，也就是取消了这次登录。 如果你曾经登录过这台主机，但是又弹出来这个对话框，可能有以下几种情形：

- 主机重新安装了操作系统
- 这台主机可能有多个IP，这次用的是另外一个 IP
- 有其他不怀好意的主机来冒充，诱骗我们登录，窃取隐秘信息

![image-20201029125255848](Typora_images\image-20201029125255848.png)

相关详细使用教程

https://www.cnblogs.com/yuwentao/archive/2013/01/06/2846953.html

