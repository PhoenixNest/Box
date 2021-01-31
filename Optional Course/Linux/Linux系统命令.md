> Author: 罗永升
>
> Version: 0.1(20201029)



[TOC]



# 1、修改主机名

```shell
jluzh@ubuntu:/$ hostnamectl set-hostname 名字 #修改名称
jluzh@ubuntu:/$ sudo reboot -f  #需要使用sudo
```

# 2、修改ip地址

## 2.1 第一步：先获取网卡名称

输入ifconfig,如下图,我们的网卡名称为 ens33

![image-20201029131748154](Typora_images\image-20201029131748154.png)

## 2.2 第二步：修改网卡配置文件

```shell
sudo vi /etc/network/interfaces
#信息修改为
auto ens33
iface ens33 inet static
address 192.168.1.10
netmask 255.255.255.0
gateway 192.168.1.1
```

![image-20201029132143200](Typora_images\image-20201029132143200.png)

## 2.3 第三步：修改DNS配置

```shell
# 永久性修改
sudo vi /etc/resolvconf/resolv.conf.d/head
# 临时性修改
sudo vi /etc/resolv.conf
#加个阿里云dns
nameserver 223.5.5.5
```

![image-20201029132402773](Typora_images\image-20201029132402773.png)

![img](Typora_images\855959-20160104142723996-1858541779.png)

## 2.4 第四部：重启网络服务

```shell
 sudo /etc/init.d/networking restart
 # ifconfig如果没有变化，重启机器
 reboot
```

# 3、Linux系统目录结构详解

![img](Typora_images\1783834-20200307181213404-595171540.png)

## 3.1、/bin 存放经常使用的指令，比如ls,cp,rm

## 3.2、/sbin 系统管理员使用的系统管理命令

## 3.3、/home 存放普通用户的主目录

在linux中每个用户都有一个自己的目录,一般该目录是以该用户的账号名为目录名

## 3.4、/root 系统管理员的用户主目录

## 3.5、/boot 存放的是启动linux是的核心文件

## 3.6、/lib 存放库文件的目录

## 3.7、/etc 存放所有系统管理所需要的配置文件

比如我们的网卡

## 3.8、/usr 用户的很多应用程序和文件都放在这个目录

有点像windows中的program files目录

## 3.9、/proc 这是系统内存的映射

## 3.10、/srv service 的缩写

存放的是一些服务启动之后所需要的数据

## 3.11、/sys 系统相关的文件

## 3.12、/tmp 用来存放临时文件

## 3.13、/dev 类型与windows的设备管理器

把所有的硬件用文件的形式存储

## 3.14、/media linux 会识别一些设备

比如u盘，光驱，linux会把这个设备挂载到这个目录底下

## 3.15、/mnt 用于让用户临时挂载别的文件系统

我们可以将外部的存储挂载在/mnt上，我们进入目录进行查看

## 3.16、/opt 这个一般用来放安装包的

## 3.17、/var 存放经常需要被修改的文件，比如日志文件

## 3.18、/usr/local 程序安装后存放的地方

# 4、文件系统常用命令

## 4.1、pwd 显示当前所在的路径

pwd -->print working directory 显示打印当前所在的目录

## 4.2、cd 切换目录结构

```shell
解释：cd --> change directory 改变目录信息 
用法：cd 你想要去的路径 绝对路径：
cd /etc/sysconfig/network-scripts/
相对路径的用法：
cd network-scripts/
快速回到自己进过的目录：
cd -
返回当前路径的上一级目录中：
cd ../
如果返回到当前登入用户的home目录
cd ~
```

## 4.3、mkdir 创建目录信息

```shell
mkdir ---> make directory
用-p参数创建多级目录
mkdir -p file3/file3.1
我们在创建目录的时候做好是绝对路径创建
```

## 4.4、创建文件touch

```shell
touch abc.txt
```

## 4.5、ls检查文件或者目录是否存在，并列出目录下的文件

```shell
#ls -l 默认是创建时间最新到最老排序
# 如何按照时间的创建顺序反排
ls -ltr 
```

## 4.6、cat查看文件信息的命令

