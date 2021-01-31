> Author: 罗永升
>
> Version: 0.1(20201029)



[TOC]

# 一. Docker介绍

## 1.1 引言

> 1. 我本地运行没问题啊。
>
>    ```
>     环境不一致
>    ```
>
> 2. 哪个哥们又写死循环了，怎么这么卡？
>
>    ```
>     在多用户的操作系统下，会互相影响。
>    ```
>
> 3. 淘宝在双11的时候，用户量暴增。
>
>    ```
>     运维成本过高的问题。
>    ```
>
> 4. 学习一门技术，学习安装成本过高。
>
>    ```
>     关于安装软件成本过高。
>    ```

## 1.2 容器发展历史

#### 1.2.1 落后的旧时代

> 业务是基于应用（Application）运转的。如果应用出现故障，业务也就无法正常运行，甚至会导致商业公司的破产。这种情况是真实的，甚至每天都在发生。
>
> 大部分应用是运行在服务器之上的。曾经，每个服务器只能运行单一应用。Windows 和 Linux 操作系统都没有相应的技术手段来保证在一台服务器上稳定而安全地同时运行多个应用。
>
> 在那个时代，经常会出现这样一幕：每次业务部门想要增加一个新的应用时，IT 部门就需要去采购一个新的服务器。大部分情况下，没有人知道新增应用所需的服务器性能究竟是怎样的，这意味着 IT 部门需要凭借经验去猜测所购买的服务器型号和规格。
>
> 因此，IT 部门在采购的时候就不得不买那些性能大幅优于业务需求的服务器。毕竟无论是 IT 部门还是业务部门，都不想看到服务器性能不足的情况出现。因为服务器性能不足，可能会导致某些交易失败，而交易失败会使得公司客户流失、收益下降，所以 IT 部门通常采购的都是更大、更好的服务器。这种做法导致了大部分服务器长期运行在他们额定负载 5%～ 10% 的水平区间之内。这对公司资产和资源是一种极大的浪费！

#### 1.2.2 你好，VMware

> 为了解决上面的问题，VMware 公司给全世界带来了一个礼物——虚拟机（VM）。然后几乎是一夜之间，世界就变得美好了！人们终于拥有了一种允许多应用能够稳定、安全地同时运行在一个服务器中的技术。
>
> 虚拟机是一种具有划时代意义的技术！每当业务部门需要增加应用的时候，IT 部门无须采购新的服务器。取而代之的是，IT 部门会尝试在现有的，并且有空闲性能的服务器上部署新的应用。
>
> 突然之间，人们发现这种技术能够让现有的资产（如服务器）拥有更大的价值，从而最终为公司节省大量的资金支出。

#### 1.2.3 虚拟机的不足

> 但是……总有这么一个但是！就连 VM 这么伟大的技术，也远未做到十全十美！
>
> 实际上，虚拟机最大的缺点就是依赖其专用的操作系统（OS）。OS 会占用额外的 CPU、RAM 和存储，这些资源本可以用于运行更多的应用。每个 OS 都需要补丁和监控。另外在某些情况下，OS 需要许可证才能运行。这对运营成本（OPEX）和资金性支出（CAPEX）都是一种浪费。
>
> 虚拟机技术也面临着一些其它挑战。比如虚拟机启动通常比较慢，并且可移植性比较差——虚拟机在不同的虚拟机管理器（Hypervisor）或者云平台之间的迁移要远比想象中困难。

#### 1.2.4 你好，容器

> 长期以来，像谷歌（Google）这样的大规模 Web 服务（Big Web-Scale）玩家一直采用容器（Container）技术解决虚拟机模型的缺点。
>
> 容器模型其实跟虚拟机模型相似，其主要的区别在于，容器的运行不会独占操作系统。实际上，运行在相同宿主机上的容器是共享一个操作系统的，这样就能够节省大量的系统资源，如 CPU、RAM 以及存储。容器同时还能节省大量花费在许可证上的开销，以及为 OS 打补丁等运维成本。最终结果就是，容器节省了维护成本和资金成本。
>
> 同时容器还具有启动快和便于迁移等优势。将容器从笔记本电脑迁移到云上，之后再迁移到数据中心的虚拟机或者物理机之上，都是很简单的事情。

#### 1.2.5 Linux 容器

