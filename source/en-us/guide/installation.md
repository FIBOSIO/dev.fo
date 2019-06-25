---
title: Installation
type: tutorials
language: en
order: 2
---

## Quick Installation

FIBOS supports the common UNIX operating systems such as Mac OSX, Linux and FreeBSD.

#### It is recommended to perform quick installation on the terminal by directly adopting the following commands:

**Stable Version**

```
curl -s https://fibos.io/download/installer.sh | sh
```

**beta Version**

```
curl -s https://fibos.io/download/installer_beta.sh | sh
```

After the installation, the FIBOS executable file is in the system directory of `bin` , which can be used to view the FIBOS version:

```
~$ which fibos
/usr/local/bin/fibos

~$ fibos --version
v0.27.0-dev
```

## Common Commands

Directly press Enter on FIBOS to query version information as follows:

```
~$ fibos
Welcome to fibjs 0.26.0-dev.
Type '.help' for more information.
> console.log('hello,FIBOS!')
hello,FIBOS!
> .info
```

Create a folder called `hello_fibos` so as to generate the configuration initialization of the file `package.json`.  

```
$ cd  hello_fibos
$ fibos --init or npm init
```

Installation package

```
$ fibos --install fibos.js or npm install fibos.js
```

## Upgrade

Re-executing the installation command will automatically overwrite the original `fibos` executable file, then restart the `fibos` service to complete the upgrade level.

## Uninstall

Simply delete the `fibos` executable file under `/usr/local/bin/`.

```javascript
  $ sudo rm /usr/local/bin/fibos
```


👉 【[Quick Start](./start.html)】