```shell
# cat查看文件内容
cat abc.txt
# 查看多个文件的内容同时输出
cat abc.txt  abc1.txt
#将多个文件的内容读取出来以后，放入到一个文件当中
cat abc.txt  abc1.txt > abc2.txt
```

## 4.7、echo将信息进行输出

```shell
# 直接输出信息
echo "hai girl"
#将echo的内容写入文件，> 是覆盖的意思，>> 是追加 
# 格式：echo 内容 > 文件 
# 格式：echo 内容 >> 文件
echo hai girl > abc1.txt
> 是覆盖的意思，会覆盖原来文件内的内容
>> 是追加
echo you are so pretty >> abc1.txt
```

## 4.8、cp复制

```shell
cp ---> copy
 语法格式： cp 参数（可选） 要进行复制的信息  复制到什么位置
 #复制文件 在复制文文件时，不要在文件名称后面加/,一般只能在目录后面加/ 
cp abc.txt abc3.txt 
 #如果存在会请求你是否覆盖 
cp test.txt abc.txt 
cp: overwrite ‘abc.txt’? y 
 #复制文件夹 
 cp -r loveyou/ loveyou1/ 
 
cp  参数： 
-d 和链接相关的文件
-r 进行递归复制 
-p 保持属性不变 
-a == -drp 

#利用cp 
cp abc.txt test1.txt  
# 多文件信息重复，会多次确认提示
```

## 4.9、mv剪切命令

mv -->move 对文件或者文件夹进行剪切（移动） 语法格式 ： mv 参数（可选） 要移动的文件或者文件夹  移动什么位置 可以是绝对路径也可以是相对路径（绝对路径是从根目录开始的路径）

```shell
移动文件
mv file2.txt test
移动文件夹
mv test/ dir1/
# 利用mv 命令给文件重命名
mv file2.txt file.txt
```

## 4.10、rm 命令（删除）

rm --->remove 语法 ：rm 参数 要删除的数据信息

```shell
#删除文件
rm file.txt
#删除文件夹
rm -f /movie/
# 强制删除rm -rf，该命令不会询问直接删除
rm -rf /movie/
```

## 4.11、vim 编辑器

![img](Typora_images\1783834-20200307181327086-1596452953.png)

> **vim 有几种状态** 
>
> ​		1 正常模式（我们用vim打开文件就是进入正常模式） 比如复制，粘贴等 
>
> ​		2 插入模式 在插入模式下，我们们输入内容，编辑内容 如何从正常模式切换插入模式：i,o,a,I，O,A,R任意一个键都能重正常模式进入插入模式 正常习惯按i,因为好记，i-->insert
>
> ​		3 命令模式 在这个模式下，我们可以输入相关的命令，比如退出，保存，等操作 
>
> 总结：vim三种模式可以随意切换
>
> **正常模式下的命令**:    
>
> ​	拷贝：yy  粘贴：p    
>
> ​	拷贝当前行向下2行，并粘贴
>
> ​	拷贝2行：2yy
>
> ​	拷贝几行数字就是几
>
> ​	粘贴：p
>
> ​	删除当前行
>
> ​	删除：dd
>
> ​	向下删除2行 
>
> ​	删除：2dd 
>
> ​	光标移到最后一行：G 
>
> ​	光标移动了首行： gg 
>
> ​	光标移动2行： 2gg 
>
> ​	 撤销： u
>
> **编辑模式下：进入以后就可以编辑**
>
> **命令模式：**
>
> ​	1 查找内容
> ​    ：/关键字
> ​    2 取消高亮
> ​    ：nohl
> ​    3 显示行数
> ​    ：set nu
> ​    4 取消行号
> ​    ：set nonu
> ​    5 没有修改的情况下推出
> ​    ：q
> ​    6如果我们改了，但是我们不想他保存
> ​    :q!
> ​    7 如果我们改了，并想保存退出，
> ​    ：wq

## 4.12、stat命令

查看文件的访问时间，修改时间等

```shell
stat file.txt
```



## 4.13、关机、重启命令

shutdown 命令： 

- shutdown -h now   #立即关机 

- shutdown -h 1     #1分钟后关机 

- shutdown -r now   # 立即重启 