> 现代的容器技术起源于 Linux，是很多人长期努力持续贡献的产物。举个例子，Google LLC 就贡献了很多容器相关的技术到 Linux 内核当中。没有大家的贡献，就没有现在的容器。
>
> 近几年来，对容器发展影响比较大的技术包括**内核命名空间（Kernel Namespace）**、**控制组（Control Group）**、**联合文件系统（Union File System）**，当然更少不了 **Docker** 。再次强调一遍，当今的容器生态环境很大程度上受益于强大的基金会，而基金会是由很多独立开发者以及公司组织共同创建并维护的。感谢你们！
>
> 虽然容器技术已经如此出色，但对于大部分组织来说，容器技术的复杂度是阻止其实际应用的主要原因。直到 Docker 技术横空出世，容器才真正被大众所接受。
>
> 注：
>
> > 有很多跟容器类似的操作系统虚拟化技术要早于 Docker 和现代容器技术出现，有些甚至可以追溯到大型机上的 System/360 操作系统当中。BSD Jails 和 Solaris Zones 也是在类 UNIX 操作系统上众所周知的容器化技术。但本实验讨论内容范围主要会限制在由 Docker 主导的现代容器技术之中。

#### 1.2.6 Windows 容器

> 在过去的几年中，微软（Microsoft Corp.）致力于 Docker 和容器技术在 Windows 平台的发展。
>
> Windows 容器已经能在 Windows 10 和 Windows Server 2016 平台上使用了。为了实现这个目标，微软跟 Docker 公司、社区展开了深入合作。
>
> 实现容器所需的核心 Windows 内核技术被统称为 Windows 容器（Windows Container）。用户空间是通过 Docker 来完成与 Windows 容器之间交互的，这使得 Docker 在 Windows 平台上的使用体验跟在 Linux 上几乎一致。那些熟悉 Linux Docker 工具的研发人员和系统管理员，在切换到 Windows 容器之后也会很快适应。

#### 1.2.7 Windows 容器 VS Linux 容器

> 运行中的容器共享宿主机的内核，理解这一点是很重要的。这意味着一个基于 Windows 的容器化应用在 Linux 主机上是无法运行的。读者也可以简单地理解为 Windows 容器需要运行在 Windows 宿主机之上，Linux 容器（Linux Container）需要运行在 Linux 宿主机上。但是，实际场景要比这复杂得多……
>
> 截至目前，在 Windows 机器上运行 Linux 容器已经成为可能。例如，Windows 版 Docker（由 Docker 公司提供的为 Windows 10 设计的产品）可以在 Windows 容器模式和 Linux 容器模式之间进行切换。这是一个正在快速发展的领域，如果大家想要了解，需要查阅 Docker 最新文档。

#### 1.2.8 Mac 容器现状

> 迄今为止，还没有出现 Mac 容器（Mac Container）。
>
> 但是读者可以在 Mac 系统上使用 Docker for Mac 来运行 Linux 容器。这是通过在 Mac 上启动一个轻量级 Linux VM，然后在其中无缝地运行 Linux 容器来实现的。这种方式在开发人员中很流行，因为这样可以在 Mac 上很容易地开发和测试 Linux 容器。

#### 1.2.9 Kubernetes

> Kubernetes 是谷歌的一个开源项目，并且开源之后迅速成为容器编排领域的领头羊。有一种很流行的说法：Kubernetes 是保证容器部署和运行的软件体系中很重要的一部分。
>
> 截至目前，Kubernetes 已经采用 Docker 作为其默认容器运行时（container runtime，注意，“容器运行时” 是一个完整概念，这里没有错误），包括 Kubernetes 启动和停止容器，以及镜像的拉取等。但是，Kubernetes 也提供了一个可插拔的容器运行时接口 CRI。CRI 能够帮助 Kubernetes 实现将运行时环境从 Docker 快速替换为其它容器运行时。在未来，Kubernetes 中的默认容器运行时可能由 Docker 替换为 containerd 。
>
> 关于 Kubernetes，大家现在需要了解的就是 —— Kubernetes 是 Docker 之上的一个平台，现在采用 Docker 实现其底层容器相关的操作。
>
> 关于容器技术的图书和探讨总是不可避免地涉及 Docker。但是当有人提到“Docker”时，可能是指如下 3 种概念之一：
>
> - Docker 公司
> - Docker 的容器运行时和编排引擎
> - Docker 开源项目（Moby）

#### 1.2.10 Docker的由来

