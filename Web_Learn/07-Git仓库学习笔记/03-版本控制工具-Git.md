# Git标签-trg标签

-  对于重大的版本我们常常会打上一个标签，以表示它的重要性

  - Git 可以给仓库历史中的某一个提交打上标签
  - 比较有代表性的是人们会使用这个功能来标记发布结点（ v1.0 、 v2.0 等等）

- 创建标签

  - Git 支持两种标签

    - 轻量标签（lightweight）

    - 附注标签（annotated）

      - 附注标签：通过-a选项，并且通过-m添加额外信息

      - ```git
        git tag -a v1.0.0 -m "附注标签"
        ```

      - 使用git show v1.0.0 查看附注标签的具体信息

- 默认情况下, git push 命令并不会将

  - 在本地仓库定义的标签传送到远程仓库服务器上

- 在本地创建完标签后

  - 必须显式地将标签推送到共享服务器上

    - 当其他人从仓库中克隆或拉取
    - 也可以得到你的那些标签

  - ```git
    //推送指定的
    git push origin v1.0.0
    ```

  - ```js
    //推送全部定义的标签
    git push origin --tags
    origin :定义的远程仓库的名称
    ```

## tag删除和检出tag

- 删除本地tag

  - 要删除掉你本地仓库上的标签，可以使用命令 git tag -d <tagname>

  - ```git
    git tag -d v1.0.0
    ```

- 删除远程tag

  - 要删除远程的tag 我们可以通过 git push <remote> –delete <tagname>

  - ```js
    git push origin -d v1.0.0
    ```

- 检出tag

  - 就是想回到初遇这个标签的版本

  - 如果你想查看某个标签所指向的文件版本

    - 可以使用 git checkout 命令

  - 通常我们在检出tag的时候还会创建一个对应的分支

  - ```git
    git checkout v1.0.0
    ```

# Git提交对象

## 暂缓区的本质

- git add . 添加到本地仓库的objects中
  - 使用git cat-file 查看
  - git cat-file -t ***
    - 查看状态
  - git cat-file -p ***
    - 查看具体信息
  - ![image-20231130174356078](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231130174356078.png)
  - fd9f
  - ![image-20231130174505278](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231130174505278.png)
  - cat-file 默认从objects中查找

## 提交文件的本质

![image-20231130175054379](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231130175054379.png)

- 一个tree的文件夹引用这暂缓区中的代码
- 提交的文件夹在引用tree的文件夹

## 分支提交的对象

- 几乎所有的版本控制系统都以某种形式支持分支
  - 使用分支意味着你可以把你的**工作从开发主线上分离开**来
    - 以免影响开发主线
- 在进行提交操作时
  - Git 会保存一个提交对象

**提交对象**

- 该提交对象会包含一个指向**暂存内容快照的指针**
- 该提交对象还包含了作者的姓名和邮箱
  - 提交时输入的信息以及指向它的父对象的指针
    - 首次**提交产生的提交对象没有父对象**
    - **普通提交操作产生的提交对象有一个父对象**
      - 而由多个分支合并产生的提交对象有多个父对象
- ![image-20231130184614786](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231130184614786.png)



# Git master分支

-  Git 的分支，其实本质上仅仅是**指向提交对象的可变指针**
  - Git 的默认分支名字是 master，在多次提交操作之后
    - 已经有一个**指向最后那个提交对象**的 master 分支
    - master 分支会在每次提交时自动移动
- Git 的 master 分支并不是一个特殊分支
  - 它就跟其它分支完全没有区别
  - 之所以几乎每一个仓库都有 master 分支
  - 是因为 git init 命令默认创建它，并且大多数人都懒得去改动它
- ![image-20231130184904567](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231130184904567.png)



# Git 创建本地分支

- Git是怎么创建新分支的呢？
  - 很简单，它只是为你创建了一个可以移动的新的指针

- 创建一个 testing 分支
  - 需要使用 git branch 命令

  - git branch testing

- Git又是怎么知道当前在哪一个分支上呢
  - 它也是通过一个名为 HEAD 的特殊指针

  - 使用git checkout testing可以切换分支


- 创建新分支的同时切换过去
  - 常我们会在创建一个新分支后立即切换过去
  - git checkout -b testing

# 为什么需要使用分支

- 简单的分支新建与分支合并的例子
  - 开发某个项目，在默认分支master上进行开发
  - 实现项目的功能需求，不断提交
  - 并且在一个大的版本完成时，发布版本，打上一个tag v1.0.0
- 继续开发后续的新功能
  - 正在此时，你突然接到一个电话说有个很严重的问题需要紧急修补
    -  你将按照如下方式来处理
  - 切换到tag v1.0.0的版本，并且创建一个分支hotfix
