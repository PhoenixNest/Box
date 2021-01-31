> Author: 罗永升
>
> Version: 0.1(20201029)



### 1、VMware创建虚拟机

> VMware Workstations安装Linux系统之Centos7系统详细过程图解

|                           详细过程                           |
| :----------------------------------------------------------: |
| ![image-20201101092617874](Typora_images\image-20201101092617874.png) |
| ![image-20201101092648463](Typora_images\image-20201101092648463.png) |
| ![image-20201101092810279](Typora_images\image-20201101092810279.png) |
| ![image-20201101092845859](Typora_images\image-20201101092845859.png) |
| ![image-20201101092915995](Typora_images\image-20201101092915995.png) |
| ![image-20201101092943530](Typora_images\image-20201101092943530.png) |
| ![image-20201101093048330](Typora_images\image-20201101093048330.png) |
| ![image-20201101093116764](Typora_images\image-20201101093116764.png) |
| ![image-20201101093152553](Typora_images\image-20201101093152553.png) |

| ![image-20201101093236429](Typora_images\image-20201101093236429.png) |
| :----------------------------------------------------------: |
| ![image-20201101093325685](Typora_images\image-20201101093325685.png) |
| ![image-20201101093438489](Typora_images\image-20201101093438489.png) |
| ![image-20201101093505446](Typora_images\image-20201101093505446.png) |
| ![image-20201101093547857](Typora_images\image-20201101093547857.png) |
| ![image-20201101093613385](Typora_images\image-20201101093613385.png) |
| ![image-20201101093639657](Typora_images\image-20201101093639657.png) |
| ![image-20201101093707588](Typora_images\image-20201101093707588.png) |
|                                                              |



### 2、安装Centos

| ![image-20201101093753009](Typora_images\image-20201101093753009.png) |
| :----------------------------------------------------------: |
| ![image-20201101094022403](Typora_images\image-20201101094022403.png) |
| ![image-20201101094054082](Typora_images\image-20201101094054082.png) |
| ![image-20201101094123876](Typora_images\image-20201101094123876.png) |

| ![image-20201101094213528](Typora_images\image-20201101094213528.png) |
| :----------------------------------------------------------: |
| ![image-20201101094246694](Typora_images\image-20201101094246694.png) |
| ![image-20201101094311361](Typora_images\image-20201101094311361.png) |
| ![image-20201101094339614](Typora_images\image-20201101094339614.png) |
| ![image-20201101094405913](Typora_images\image-20201101094405913.png) |
| ![image-20201101094428376](Typora_images\image-20201101094428376.png) |
| ![image-20201101094458480](Typora_images\image-20201101094458480.png) |

| ![image-20201101094536044](Typora_images\image-20201101094536044.png) |
| :----------------------------------------------------------: |
| ![image-20201101094603870](Typora_images\image-20201101094603870.png) |
| ![image-20201101094632239](Typora_images\image-20201101094632239.png) |
| ![image-20201101094654250](Typora_images\image-20201101094654250.png) |
| ![image-20201101094721219](Typora_images\image-20201101094721219.png) |
| ![image-20201101094754579](Typora_images\image-20201101094754579.png) |
| ![image-20201101094831264](Typora_images\image-20201101094831264.png) |

| ![image-20201101094909610](Typora_images\image-20201101094909610.png) |
| :----------------------------------------------------------: |
| ![image-20201101094932211](Typora_images\image-20201101094932211.png) |
| ![image-20201101094955878](Typora_images\image-20201101094955878.png) |
| ![image-20201101095020111](Typora_images\image-20201101095020111.png) |
| ![image-20201101095043852](Typora_images\image-20201101095043852.png) |
| ![image-20201101095109305](Typora_images\image-20201101095109305.png) |
| ![image-20201101095150809](Typora_images\image-20201101095150809.png) |

| ![image-20201101095240403](Typora_images\image-20201101095240403.png) |
| :----------------------------------------------------------: |
| ![image-20201101095308112](Typora_images\image-20201101095308112.png) |
| ![image-20201101095328786](Typora_images\image-20201101095328786.png) |

### 3、附注意事项

> Centos和Ubuntu之间有些命令不一样
>
> 修改网卡配置信息，命令如下：
>
> ```shell
> vi /etc/sysconfig/network-scripts/ifcfg-eth0 
> ```
>
> DEVICE=eth0 网卡对应的设备别名，如ifcfg-eth0第一块网卡,输入命令可以查看网卡信息 
>
> ```shell
> ifconfig
> ifconfig eth0
> ```
>
> 