> 一帮年轻人创业，创办了一家公司，2010年的专门做PAAS平台。
>
> 到了2013年的时候，像亚马逊、微软、Google都开始做PAAS平台。
>
> 2013年，将公司内的核心技术对外开源，核心技术就是Docker。
>
> 到了2014年的时候，得到了C轮融资，$4000W
>
> 到了2015年的时候，得到了D轮融资，$9500W
>
> 全神贯注的维护Docker。
>
> 所罗门主要作者之一。
>
> Docker的作者已经离开了维护Docker的团队。
>
> Docker 是一种运行于 Linux 和 Windows 上的软件，用于创建、管理和编排容器。Docker 是在 GitHub 上开发的 Moby 开源项目的一部分。Docker 公司，位于旧金山，是整个 Moby 开源项目的维护者。Docker 公司还提供包含支持服务的商业版本的 Docker。

![Docker作者](Typora_images\4c6d8d923d3e903eb286718c2fec20092)

## 1.3 Docker的思想

![image-20201029231439528](Typora_images\image-20201029231439528.png)

> 1. 集装箱：
>    1. 会将所有需要的内容放到不同的集装箱中，谁需要这些环境就直接拿到这个集装箱就可以了
> 2. 标准化：
>    1. 运输的标准化：Docker有一个码头，所有上传的集装箱都放在了这个码头上，当谁需要某一个环境，就直接指派大海豚去搬运这个集装箱就可以了。
>    2. 命令的标准化：Docker提供了一系列的命令，帮助我们去获取集装箱等等操作。
>    3. 提供了REST的API：衍生出了很多图形化界面，Rancher。
> 3. 隔离性：
>    1. Docker在运行集装箱内的内容时，会在LInux的内核中，单独的开辟一片空间，这片空间不会影响到其他程序。

> - 注册中心。（超级码头，上面放的就是集装箱）
> - 镜像。（集装箱）
> - 容器。（运行起来的镜像）

# 二. Docker的基本操作

## 2.1 安装Docker

> 要安装Docker Engine，您需要以下Ubuntu版本之一的64位版本：
>
> - Ubuntu Focal 20.04（LTS）
> - Ubuntu Bionic 18.04（LTS）
> - Ubuntu Xenial 16.04（LTS）
>
> Docker Engine在`x86_64`（或`amd64`）`armhf`，和`arm64`体系结构上受支持。

#### 2.1.1 使用官方安装脚本自动安装

安装命令如下：

