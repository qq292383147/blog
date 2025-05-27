---
title: git 解决冲突
date: 2021-03-18 21:44:57
tags: git
type: git
categories: git
---


### 三、解决冲突


#### 1、使用git pull文件时和本地文件冲突

场景：在使用 `git pull` 代码时，经常会碰到有冲突的情况
简要：主要是使用 `git stash` 命令分成以下几个步骤进行处理


```json
git stash
```

先将本地修改存储起来

```bash
git stash list
```

可以看到保存的信息， stash@{0}就是刚才保存的标记

```bash
git pull
```

获取内容

```bash
git stash pop stash@{0}
```

还原暂存的内容

系统提示如下类似的信息，系统自动合并修改的内容，但是其中有冲突，需要解决其中的冲突

Auto-merging c/environ.c CONFLICT (content): Merge conflict in c/environ.c

解决文件中冲突的的部分

这里写图片描述

```json
  <<<<<<< Updated upstream 和=====之间的内容就是pull下来的内容，
  ====和stashed changes之间的内容就是本地修改的内容。自行确定需要的内容。解决完成之后，就可以正常的提交了。
```

7.最后一步清空 `stash`

```bash
git stash clear
```