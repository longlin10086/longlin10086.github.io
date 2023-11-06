# CommonGit | 个人用常见git命令记录


<!--more-->

本篇文章基于[阮一峰：常用Git命令清单](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)进行了适当修改。主要攫取了我日常使用过程中可能会经常使用的命令做了一个记录。

## 0 SSH连接Git服务器

首先需要我们在本地生成ssh的公钥私钥：

```
$ ssh-keygen -t rsa -C "xx@xx.com"
```

- -t 指定密钥类型，默认是 rsa
- -C 设置注释文字

接着在 `~/.ssh` 文件夹中即可找到刚才生成的公私钥，把公钥提交到GitHub网页即可。

## 1 新建代码库

```
# 在当前目录新建一个Git代码库
$ git init

# 新建一个目录并将其初始化为Git代码库
$ git init [project-name]

# 下载克隆项目到本地
$ git clone [url]
```

## 2 增加/删除文件

```
# 将文件添加到暂存区
$ git add [file]

# 删除工作区文件，并提交到暂存区
$ git rm [file]

# 停止追踪指定文件，但保留该文件留在工作区
$ git rm --cached [file]

# 将文件改名
$ git mv [file-original] [file-renamed]
```

## 3 代码提交

```
# 将代码提交至仓库区
$ git commit -m ["message"]

# 使用一次新的commit代替上次提交
$ git commit --amend -m ["message"]
```

## 4 仓库分支

```
# 列出本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有分支，包括远程和本地
$ git branch -a

# 新建一个分支，并于指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 将一个现有分支与远程分支建立追踪关系
$ git branch --set-upstream [branch] [remote-branch]

# 查看所有的跟踪分支
$ git branch -vv

# 切换到指定分支
$ git checkout [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch]

# 删除远程分支
$ git push origin --delete [branch]
$ git push :branch_name
```

## 5 远程同步

```
# 下载远程仓库的所有变动
$ git fetch [remote]

# 取回远程仓库的变化并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强制上传
$ git push [remote] --force
```

## 6 撤销

```
# 恢复暂存区文件到工作区
$ git checkout [file]

# 重置暂存区和工作区，与上一次commit保持一致
$ git reset --hard

# 重置暂存区与上次commit一致，但工作区不变
$ git reset

# 新增一个commit用于撤销指定commit
$ git revert [commit]
```

<br></br>

## 7 一些个人平时碰到使用的命令组合


### 7.1 删除已经push的远程文件/文件夹

```
# 预览暂存区中需要删除的文件或文件夹
$ git rm -r -n --cached 文件/文件夹
```
`-n` 参数执行命令时不会删除任何文件，取而代之时展示此命令要删除的文件列表预览
`-r` 参数表示递归删除

```
# 确认好之后去掉-n参数删除文件
$ git rm -r --cached 文件/文件夹

# 提交并推送
$ git commit -m "xxx"
$ git push
```

<br></br>

### 7.2 本地文件删除后同步删除远程代码仓库
```
# 清理本地缓存文件
$ git rm -r --cached .

# 提交并推送
$ git commit -m "xxx"
$ git push
```
