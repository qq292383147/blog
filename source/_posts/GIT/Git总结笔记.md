---
title: Git总结笔记
date: 2019-04-02 01:34:05
tags: git
type: git
categories: git
---

<font color="#EE1289">工作流    工作区---->暂存区----->版本库</font>
<br>
<font color="#76EE00">初始化		  git init----> git add -----> git commit</font>
<br>
<font color="#00F5FF">远程仓库		git remote add---->git pull------>git push ----> git clone</font>
<br>
<font color="#EEEE00">分支管理   git branch ---->git checkout---->git merge</font>
<br>
<font color="#FFBBFF">标签管理			 git tag---->git push</font>

 

## Git 安装

下载window git

- Msysgit   https://git-scm.com/download/win

### 配置用户信息

- `git config --global user.name` “你的用户名”

- `git config --global user.email` “你的邮箱”

- `git config user.name` 查看用户名

- `git config user.password` 查看密码

- `git config user.email` 查看邮箱

- `git config --list` 查看配置信息

- `git config --global user.name "xx(新的用户名)"` 修改用户名

- `git config --global user.password "xxx(新的密码)"` 修改密码

- `git config --global user.email "xxx@xxx.com(新的邮箱)"` 修改邮箱



### 可以使用两种操作方式：

- 1、图形化界面（初级）sourcetree

- 2、命令（高级）

 

### 一：说明开发过程中的工作流程

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/1.png)

### 二：什么是shell

在计算机科学中，Shell俗称壳，用来区别于Kernel（核），是指“提供使用者使用界面”的软件（命令解析器）。它类似于[DOS](http://baike.baidu.com/view/365.htm)下的`command`和后来的`cmd.exe`。它接收用户命令，然后调用相应的应用程序

## 三：认识bash这个shell

bash常见命令

`pwd` (Print Working Directory) 查看当前目录

`cd` (Change Directory) 切换目录，如 cd /etc

`ls` (List) 查看当前目录下内容，如 ls -al

`mkdir` (Make Directory) 创建目录，如 mkdir blog

`touch` 创建文件，如 touch index.html

`cat` 查看文件全部内容，如 cat index.html

`rm` (remove) 删除文件，如 rm index.html、rm -rf  blog

`rmdir` (Remove Directory) 删除文件夹，只能删除空文件夹，不常用

`mv` (move) 移动文件或重命名，如 mv index.html ./demo/index.html

`cp` (copy) 复制文件，cp index.html ./demo/index.html

`head` 查看文件前几行，如 head -5 index.html 

`history` 查看操作历史

`who am i` 查看当前用户

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/2.png) 

## 四：vi编辑器

vi编辑器提供了3种模式，分别是命令模式、插入模式、底行模式，每种模式下用户所能进行的操作是不一样的
![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/3.png)

使用vi编辑器

​	a) 打开/创建文件， vi 文件路径

​	b) 底行模式 :w保存，:w filenme另存为

​	c) 底行模式 :q退出

​	d) 底行模式 :wq保存并退出

​	e) 底行模式 :e! 撤销更改，返回到上一次保存的状态

​	f) 底行模式 :q! 不保存强制退出

------------------------------------------------------------------------------------------------

​	h) 命令模式 ZZ（大写）保存并退出

​	i) 命令模式 u辙销操作，可多次使用

​	j) 命令模式 dd删除当前行

​	k) 命令模式 yy复制当前行

​	l) 命令模式 p 粘贴内容

​	o) 命令模式 i进入编辑模式，当前光标处插入

​	p) 命令模式 a进入编辑模式，当前光标后插入

​	q) 命令模式 A进入编辑模式，光标移动到行尾

​	r) 命令模式 o进入编辑模式，当前行下面插入新行

​	s) 命令模式 O进入编辑模式，当前行上面插入新行

当我们处在编辑模式的情况下，和我们在Windows编辑器的使用相似

 

## 五：版本控制

- 1.本地版本控制系统

- 2.集中式版本控制系统-SVN

- 3.分布式版本控制系统-git

## 六：git

- 1. git工作原理

>Git仓库目录是Git用来保存项目的元数据和对象数据库的地方。 这是Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。

工作目录是对项目的某个版本独立提取出来的内容。 这些从Git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。

暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在Git仓库目录中。有时候也被称作“索引”（Index），不过一般说法还是叫暂存区域。

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/4.png) 

