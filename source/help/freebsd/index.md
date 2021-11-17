---
layout: help
title: FreeBSD 镜像使用帮助
date: 2021-11-17 22:00:15
---

## 2021-11-17日更新

## pkg 源:pkg源提供二进制安装包.

FreeBSD中pkg源分为系统级和用户级两个源.不建议直接修改/etc/pkg/FreeBSD.conf,因为该文件会随着基本系统的更新而发生改变.

创建用户级源目录:

`#mkdir -p /usr/local/etc/pkg/repos `

创建用户级源文件:

`#ee /usr/local/etc/pkg/repos/bjtu.conf`

写入以下内容:

```
bjtu: {
  url: "pkg+http://mirror.bjtu.edu.cn/reverse/freebsd-pkg/${ABI}/quarterly",
  mirror_type: "srv",
  signature_type: "none",
  fingerprints: "/usr/share/keys/pkg",
  enabled: yes
}
FreeBSD: { enabled: no }
```

若要获取滚动更新的包,请将`quarterly`修改为`latest`.请注意,`CURRENT`版本只有`latest`.

若要使用https,请先安装security/ca_root_nss,并将`http`修改为`https`,最后使用命令`#pkg update -f `刷新缓存即可.

## ports源:提供源码方式安装软件的包管理器

创建或修改文件`#ee /etc/make.conf`:

写入以下内容:

`MASTER_SITE_OVERRIDE?=http://mirror.bjtu.edu.cn/reverse/freebsd-pkg/ports-distfiles/`

## portsnap源:打包的ports文件

编辑portsnap配置文件 `#ee /etc/portsnap.conf` :

将`SERVERNAME=portsnap.FreeBSD.org` 修改为`SERVERNAME=freebsd-portsnap.mirror.bjtulug.org`

获取portsnap更新:

`#portsnap fetch extract`

## freebsd-update源:提供基本系统更新

编辑`#ee /etc/freebsd-update.conf` 文件:

将`ServerName update.FreeBSD.org` 修改为`ServerName freebsd-update.mirror.bjtulug.org`

例:从FreeBSD 11升级到12.0

`#freebsd-update -r 12.0-RELEASE upgrade`