## Git Intro

[官方手册](https://git-scm.com/book/zh/v1/) https://git-scm.com/book/zh/v1/


### 什么是git？

> 一个代码管理工具
> 我们把用代码以及git管理程序产生的附加文件称为一个版本库(repository)

### 有什么特点

> 如word等工具，文件编辑后不能保存历史。git用于**编辑历史**的管理记录
> git是围绕代码编辑历史和多人同时编写代码的管理工具

### 预备知识需求

1. 代码管理
2. 软件版本
3. 本机/服务器 (git将其称之远端)
4. bash的几条基本命令

## 安装

```
$sudo apt-get install git          # ubuntu, windows请下载git安装程序，并代开git-bash完成如下命令
$git config --global user.email "you@example.com"   # 自己的邮箱
$git config --global user.name "Your Name"          # 自己喜欢的用户名
```

## git用于本地代码历史管理

1. 创建版本库

```
$cd path/to/repository
$git init       # 设定这个目录为git版本库，git会生成一个.git隐藏文件夹
```

2. 添加跟踪文件，提交一次修改
```
$git add -A     # 将目录下的所有文件添加到git的管理功能，-A是all的意思，还可以指定文件，这样只需要跟踪管理指定文件
$git commit -m 'init or some comment' # 将修改提交成为一次历史，git会产生一次记录，记录时间，修改内容等
```

> 上述命令即完成了本地的代码的一次提交，提交一次将产生一次历史，所有的历史记录和更改内容被记录在 .git目录下面
> 本地代码管理一般用到上述命令

即：

1. 创建版本库 `git init` (这条命令只需要执行一次) ->  
2. 添加跟踪文件  `git add filename.ext`  -> 提交一次形成记录 `git commit -m '说明文字'`  

## Git和远端 remote (如：github.com)的交互

1. 获取别人的代码

```
$git clone https://github.com/tair-ai/tutorials.git  # 如获取TAIR.AI的tutorial，把url换成其url即获取其他版本库
$ls tutorials   # 可以查看到获取的代码版本库
```

2. 将自己的代码推到远端，如github.com
```
前提条件： 
# 1. 首先，需要在远端服务器上新建一个版本库，如github.com添加一个新的repository
# 2. 然后获取到版本库的http格式的git地址，形如 https://github.com/tair-ai/test_git.git，注意要新建的
# 3. 本地有一个git管理的仓库，并至少完成了一次记录提交，即执行过如:`git init`, `git add -A`, `git commit -m 'xxx'`

$cd /path/to/repos
$git remote add origin https://github.com/tair-ai/test_git.git   # origin为别名，可以随意命名；http换成自己对应的远端地址即可
$git push origin master    # 将代码推送到远端，完成当前所有提交记录的推送；http格式地址需要输入用户名和密码
$git pull origin master    # 获取远端的更新
```

##  单人项目最常用的命令即：

```
# 本地
$git init
$git add <filename>.<ext>
$git commit -m 'message'

# 远端
$git push origin master
$git pull origin master 
```

## Git 其他操作请查阅官方文档

