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

克隆命令 `git clone <url>`

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

```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git.md

nothing added to commit but untracked files present (use "git add" to track)
```

```
$ git status -s
?? git.md
```

##### 将文件放入暂存区：

命令 `git add  filename` 将为跟踪的文件加入暂存区

```
$ git add git.md
$ git status -s
A  git.md
```

##### 取消暂存区文件暂存：

命令 `git reset filename`取消暂存

##### 提交暂存区文件到本地仓库：

命令 `git commit -m "message" <filename>`

```
$ git commit -m "add git.md"
[master (root-commit) d18ef13] add git.md
 1 file changed, 76 insertions(+)
 create mode 100644 git.md
```

直接将修改的文件提交到本地仓库：`"git commit -a"`

```
$ git commit -a -m "update git.md"
[master d91603c] update git.md
 1 file changed, 122 insertions(+), 1 deletion(-)
```

##### 删除文件：

命令 `git rm filename`删除文件(是删除工作区的文件)

直接使用 `git commit -m "message"` 就可以提交

##### 将文件添加至忽略列表：

在工作区中创建一个.gitignore文件，列出要忽略的文件模式。

`*.a   #忽略所有以.a结尾的文件`

`！lib.a        !表示取反 即lib.a不需要忽略`

`/TODO          表示忽略名叫TODO的文件`

`build/         表示忽略build目录下的文件`

`doc/*.txt      表示忽略doc目录下所有的.txt文件`

`doc/**/*.pdf   表示doc目录及其子目录下的.txt文件都忽略`

##### 查看日志记录：

通过 `git log`命令



#### 6.远程仓库操作

##### 查看远程仓库：

运行 `git remote`，会列出每一个远程服务器的简写。已经克隆的仓库至少应该看到origin。

```
$ git remote
origin
```

```
$ git remote -v
origin  https://github.com/Leyusf/git_study.git (fetch)
origin  https://github.com/Leyusf/git_study.git (push)
```

##### 添加远程仓库：

运行`git remote add <shortname> <url>`添加一个新的远程git仓库，同时指定一个简写。

 一个仓库可以添加多个远程仓库。

##### 远程仓库克隆：

使用`git clone <url>`命令。 将该git远程仓库几乎所有的数据都克隆（日志信息，历史记录）。

拉取每一个文件的每一个版本。

```
$ git clone https://github.com/Leyusf/JavaGuide.git
Cloning into 'JavaGuide'...
remote: Enumerating objects: 12970, done.
remote: Total 12970 (delta 0), reused 0 (delta 0), pack-reused 12970
Receiving objects: 100% (12970/12970), 51.84 MiB | 1.58 MiB/s, done.
Resolving deltas: 100% (8414/8414), done.
```

##### 移除无效的远程仓库：

可以使用`git remote rm <shortname>` 移除远程仓库。

**注意**：此命令只从本地移除远程仓库记录，并不会真正影响到远程仓库。

```
$ git remote
my
origin
$ git remote rm my
$ git remote
origin
```

##### 从远程仓库中抓取与拉取：

`git fetch <shortname> <branch>`  或 `git fetch` 从远程仓库获取最新版本到本地仓库，不自动merge。

```
$ git fetch
remote: Enumerating objects: 12970, done.
remote: Total 12970 (delta 0), reused 0 (delta 0), pack-reused 12970
Receiving objects: 100% (12970/12970), 51.84 MiB | 3.29 MiB/s, done.
Resolving deltas: 100% (8414/8414), done.
From https://github.com/Leyusf/JavaGuide
 * [new branch]      master     -> origin/master
```

使用`git merge origin/master` 将抓取的文件合并到工作区。

`git pull <shortname> <branch>`从远程仓库获取最新数据并merge到本地仓库。

```
$ git pull origin master
remote: Enumerating objects: 7898, done.
remote: Counting objects: 100% (7898/7898), done.
remote: Compressing objects: 100% (3004/3004), done.
remote: Total 7898 (delta 4508), reused 7886 (delta 4500), pack-reused 0
Receiving objects: 100% (7898/7898), 5.32 MiB | 719.00 KiB/s, done.
Resolving deltas: 100% (4508/4508), done.
From https://gitee.com/red_coated_leaves/linux-lab
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
```

**注意**：仓库中存在文件时会报错(fatal: refusing to merge unrelated histories)。

使用参数 `--allow-unrelated-histories`可以强制合并。

```
$ git pull origin master --allow-unrelated-histories
From https://gitee.com/red_coated_leaves/linux-lab
 * branch            master     -> FETCH_HEAD
Merge made by the 'recursive' strategy.
 .gdb/.gitignore                                    |     1 +
 .gdb/kernel.default                                |    31 +
 .gdb/uboot.default                                 |    18 +
 .gitignore                                         |    18 +
 .gitmodules                                        |    80 +
 .labinit      
```

##### 推送到远程仓库:

使用`git push <shortname> <branch>`将代码推送至远程仓库。

```
$ git push origin master
Logon failed, use ctrl+c to cancel basic credential prompt.
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 12 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (13/13), 2.42 KiB | 1.21 MiB/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/Leyusf/git_study.git
 * [new branch]      master -> master
```



