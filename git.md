### git学习



#### 1. 查看git信息：

查看git信息   `git config --list`

查看指定的git信息 `git config user.name`



#### 2.设置git信息：

设置用户信息 `git config --global user.name "username"`

设置用户邮箱 `git config --global user.email "123@163.com"`



#### 3.获取git仓库：

##### 1.方法一：

在本地初始化一个git仓库。

在本地文件夹目录下打开 git bash

初始化仓库： `git init`

```
$ git init
Initialized empty Git repository in E:/study/gitStudy/repo1/.git/
```

##### 2.方法二：

从远程仓库克隆 。

克隆命令 `git clone 网络地址`

```
$ git clone https://github.com/Leyusf/git_study.git
Cloning into 'git_study'...
warning: You appear to have cloned an empty repository.
```



#### 4. git相关概念：

**版本库：**.git 文件夹就是版本库，其中储存了很多配置信息、日志信息和文件版本信息等

**工作目录(工作区)：**包含.git文件夹的目录就是工作目录，主要用于存放代码。

**暂存区：**.git文件夹中有很多文件，其中一个index文件就是暂存区，也可以叫做stage。是保存临时文件修改的地方。

**文件状态：**

**1.untracked 未跟踪(未被纳入版本控制)**

**2.tracked 已跟踪(被纳入版本控制)：**

​	unmodified 未修改状态

​	modified 已修改状态

​	staged 已暂存状态



#### 5.本地仓库操作

##### 查看文件状态：

命令 `git sttus` 或 `git status -s`