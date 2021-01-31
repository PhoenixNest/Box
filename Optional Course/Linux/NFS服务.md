> Author: 罗永升
>
> Version: 0.1(20201029)



[TOC]

## 一 ： 服务端

NFS主要功能是通过网络让不同的机器系统之间可以彼此共享文件或目录。NFS客户端可以通过挂载的方式将NFS服务端共享的数据文件目录挂载到NFS客户端本地系统之中。
NFS一般用来存储共享视频，图片，附件等静态数据（用户上传的文件在NFS存储服务器中），是当前互联网系统架构中最常用的服务之一，特别是中小公司应用频率很高。大公司可能用MFS，GFS，FASTFS分布式系统。

NFS常用架构图如下：

![image-20201029223021004](Typora_images\image-20201029223021004.png)

### 1.1  安装NFS服务：

```shell
sudo apt install nfs-kernel-server
```

### 1.2 创建共享目录

```shell
sudo mkdir -p /data/share1
```

### 1.3 编写配置文件

配置共享目录的权限等等

```shell
sudo vi /etc/exports
/data/share1 *(rw,sync,no_subtree_check,no_root_squash)
```

NFS共享的常用参数：

```powershell
访问权限选项

设置输出目录只读：ro
设置输出目录读写：rw
用户映射选项

  all_squash：将远程访问的所有普通用户及所属组都映射为匿名用户或用户组（nfsnobody）；
  no_all_squash：与all_squash取反（默认设置）；
  root_squash：将root用户及所属组都映射为匿名用户或用户组（默认设置）；
  no_root_squash：与rootsquash取反；
  anonuid=xxx：将远程访问的所有用户都映射为匿名用户，并指定该用户为本地用户（UID=xxx）；
  anongid=xxx：将远程访问的所有用户组都映射为匿名用户组账户，并指定该匿名用户组账户为本地用户组账户（GID=xxx）；

其它选项

  secure：限制客户端只能从小于1024的tcp/ip端口连接nfs服务器（默认设置）；
  insecure：允许客户端从大于1024的tcp/ip端口连接服务器；
  sync：将数据同步写入内存缓冲区与磁盘中，效率低，但可以保证数据的一致性；
  async：将数据先保存在内存缓冲区中，必要时才写入磁盘；
  wdelay：检查是否有相关的写操作，如果有则将这些写操作一起执行，这样可以提高效率（默认设置）；
  no_wdelay：若有写操作则立即执行，应与sync配合使用；
  subtree：若输出目录是一个子目录，则nfs服务器将检查其父目录的权限(默认设置)；
  no_subtree：即使输出目录是一个子目录，nfs服务器也不检查其父目录的权限，这样可以提高效率；
```

### 1.4 重启nfs服务

```shell
sudo service nfs-kernel-server restart
```

### 1.5常用命令工具

> 在安装NFS服务器时，已包含常用的命令行工具，无需额外安装。

显示已经mount到本机nfs目录的客户端机器。

```shell
sudo showmount -e localhost
```

showmount命令的用法:

| 参数 | 作用                                      |
| ---- | ----------------------------------------- |
| -e   | 显示NFS服务器的共享列表                   |
| -a   | 显示本机挂载的文件资源的情况NFS资源的情况 |
| -v   | 显示版本号                                |

将配置文件中的目录全部重新export一次！无需重启服务。

```shell
sudo exportfs -rv
```

查看NFS的运行状态

```shell
sudo nfsstat
```

查看rpc（远程调用服务，是nfs的实现协议）执行信息，可以用于检测rpc运行情况

```shell
sudo rpcinfo
```

查看网络端口，NFS默认是使用111端口。

netstat是一款命令行工具，可用于列出系统上所有的网络套接字连接情况，包括 tcp, udp 以及 unix 套接字，另外它还能列出处于监听状态（即等待接入请求）的套接字。

```
-a : 列出所有的连接状态，包括tcp/udp/unix socket等
-t : 仅列出tcp数据包的连接
-u : 仅列出udp数据包的连接
-l : 仅列出已在listen(监听)的服务的网络状态
-p : 列出pid进程号与program文件名
-i : 打印网络接口
-g : 显示IPv4和IPv6的多播组信
-c : 可以设置几秒后自动更新一次，例如-c 5为每5s更新一次网络状态
-s : 显示网络统计数据
-e : 显示更多的信息(如用户ID、网卡IP等)
```

```shell
sudo netstat -tu
```

## 二 : 客户端

### 2.1 安装客户端工具：

> 在需要连接到NFS服务器的客户端机器上

```shell
sudo apt install nfs-common
```

### 2.2 查看NFS服务器上的共享目录

```shell
sudo showmount -e 服务器ip
```

### 2.3 创建本地挂载目录

```shell
sudo mkdir -p /tmp/k8svolume
```

### 2.4 挂载共享目录

\#将NFS服务器ip上的目录，挂载到本地的/mnt/目录下

```shell
sudo mount -t nfs 服务器ip:/data/share1  /tmp/k8svolume
```

## 三：测试服务

### 3.1 在服务端的/data/share1下新建一个文件

```shell
cd /data/share1
sudo touch h.txt
ls
```

### 3.2 在客户端的/tmp/k8svolume下新建一个文件

```shell
cd /tmp/k8svolume
sudo vi hello.txt
ls
```