```shell
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

也可以使用国内 daocloud 一键安装命令：

```shell
curl -sSL https://get.daocloud.io/docker | sh
```

#### 2.1.2 手动安装(先将虚拟机修改成NAT方式)

```shell
# 1. 卸载旧版本, Docker 的旧版本被称为 docker，docker.io 或 docker-engine 。当前称为 Docker Engine-Community 简称 docker-ce。如果已安装，请卸载它们：
sudo apt-get remove docker docker-engine docker.io containerd runc
```

```shell
# 2. 首先更新 apt 软件包数据库，以确保软件包列表是最新的。
sudo apt-get update
```

```shell
# 3. 安装一些软件包，以允许 apt 通过 HTTPS 使用存储库：
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```

```shell
# 4. 首先，我们添加阿里云提供的镜像源以便于加快国内安装速度，先添加相应的密钥：
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```

```shell
# 5. 再添加相应源的信息，在新主机上首次安装 Docker Engine-Community 之前，需要设置 Docker 仓库。之后，您可以从仓库安装和更新 Docker 。：
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
```

```shell
# 6.再更新 apt 索引库
sudo apt-get update
# 安装 docker-ce
sudo apt-get install docker-ce
# 在安装成功后，Docker 的守护进程自动启动，不需要手动启动服务。此时，我们可以查看其版本信息，使用如下命令：
docker version
```

|             环境中的 Docker 版本信息如下图所示：             |
| :----------------------------------------------------------: |
| ![image-20201030145743116](Typora_images\image-20201030145743116.png) |

> 自己搭建的 Docker 环境，可能会提示我们没有相应的权限连接到 Docker 守护进行绑定的 Unix 套接字。
>
> 默认情况下，该套接字归属于 `root` 用户，对于其它用户只能通过 `sudo` 来进行访问。
>
> 要让 `jluzh` 用户可以直接执行 Docker 命令而不必在每次执行时都输入 `sudo` 来获得权限，我们可以将要执行 Docker 命令的用户添加到用户组 Docker 中。该用户组会在安装后自动创建，我们只需执行添加用户到 Docker 用户组的操作：
>
> ```shell
> sudo usermod -aG docker jluzh
> ```
>
> 在添加成功后，我们还需要重新打开一个 `shell` 修改才能生效。使用如下命令:
>
> ```shell
> sudo su jluzh
> ```
>
> 在这之后运行docker不需要 sudo docker run XX 。改为docker run XX。

#### 2.2 Docker的中央仓库

> 1. Docker官方的中央仓库：这个仓库是镜像最全的，但是下载速度很慢。[https://hub.docker.com](https://hub.docker.com/)
> 2. 国内的镜像网站：网易蜂巢、daoCloud、阿里云 (推荐使用)
> 3. 在公司内部会采用私服的方式拉取镜像。

首先，我们需要编辑 `/etc/docker/daemon.json` 文件：

```shell
sudo vi /etc/docker/daemon.json
```

然后加入如下内容：

```json
{
  "registry-mirrors": ["https://n6syp70m.mirror.aliyuncs.com"]
}
```

修改之后，需要重启 Docker和Daemon 服务，让修改生效。使用如下命令：

```shell
sudo systemctl daemon-reload
sudo service docker restart
# sudo systemctl restart docker
# sudo systemctl stop docker
# sudo systemctl start docker
```

在安装之后，我们可以通过运行一个 `hello-world` 的镜像来验证 `Docker CE` 是否被正确的安装，使用如下命令：

```shell
docker run hello-world
```

| 先从本地仓库找hello-world镜像，不存在再云远程仓库(阿里云)拉取下来 |
| :----------------------------------------------------------: |
| ![image-20201030152802692](G:\Typora_images\image-20201030152802692.png) |

#### 2.3 镜像的操作

```shell
# 1. 拉取镜像到本地
docker pull 镜像名称[:tag]
# 举个例子
docker pull tomcat:8.5.15-jre8
```

```shell
# 2. 查看全部本地的镜像
docker images
```

```shell
# 3. 删除本地镜像
docker rmi 镜像的标识
```

```shell
# 4. 镜像的导入导出（不规范）
# 将本地的镜像导出
docker save -o 导出的路径 镜像id
# 加载本地的镜像文件
docker load -i 镜像文件
# 修改镜像名称
docker tag 镜像id 新镜像名称:版本
```

#### 2.4 容器的操作

```shell
# 1. 运行容器
# 简单操作
docker run 镜像的标识|镜像名称[:tag]
# 常用的参数
docker run -d -p 宿主机端口:容器端口 --name 容器名称 镜像的标识|镜像名称[:tag]
# -d：代表后台运行容器
# -p 宿主机端口:容器端口：为了映射当前Linux端口和容器端口
# --name 容器名称：指定容器的名称
```

```shell
# 2. 查看正在运行的容器
docker ps [-qa]
# -a：查看全部的容器，包括没有运行
# -p：只查看容器得到标识
```

```shell
# 3. 查看容器的日志
docker logs -f 容器id
# -f：可以滚动查看日志的最后几行
```

```shell
# 4. 进入到容器内部
docker exec -it 容器id bash
```

```shell
# 5. 删除容器（删除容器前，需要停止容器）
# 停止指定的容器
docker stop 容器id
# 停止全部容器
docker stop $(docker pa -qa)
# 删除指定的容器
docker rm 容器id
# 删除全部容器
docker rm $(docker pa -qa)
```

```shell
# 6. 启动容器
docker start 容器id
```

#### 2.5 Docker安装Nginx

Nginx 是一个高性能的 HTTP 和反向代理 web 服务器，同时也提供了 IMAP/POP3/SMTP 服务 。

```shell
# 1、查看可用的 Nginx 版本
# 访问 https://hub.daocloud.io/ 搜索 Nginx
```

```shell
# 2、我们还可以用 docker search nginx 命令来查看可用版本： -s 100 表示收藏收大于100
docker search nginx -s 100
```

```shell
# 3、从远程仓库拉取最新(latest)的nginx。
docker pull nginx:latest
```

```shell
# 4、使用以下命令来查看是否已安装了nginx镜像：
docker images
```

```shell
# 5、完成后，我们可以使用以下命令来运行 nginx 容器：
docker run --name nginx-test -p 80:80 -d nginx
```

```shell
# 6、查看容器是否运行
docker ps
# 或访问  http://服务器ip:80
```

|                          docker ps                           |                      http://服务器ip:80                      |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![image-20201030163358470](Typora_images\image-20201030163358470.png) | ![image-20201030163310636](Typora_images\image-20201030163310636.png) |

#### 2.6 Docker相关命令

|     命令      |          说明          |
| :-----------: | :--------------------: |
|  docker info  | 查看系统的一些相关信息 |
| docker --help | 查看相关命令的详细说明 |
|               |                        |
|               |                        |
|               |                        |

