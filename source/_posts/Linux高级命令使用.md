---
title: Linux高级命令使用
date: 2022-07-02 16:38:53
tags: linux
---

## ln(link, 连接文件)
- windows中的快捷方式和指向的目标是两个独立文件
- Linux中有两种连接文件：
  - 软链接（符号链接）等同于Windows里的快捷方式
  - 硬链接 增加源文件的引用计数，删除文件时，引用计数减一，当引用计数为0，源文件才会被真正删除

- 创建软链接
```bash
ln -s src link->src
```

- 创建硬链接
```bash
ln src link->src
```

- ls -l查看文件类型：
  - '-' 表示普通文件
  - 'd' 表示文件夹
  - 'l' 表示符号连接文件
  - 'p' 表示管道文件
  - 's' 表示socket文件

## man 查询手册
- 查询命令
```bash
man 1 ls
```

- 查询linux api
```bash
man 2 mkdir
```

- 查询C库函数
```bash
man 3 stoi
```

## vim 高级命令
- 快速换行(命令模式+行号)
```vim
: 1 # 快速跳转到第一行
```

- 删除连续多行
```vim
3dd # 删除从当前行开始的三行
```

- 行复制粘贴
```
3yy # 复制从当前行开始的三行
p # 粘贴到下一行
```

## rwx与权限表示
drwxr-xr-x : 10个字符， 第一个字符表示文件类型。剩下9个分成3组， 表示文件权限。
- 前三个表示此文件属主对文件的权限
- 中间三个表示此文件属主所在的组对文件的权限
- 后三个表示其他用户对文件的权限

- 'r' 代表可读4
- 'w' 代表可写2
- 'x' 代表可执行1
- '-' 代表空权限0


## find 查找文件
知道文件名，但是不知道具体路径在哪
```bash
find /etc -name "interfaces"
```

## grep 在文件中查找
想查找字符串出现在哪些文件的哪些行
```bash
grep -nr "字符串" *
```

## uname 查看系统信息
```bash
uname -a
```

## mount/umount 挂载
```bash
mount -t nfs -o nolock 192.168.1.141:/root/rootfs /mnt
umount /mnt
```

## df/du 磁盘空间相关
```bash
df -h # 显示已挂载的分区列表
du -h # 列出文件或文件夹的大小
du -h "文件名" # 以G/M表示展示文件大小
```

## 用户管理
```bash
useradd username # 添加username 用户
userdel username # 删除username 用户
passwd username # 为username设置密码
```

## 权限管理 chmod/chown/chgrp
权限的数字表示法：
- 'r'   可读    4
- 'w'   可写    2
- 'x'   可执行  1
- '-'   无权限  0

改权限的命令
```bash
chmod 755 文件名 # 改变文件权限（主权限/组权限/其他用户权限）
chmod +x  文件名 # 给文件增加可执行权限
chmod -x  文件名
```
改用户和组的命令
```bash
chown # 修改文件的用户
chgrp # 修改文件的组
```

## 网络配置
```bash
ifconfig eth0 192.168.1.13 # 设置ip地址
ifconfig eth0 up # 启动网卡
ifconfig eth0 down # 关闭网卡
ifup eth0
ifdown eth0
ifconfig eth0 192.168.1.13 netmask 255.255.255.0 # 同时设置ip和子网掩码
```