- shutdown -r 1     #1分钟后重启  

  halt 关机 

  reboot 重启 

  sync  把内存中的数据同步到硬盘中 

  注意：当关机或者从起的时候，一定要先执行sync命令，防止数据丢失。

# 5、用户与用户组

### 5.1 为什么要用户

正常公司的服务器，不会给你root用户，就算给你root用户，你也不要要，权限越大风险就越大。正常情况下使用的是普通用户登入。当然可以切换用户

### 5.2 如何查看当前登入的用户

```shell
whoami
```

### 5.3 如何添加用户

```shell
useradd 选项 用户名
例如：
sudo useradd lxx
说明：成功创建后，就会自动创建于用户名同名的家目录
给用户自定家目录
sudo useradd -d 目录路径 用户名
指定用户组
sudo useradd -g 用户主名 用户名
```

### 5.4 给指定用户添加或修改密码

```shell
passwd 用户名
密码最少要8个字符
```

### 5.5 如何删除用户

```shell
userdel 用户名                 删除用户，保留家目录
userdel -r 用户名              删除用户，不保留家目录
#一般不会删除用户的家目录
```

### 5.6如何查询用户是否存在

```shell
id 用户名
如何切换用户：su - 用户名
回到原来的用户： exit
```

### 5.7 编辑用户组

```shell
1 如何添加一个组
groupadd  组名 
2 删除组
groupdel 组名
groupdel如果该组里面有用户的话，是不能删除的，除非删除这个用户
3 如何给用户切换组
usermod -g 组名 用户名
```

# 6、查看文件权限

```
查看文件权限ls -lhi /etc 最多用的是ll
结果如下：
 4261971 -rw-r--r--.  1 root root  111 Oct 31  2018 magic
 4657110 -rw-r--r--.  1 root root 2.0K Apr 11  2018 mail.rc
 4790595 -rw-r--r--.  1 root root 5.1K Aug  8  2019 makedumpfile.conf.sample
 4916208 -rw-r--r--.  1 root root 5.1K Oct 31  2018 man_db.conf
 4937598 -rw-r--r--.  1 root root  936 Aug  9  2019 mke2fs.conf
01        02          03 04   05    06      07       08

01 文件索引节点信息 inode
02 文件的类型以及文件的权限信息
03 硬链接数
04 文件所属的用户
05 文件所属的用户组
06 文件大小
07 最后一次被修改的时间
08 文件名

*******解释02***********
d    rwx    r-x    ---
1     2      3      4

上述*******解释02***********的1，表示文件的类型
d  directory 目录类型文件
-  file   普通文件
l  softlint 链接类型

上述*******解释02***********的2，表示当前用户对当前文件权限
上述*******解释02***********的3，表示当前用户组对当前文件权限
上述*******解释02***********的4，表示其他用户对当前文件的权限
总结：
文件（你的玩具） ：上述*******解释02***********的2，你自己对你的玩具有什么权限
文件（你的玩具）：上述*******解释02***********的3，你的家人对你的玩具有什么权限
文件（你的玩具）： 上述*******解释02***********的4，隔壁老王，陌生人对你的玩具有什么权限

一个文件的权限有3位组成：
rwx --->分别代表了读，写，执行这个三个权限
r -->read-->读权限  数值 4
w --->write--->写权限  数值 2
x ---> exwcute-->执行  数值 1
- --->没有权限          数值 0

rwx  r-x  r-x  请问属主什么权限  属主组有什么权限   其他用户有什么权限
7    5    5    读 写 执行           读 执行       读 执行

############
04 文件所属的用户 root -->该文件的属主是root
05 文件所属的用户组root  ---》该文件的属主组是root组
```

### 6.1 如何修改文件的权限

```shell
语法 ： chmod 参数  权限值 文件路径
chmod 777 dir1/
让文件夹以及子文件递归变成我们指定的权限，执行 ：
chomd  -R 777 /dir1
```

### 6.2 如何修改文件的属主及属主组

```shell
chown 参数 用户名.组名  文件/文件夹
让文件夹以及子文件递归变成我们指定的用户.组  执行 ：
chown  -R jj.sb a.txt
```

