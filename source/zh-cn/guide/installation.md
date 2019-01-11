---
title: 安装
type: tutorials
language: zh-cn
order: 2
---

## 快速安装

FIBOS 支持常用的 UNIX 操作系统，比如 Mac OSX，Linux 和 FreeBSD。

#### 建议在终端直接使用下面的命令快速安装：

**稳定版**

```
curl -s https://fibos.io/download/installer.sh | sh
```

**beta 版**

```
curl -s https://fibos.io/download/installer_beta.sh | sh
```

安装结束后 FIBOS 可执行文件在系统 `bin` 目录下，使用查看 FIBOS 版本：

```
~$ which fibos
/usr/local/bin/fibos

~$ fibos --version
v0.27.0-dev
```

## 常用命令

直接执行 FIBOS 回车，查询版本信息，如：

```
~$ fibos
Welcome to fibjs 0.26.0-dev.
Type '.help' for more information.
> console.log('hello,FIBOS!')
hello,FIBOS!
> .info
```

创建 `hello_fibos` 文件夹 ，生成 `package.json`  文件配置初始化：

```
$ cd  hello_fibos
$ fibos --init 或者 npm init
```

安装包

```
$ fibos --install fibos.js 或者 npm install fibos.js
```

## 升级

重新执行安装命令会自动覆盖原有的 `fibos` 可执行文件，然后重启一下 `fibos` 服务即可完成升级。

## 卸载

直接删除 `/usr/local/bin/` 下的 `fibos` 这个可执行文件即可。

```
$ sudo rm /usr/local/bin/fibos
```


👉 【[快速入门](./start.html)】