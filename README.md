# bash在线实验环境

## 软件简介

软件基本信息，License，所属的类别，作用，特点等。

Bash是GNU项目的Bourne Again SHell，完整实现了具有交互式命令行编辑的IEEE POSIX和Open Group shell规范，支持它的架构上的作业控制，像历史替换和扩展扩展一样的类似csh的功能，以及一个转换的其他功能。

所属类别为编程语言

特点：

1.命令补全

2.历史命令
 
3.命令别名

4.命令行编辑

5.文件名通配, globbing

6.变量

7.编程


## 软件官网

http://www.gnu.org/software/bash/

## Dockerfile 使用方法

### 笔记
有一些关于这个图像的重要事项要注意：

Bash本身安装在/usr/local/bin/bash，不是/bin/bash，所以推荐的shebang是#!/usr/bin/env bash，不#!/bin/bash（或明确地运行你的脚本bash /.../script.sh而不是让shebang自动调用Bash）。该图像不包括/bin/bash，但如果它被安装通过包含在图像中的包管理器，该软件包将安装/bin/bash并可能会引起混淆（尽管/usr/local/bin是超前/bin的$PATH，所以只要简单的bash或/usr/bin/env一致地使用，所提供的图像Bash将是首选）。

Bash是唯一包含的内容，所以如果您的脚本依赖于外部工具（jq例如），则需要手动添加（apk add --no-cache jq例如通过）。

### 交互式外壳
$ docker run -it --rm bash:4.4

bash-4.4# which bash

/usr/local/bin/bash

bash-4.4# echo $BASH_VERSION

4.4.0(1)-release

### 通过bind-mount测试脚本
$ docker run -it --rm -v /path/to/script.sh:/script.sh:ro bash:4.4 bash /script.sh
...
$ docker run -it --rm -v /path/to/script.sh:/script.sh:ro bash:3.2 bash /script.sh
...
### 通过测试脚本 Dockerfile

FROM bash:4.4

COPY script.sh /

CMD ["bash", "/script.sh"]

然后，构建并运行Docker映像：

$ docker build -t my-bash-app .
...
$ docker run -it --rm --name my-running-app my-bash-app
...

## 资源链接

- http://www.jcwcn.com/article-31939-1.html
- https://www.ibm.com/developerworks/cn/linux/shell/bash/bash-1/index.html
- http://www.oschina.net/p/bash