基本的Git工作流程如下：

​	1、在工作目录中修改文件。

​	2、暂存文件，将文件的快照放入暂存区域。

​	3、提交更新，找到暂存区域的文件，将快照永久存储到Git仓库目录
<br>

- 2. git安装

>a) 配置用户名： git config --global user.name "用户名"
><br>
>b) 配置邮箱： git config --global user.email "邮箱地址"
><br>
>c) 查看配置信息： git config --list

- 3. 初始化仓库：

>a) 命令：git init
><br>
>b) 作用：使用Git管理项目的初始化操作，会创建一个名为.git的隐藏目录
><br>
>c) 一般是在项目的根目录执行这个命令

- 4. 跟踪文件

>a) 将文件由 工作区 添加到 暂存区（Index），暂存文件
><br>
>b) 命令：git add 文件路径
><br>
>c) git add --all 或者 git add -A（简写） 添加所有文件

- 5. 提交更新

>a) 作用：将文件由 暂存区 添加到 仓库（HEAD）
><br>
>b) git commit -m "提交说明"

- 6. 查看文件状态

>a) 命令：git status

- 7. Git工作流程

>a) 在工作目录中修改某些文件。
><br>
>b) 对修改后的文件进行快照，然后保存到暂存区域。
><br>
>c) 提交更新，将保存在暂存区域的文件快照永久转储到.git目录中。

- 8. 查看提交日志

>a) 命令：git log 查看详细的提交信息

- 9. 版本回退

>a) 作用：恢复到已经提交的某一个版本中
><br>
>b) 命令：git reset --hard [版本号]
><br>
>c) 其他方式：git reset --hard head~1

- 10. git分支

>a) 查看分支：git branch，当前分支会标有一个*
><br>
>b) 创建分支：git branch [分支名称]
><br>
>c) 切换分支：git checkout [分支名称]
><br>
>d) 合并分支：git merge [分支名称]，即：将其他分支合并到当前分支
><br>
>e) 删除分支：git branch -d [分支名称]

- 11. 创建本地共享仓库:仓库就是一个文件夹

>a) ![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/5.png)
><br>
>b) 通过—bare创建裸仓库
><br>
>c) 共享的仓库必须是一个裸仓库
><br>
>d) 通过从共享仓库中复制内容
><br>
>e) 虽然复制的时候是从裸仓库中复制的，但是复制到的内容是真正的工作目录下的内容![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/6.png)
><br>
>f) 修改内容，并且将修改的内容更新![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/7.png)
><br>
>g) 进入到另外的目录，将之前提交的内容拉取![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/8.png)

- 12. git远程仓库

### 1 在本地创建仓库

`git init`

`git config`

2 新建 README.md 文件，并输入任意内容

3 将 README.md 提交到本地

`git add`

`git commit`

4 在github中新建仓库，并拿到仓库地址

5 使用命令 `git push [仓库地址] master` 提交内容到github的默认分支

6 刷新github仓库页面，在线修改 README.md 文件，并提交

7 使用命令 `git pull [仓库地址] master` 获取仓库中的最新内容

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/9.png) 

### 文件对比


- 命令：git diff：将工作区与暂存区或者仓库对比

- 说明：如果暂存区没有文件，就会将工作区代码与上一次提交对比

  - 1 工作区 与 暂存区对比

  - 2 工作区 与 仓库  对比

- 命令：git diff --cached：将当前暂存区与仓库对比

- 命令：git diff [版本号1] [版本号2] [对比的文件路径]

  - 对比仓库区两次提交的差异

 

### 撤销和删除

- git reset HEAD 文件名 从暂存区撤销（结果：变为 未 add 状态）

- git checkout -- test.txt 撤销文件变化

  - 一种是 readme.txt 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

  - 一种是 readme.txt 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

- `rm [文件名称]`：删除文件（物理删除）

- `git rm [文件名称]`：从仓库中删除文件

- `git rm --cached [文件名称]`：从暂存区删除文件

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/10.png) 

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/11.png) 

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/12.png) 



设置默认地址的几种方法：

`git push` [远程终端的地址] 默认节点

改：

1、`git push` 变量名 -u

2、`git push` 地址名 -u 

下次就可以直接`git push`

 

清除安装的缓存

![img](http://zhanglong292383147.gitee.io/picture_images/picture/git/13.png) 