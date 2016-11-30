
# [shell] lost+found目录的作用

------------------------------------------
## 问题描述

平时使用Linux服务器安装应用时，偶尔会看到当前目录下有一个`lost+found`目录。
之前也没太注意，最近考虑这个目录是不是可以删除掉呢？看起来比较碍眼啊~

要确认能不能删除此目录，先了解下它是做什么的吧。

### lost+found目录说明

以下内容引自《鸟哥的Linux菜鸟私房菜》:
> 这个目录是使用标准的ext2/ext3档案系统格式才会产生的一个目录，目的在于当
> 档案系统发生错误时，将一些遗失的片段放置到这个目录下。这个目录通常会在
> 分割槽的最顶层存在， 例如你加装一颗硬盘于/disk中，那在这个系统下就会自
> 动产生一个这样的目录『/disk/lost+found』。
> 当你使用 fsck 检查文件系统后，若出现问题时，有问题的数据会被放置到这个
> 目录中喔！ 所以理论上这个目录不应该会有任何数据，若系统自动产生数据在
> 里面，那你就得特别注意你的文件系统啰！ 

由上述内容可知，最好还是不要删除此目录，避免进行磁盘恢复时出问题。

------------------------------------------
## 其他信息：`mklost+found`命令

如果实在是不小心把`lost+found`目录删除了，那么不能够直接通过mkdir来新建个
同名目录了事。必须通过`mklost+found`命令来创建。

因为`mklost+found`命令在创建`lost+found`目录时，还会给该目录预分配磁盘数
据块，以减轻 e2fsck 命令的负担。

如下，是此命令的man手册，供参考：

```shell
                           MKLOST+FOUND(8)

NAME
    mklost+found  - create a lost+found directory on a mounted Linux second
extended file system

SYNOPSIS
    mklost+found

DESCRIPTION
    mklost+found is used to create a lost+found directory  in  the  current
working  directory  on  a  Linux second extended file system.  There is
normally a lost+found directory in the root directory of each  filesys-
tem.

    mklost+found  pre-allocates  disk blocks to the lost+found directory so
that when e2fsck(8) is being run to recover a filesystem, it  does  not
need  to  allocate  blocks in the filesystem to store a large number of
unlinked files.  This ensures that e2fsck will  not  have  to  allocate
data blocks in the filesystem during recovery.
```
