

# **获取Git仓库**

- git init : 初始本地Git仓库
- git clone : 获取git远程仓库

# **修改和提交**

- 检测文件的状态
  - git status
- 查看文件的变更内容
  - git diff
- 文件添加到暂存区
  - git add .
    - . : 点代表全部文件
    - 也可以输入路径指定单独文件
- 删除文件
  - git rm
  - 停止跟踪文件但不删除
  - git rm --cached
- 文件更新提交
  - git commit
    - -a  : 自动执行 git add .
    - -m : 添加注释
  - 修改最后一次提交
  - git commit --amend

# **查看提交历史**

- 查看提交的历史
  - git log
- 查看提交的历史 (简洁)
  - git log --pretty=oneline
- 查看提交的历史的图结构
  - git log --pretty=oneline --graph
- 记录着版本回退 和 提交的历史
  - git reflog

# **撤销**

- 版本回退 
  - git reset
  - git reset --hard HEAD^
    - 上一个版本
  - git reset --hard HEAD~1000 
    - 指定版本排序
  - git reset --hard 2d44982
    - 指定某一个commit id (校验和)
- 撤销指定的没提交文件的修改内容
  - git checkout HEAD <file>
- 撤销指定的提交
  - git revert <commit>

# **分支**

- 显示所有本地分支
  - git branch
- 切换到指定**分支或标签**
  - git checkout <branch/tag>
- 创建新分支
  - git branch <new-branch>
- 删除本地分支
  - git branch -d <branch>
- 删除远程分支
  - git push origin --delete <branch>
- 创建分支并进入
  - git checkout --track origin/main

# **标签**

- 列出所有本地标签
  - git tag
- 基于最新提交创建标签
  - git tag <tagname>
    - tagname : 设置的标签名称
- 删除标签
  - git tag -d <tagname>

# 合并

- 合并指定分支到当前分支
  - git merge <branch>
- 衍生合并指定分支到当前分支
  - git rebase <branch>
- 合并远程分支
  - git merge <remote>/<branch>

# 远程操作

- 查看远程版本库信息
  - git remote -v
    - git remote
    - git remote –v 
      - 详细信息
      - -v是—verbose的缩写(冗长的)
- 查看指定远程版本库信息
  - git remote show <remote>
- 添加远程版本库
  - git remote add <remote> <url>
    - url :  “远程版本库的地址链接”
    - remote : 起的名称
- 从远程仓库获取代码
  - git fetch <remote>
    - 在使用 git merge 将获取到的远程仓库的代码合并到本地仓库中
    - 这两步操作可以使用git pull 直接完成
- 下载远程仓库代码并且快速合并
  - git pull
- 上传本地仓库代码并且快速合并
  - git push
  - git push <remote><branch>
    - remote : 远程仓库的名称
    - branch : 指定的远程仓库的分支
- 删除远程分支或标签
  - git push <remote> -delete <brancch / tag-name>
- 给远程分支上传所有标签
  - git push --tags



# 配置信息

- git config --global user.name
  - 配置用户名
- git config --global user.email
  - 配置邮箱

- 检测当前的配置信息
  - git config --list
  
- 设置push默认行为

  - git config push.default  simple 
  - simple :系统默认设置的行为
    - 找到当前分支的远程仓库
      - 并找到远程仓库中相同名称的分支
    - 找远程仓库的相同名称的分支
      - 如果找不到会报错
  - upstream
    - 设置找上游分支
  - current
    - 找远程仓库的相同名称的分支
      - 如果找不到
      - 就会再远程仓库给我新建一个分支

  

# git忽略文件

- 以创建一个名为 .gitignore 的文件



# 常见的问题处理

- 设置本地分支的上游分支

  - git fetch

  - git branch --set-upstream-to=origin/main

- 合并远程和本地仓库时没有共同base

  - 强制合并
  - git merge --allow-unrelated-histories



# 从本地仓库连接远程仓库

```shell
# 初始化本地仓库
git init

# 添加远程仓库
git remote add origin xxxx


# 从远程仓库获取内容
git fetch
git branch --set-upstream-to=origin/main
git merge --allow-unrelated-histories

# git push
git config push.default upstream

# 换一种做法
git checkout main
```



# git tag

- ```shell
  git tag v1.0.0
  
  git tag
  
  git tag -d v1.0.0
  
  # 将本地tag push远程仓库
  git push origin v1.0.0
  git push origin --tags
  
  # 删除远程的tag
  git push origin -d v1.0.0
  ```



# git的原理(git如何保存内容)

```shell
git add .
# .git/objects/00 40

git commit -m "aaa"
# .git/object/eb -> 提交信息/作者/tree
# .git/object/aa
# aaa.js -> 00
# bbb.js -> 40
```



# 分支结构

## 本地分支

创建分支

- ```shell
  git branch testing
  git checkout testing
  # 合并
  git checkout -b testing
  ```

合并分支

- ```shell
  git merge testing
  git add .
  git commit -m ""
  ```

查看所有分支

- ```shell
  git branch
  
  # 删除本地分支
  git branch -d testing
  ```

## 远程分支

- ```shell
  # 初始化本地仓库
  git init
  
  # 添加远程仓库
  git remote add origin xxxx
  
  
  # 从远程仓库获取内容
  git fetch
  git branch --set-upstream-to=origin/main
  git merge --allow-unrelated-histories
  
  # git push
  git config push.default upstream
  
  # 换一种做法
  git checkout main
  ```



推送一个远程分支

- ```shell
  git push origin develop
  
  # 李四操作
  git checkout develop
  ```



删除远程分支

- ```shell
  git push origin -d develop
  ```



# git flow工作流

第一图:

* master: 记录主要的版本
* develop: 开发版本
* topic: 新主题



第二图:

* master: 记录主要的版本
  * tag
* hotfix: 热修复
  * merge master
  * merge develop
* develop: 开发分支
* release: 上线的分支
  * merge master
  * merge develop
* feature: 新特性

### git rebase

* 改变某一个分支base, 目的让log的历史记录更加的简洁
* 黄金原则: 不要在主分支中使用rebase



# Git中常见的命令总结

## 基础的命令

```shell
git clone xxxxxxxx

git add .
git commit -m "xxxx"

git pull ->(git fetch + git merge)
git push
```



## 进阶的命令

```shell
git checkout develop
# 1.检查服务器是否有origin/develop这个分支
# 2.创建一个本地的develop分支
# 3.让本地的develop分支自动跟踪origin/develop
# 4.切换到develop分支
```



## 高级的命令

```shell
git tag

git checkout -b develop
git push origin develop

git merge develop
git rebase
```