- 想要新建一个分支并同时切换到那个分支上
  - git checkout –b hotfix

# 分支开发和合并

- 分支上开发、修复bug
  - 我们可以在创建的hotfix分支上继续开发工作或者修复bug
  - 当完成要做的工作后，重新打上一个新的tag v1.0.1
- 切换回master分支
  - 但是这个时候master分支也需要修复刚刚的bug
- 所以我们需要将master分支和hotfix分支进行合并
- 切换到master分支
  - git checkout master
- 将hotfix分支合并到master分支
  - git merge hotfix

# 查看和删除分支

- 如果我们希望查看当前所有的分支
  - 可以通过以下命令
- 查看当前所有的分支
  - git branch
- 查看最后一次提交
  - git branch –v
- 查看所有合并到当前分支的分支
  - git branch --merged
- 查看所有没有合并到当前分支的分支
  - git branch --no-merged
- 如果某些已经合并的分支我们不再需要了，那么可以将其移除掉
  - 删除当前分支
    - git branch –d hotfix
  - 强制删除某一个分支
    - git branch –D hotfix



# Git的工作流

- 由于 Git上 的分支的使用便捷性
  - 产生了很多Git的工作流
- 也就是说, 在整个项目开发周期的不同阶段
  - 可以同时拥有多个开放的分支
  - 可以定期地把某些主题分支合并入其他分支中

以下工作流

- master作为主分支
- develop作为开发分支
  - 并且有稳定版本时
    - 可以合并到master分支中
- topic作为某一个主题或者功能或者特性的分支进行开发
  - 开发完成后合并到develop分支中
- ![image-20231201101820816](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201101820816.png)



![image-20231201102442200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201102442200.png)



# Git的远程分支

- 远程分支是也是一种分支结构
  - 以 <remote>/<branch> 的形式命名的
    - remote : 远程
    - branch : 分支
- 需要通过fetch来获取最新的远程分支提交信息

# 远程分支的管理

- **操作一：推送本地分支到远程**
  -  想要公开分享一个分支时
    - 需要将其推送到有写入权限的远程仓库上
  - 运行 git push <remote> <branch>
- **操作二：跟踪远程分支**
  - 当克隆一个仓库时
    - 它通常会自动地创建一个跟踪 origin/master 的 master 分支
    - 也可以设置其他的跟踪分支
      - 可以通过运行 git checkout --track <remote>/<branch
- **操作三：删除远程分支**
  - 如果某一个远程分支不再使用，我们想要删除掉
    - 可以运行带有 --delete 选项的 git push 命令来删除一个远程分支
  - git push origin --delete <branch>
  - git push origin -d <branch>

# Git rebase用法

- 在 Git 中整合来自不同分支的修改主要有两种方法：merge 以及 rebase

- ![image-20231201103538332](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201103538332.png)

-  什么是rebase

  - 在上面的图例中

    - 可以提取在 C4 中引入的补丁和修改
    - 然后在 C3 的基础上应用一次

  - 在 Git 中，这种操作就叫做 变基（rebase）

  - 使用 rebase 命令将提交到某一分支上的**所有修改都移至另一分支**上

  - rebase

    - 我们可以将其理解成改变当前分支的base
      - base :根基
    - 比如在分支experiment上执行rebase master
      - 那么可以改变experiment的base为master

    

  - 切换到experiment分支中

    - git checkout experiment

  - 将master分支合并到experiment最后

    - git rebase master



# rebase 的原理

- 它的原理是首先找到这两个分支
- 即当前分支 experiment
  - 变基操作的目标
  - 基底分支master的
  - 最近共同祖先 C2
- 然后对比当前分支相对于
  - 该祖先的历次提交
  - 提取相应的修改并存为临时文件
- 然后将当前分支指向目标基底 C3
  -  最后以此将之前另存为临时文件的修改依序应用
  - ![image-20231201113747986](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201113747986.png)



# rebase和merge的选择

- 事实上，rebase和merge是对Git历史的不同处理方法
  -  merge用于记录git的所有历史
    - 那么分支的历史错综复杂，也全部记录下来
  -  rebase用于简化历史记录
    - 将两个分支的历史简化，整个历史更加简洁
- 了解了rebase的底层原理，就可以根据自己的特定场景选择merge或者rebase
- rebase有一条黄金法则：永远不要在主分支上使用rebase
  - 如果在main上面使用rebase
    - 会造成大量的提交历史在main分支中不同
  - 而多人开发时，其他人依然在原来的main中
    - 对于提交历史来说会有很大的变化

![image-20231201113804903](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201113804903.png)