#### 7.git分支:

master是默认分支与其他分支并无区别。

##### 查看分支：

列出所有本地分支：

`git branch`

```
$ git branch
* master
```

列出所有远程分支：

`git branch -r`

```
$ git branch -r
  origin/master
```

列出所有本地分支和远程分支：

`git branch -a`

```
$ git branch -a
* master
  remotes/origin/master
```

##### 创建分支：

创建本地分支：

`git branch <branchname>`

`git branch b1`

`git branch b2`

```
$ git branch
  b1
  b2
* master
```

##### 切换分支：

`git checkout <branchname>`

`git checkout b1`

```
$ git branch
* b1
  b2
  master
```

##### 推送至远程仓库分支：

`git push origin <branchname>`

`git push origin b1`

```
$ git push origin b1
Logon failed, use ctrl+c to cancel basic credential prompt.
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'b1' on GitHub by visiting:
remote:      https://github.com/Leyusf/git_study/pull/new/b1
remote:
To https://github.com/Leyusf/git_study.git
 * [new branch]      b1 -> b1
```

##### 合并分支：

在要合并到的分支下使用命令

`git merge <branchname>`

```
zly@LAPTOP-QOH779PM MINGW64 /e/study/gitStudy/git_study (master)
$ git merge b1
Updating 1b1faf5..6545dc7
Fast-forward
 b1.txt | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 b1.txt
```

有时，在两个不同的分支中对同一个文件的同一个部分进行了不同的修改，就会产生冲突。

此时需要我们打开冲突文件并修复冲突内容，最后执行`git add`命令来标示冲突已经解决。

```
$ git merge b1
Auto-merging b1.txt
CONFLICT (content): Merge conflict in b1.txt
Automatic merge failed; fix conflicts and then commit the result.
```

手动处理冲突内容。

```
zly@LAPTOP-QOH779PM MINGW64 /e/study/gitStudy/git_study (master|MERGING)
$ git add b1.txt

zly@LAPTOP-QOH779PM MINGW64 /e/study/gitStudy/git_study (master|MERGING)
$ git commit -m "fix conflict"
[master c3ae8d5] fix conflict
```

##### 删除本地分支：

`git branch -d <branchname>`

```
$ git branch -d b2
Deleted branch b2 (was 1b1faf5).
```

如果要删除的分支中进行了一些开发，此时执行上面的删除命令并不会删除分支，如果要坚持删除分支，可以使用 `git branch -D <branchname>`

修改b1分支中的文件。

```
$ git branch -d b1
error: The branch 'b1' is not fully merged.
If you are sure you want to delete it, run 'git branch -D b1'.
```

强制删除。

```
$ git branch -D b1
Deleted branch b1 (was 68f3625).
```

##### 删除远程分支：

`git push origin -d <branchname>`删除远程分支。

```
$ git push origin -d b2
Logon failed, use ctrl+c to cancel basic credential prompt.
To https://github.com/Leyusf/git_study.git
 - [deleted]         b2
```



#### git标签：

给某一版本打上标签，可以方便的切换标记时的状态。

##### 创建新标签：

使用`git tag <tagname>`创建标签

`git tag v0.1`

##### 列出已有标签：

使用命令`git tag`

```
$ git tag
v0.1
```

也可以使用`git show <tagname>`查看标签信息。

```
$ git show v0.1
commit c3ae8d5960bd297e14c4c44a785fe52b8ce2991b (HEAD -> master, tag: v1.0, tag: v0.1, origin/master)
Merge: ed9a6b4 c43839e
Author: Leyusf <53003567+Leyusf@users.noreply.github.com>
Date:   Sat Apr 17 21:04:43 2021 +0800

    fix conflict

diff --cc b1.txt
index 64d3029,4ca1394..48b6ead
--- a/b1.txt
+++ b/b1.txt
@@@ -1,3 -1,3 +1,4 @@@
  public class user;
  // 在b1分支中创建文件
- //已经被master修改了
 -//在b1中进行修改
++//已经被master修改了
++//在b1中进行修改
```

##### 将标签推送至远程仓库：

使用`git push origin <tagname>`将标签推送至远程仓库。

```
$ git push origin v0.1
Logon failed, use ctrl+c to cancel basic credential prompt.
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/Leyusf/git_study.git
 * [new tag]         v0.1 -> v0.1
```

##### 检出标签：

一般来说，新建一个分支，指向检出的标签。

使用命令`git chekout -b <branchname> <tagname>`

```
$ git checkout -b b3 v1.0
Switched to a new branch 'b3'
```

##### 删除标签：

1.删除本地标签：

`git tag -d <tagname>`

```
$ git tag -d v0.1
Deleted tag 'v0.1' (was c3ae8d5)
```

2.删除远程标签：

`git push origin :refs/tags/<tagname>`

```
$ git push origin :refs/tags/v0.1
Logon failed, use ctrl+c to cancel basic credential prompt.
To https://github.com/Leyusf/git_study.git
 - [deleted]         v0.1
```

