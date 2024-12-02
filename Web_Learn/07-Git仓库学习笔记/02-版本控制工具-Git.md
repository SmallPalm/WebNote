# 	Git的校验和

- Git 中**所有的数据**在存储前都计算校验和，然后以 **校验和** 来引用。
  - Git 用以计算校验和的机制叫做 SHA-1 散列（hash，哈希）
  - 这是一个由 40 个十六进制字符（0-9 和 a-f）组成的字符串
    - 基于 Git 中文件的内容或目录结构计算出来
    - ![image-20231128194922566](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231128194922566.png)

# 查看提交的历史

- git log
- 在提交了若干更新
  - 又或者克隆了某个项目之后
  - 有时候我们想要查看一下所有的历史提交记录
- 这个时候我们可以使用git log命令
  - 不传入任何参数的默认情况下
    - git log 会按时间先后顺序列出所有的提交
    - 最近的更新排在最上面
- 这个命令会列出每个提交的 **SHA-1 校验和**
  - 作者的名字和电子邮件地址、提交时间以及提交说明
- 更佳简洁的方法
  - git log --pretty=oneline
- 查看分支历史的方法
  - git log --pretty=oneline  --graph
  - ![image-20231128195220415](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231128195220415.png)



# 版本回退

- git reset
-  如果想要进行版本回退
  - 我们需要先知道目前处于哪一个版本
    - Git通过HEAD指针记录当前版本
- HEAD 是当前分支引用的指针
  - 它总是指向该分支上的最后一次提交
- 理解 HEAD 的最简方式
  - 就是将它看做 **该分支上的最后一次提交** 的快照
- 我们可以通过HEAD来改变Git目前的版本指向
  - 上一个版本就是HEAD^
    - git reset --hard HEAD^
  - 上上一个版本就是HEAD^^
    - git reset --hard HEAD^^
  - 如果是回退1000个版本
    - git reset --hard HEAD~1000
  - 可以指定某一个commit id
    - git reset --hard 校验和 (写6到9位就即可)
- 如果想从新回到最新的文件
  - 直接使用指定某一个commit id
    - 根据校验和回到最新的文件即可

# 什么是远程仓库

- 什么是远程仓库（**Remote** Repository）
  - 目前我们的代码是保存在一个本地仓库中
    - 也就意味着我们只是在进行本地操作
  - 在真实开发中，我们通常是多人开发的
    - 所以我们会将管理的代码共享到远程仓库中
- 如何创建一个远程仓库呢
  - 远程仓库通常是搭建在某一个服务器上的
    - 当然本地也
    - 可以，但是本地很难共享
  - 所以我们需要在Git服务器上搭建一个远程仓库
- 目前我们有如下方式可以使用Git服务器
  - 使用第三方的Git服务器：比如GitHub、Gitee、Gitlab等等
  - 也可以在自己服务器搭建一个Git服务

## 访问远程仓库的验证

- 对于私有的仓库我们想要进行操作
  - 远程仓库会对我们的身份进行验证
  - 如果没有验证，任何人都可以随意操作仓库是一件非常危险的事情
- 目前Git服务器验证手段主要有两种
  - 方式一：基于HTTP的凭证存储（Credential Storage)
  - 方式二：基于SSH的密钥

## 验证 – HTTP的凭证存储

- 因为本身HTTP协议是无状态的连接
  - 所以每一个连接都需要用户名和密码
  - 如果每次都这样操作，那么会非常麻烦
  - 但幸运的是，**Git 拥有一个凭证系统**来处理这个事情\
- 下面有一些 Git Crediential (凭证) 的选项

选项一 : 不使用 

- 默认所有都不缓存。每一次连接都会询问你的用户名和密码

选项二 : 不使用

- “cache” 模式会将凭证存放在内存中一段时间
  -  密码永远不会被存储在磁盘中
    - 并且在15分钟后从内存中清除

选项三 : 比较危险

- “store” 模式会将凭证用明文的形式存放在磁盘中
  - 并且永不过期

选项四 : 使用

- 它会将凭证缓存到你系统用户的钥匙串中（加密的）
- 如果你使用的是 Windows
  - 你可以安装一个叫
    -  “Git Credential Manager for Windows” 的辅助工具
  - **这个工具git自带了**
- 当第一次输入密码时
  - 会将凭证缓存到你系统用户的钥匙串
  - 并且永久保存
- ![image-20231128201940665](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231128201940665.png)

## 验证 – SSH密钥

- Secure Shell（安全外壳协议，简称SSH ) 
  - 是一种加密的网络传输协议
  - 可在不安全的网络中为网络服务提供安全的传输环境
- SSH以**非对称加密**实现身份验证

方式一

- 是使用自动生成的公钥-私钥对来简单地加密网络连接
  - 随后使用密码认证进行登录

方式二

- 人工生成一对公钥和私钥
  - 通过生成的密钥进行认证
  - 这样就可以在不输入密码的情况下登录
- 公钥需要放在待访问的电脑之中
  - 而对应的私钥需要由用户自行保管

- 如果我们以SSH的方式访问Git仓库
  - 那么就需要生产对应的公钥和私钥

这两个命令是固定的 选其一即可 ed25519这个方法流行

- ssh-keygen -t ed25519 -C “自己的邮箱"
- ssh-keygen -t rsa -b 2048 -C “your email"

# 管理远程服务器

- 查看远程地址
  - 比如我们之前从GitHub上clone下来的代码
    - 它就是有自己的远程仓库的
  - git remote
  - git remote –v
    - -v是—verbose的缩写(冗长的)
- 添加远程地址
  - 我们也可以继续添加远程服务器
  - 让本地的仓库和远程服务器仓库建立连接

- git remote add <shortname> <url>
- git remote add gitlab http://152.136.185.210:7888/coderwhy/gitremotedemo.git
  -  <shortname>  : 自己起的名字
  - <url> : 远程服务器仓库的地址
- 重命名远程地址
  - git remote rename gitlab glab
    - gitlab : 原来的名字
    - glab : 重新的名字 
- 移除远程地址
  - git remote remove gitlab

# 远程仓库的交互

- git pull origin master --allow-unrelated-histories 
- 从远程仓库clone代码将存储库**克隆到新创建的目录**中
  - git clone 
- 将代码push到远程仓库：将**本地仓库的代码推送到远程仓库**中
  - 默认情况下是将当前分支（比如master）
    - push到origin远程仓库的
  - git push
- 指定push到那个分支中
  - **git push origin master**
- 从远程仓库fetch代码：从远程仓库获取最新的代码
  - git fetch
- 默认情况下是从origin中获取代码 
  - git fetch origin

- 获取到代码后默认并没有合并到本地仓库
  - 需要通过merge来合并
  - git merge
  - 也可以指定合并那个仓库
  - git merge origin/master
  - 合并远程分支时
    - 会拒绝合并不相干的历史

  - 原因是: 本地仓库和远程仓库不相干
    - 我们将两个不相干的分支进行了合并

  - 使用--allow-unrelated-histories
    - 选项来逃逸这个限制
      - 来合并两个独立的项目

- 从远程仓库pull代码：上面的两次操作有点繁琐，我们可以通过一个命令来操作
  - git pull
    - git fetch + git merge(rebase)


​	

# 开发流程-远程仓库

![image-20231129102228137](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231129102228137.png)





# 给本地仓库创建远程仓库连接



- 给本地仓库添加远程仓库地址
  - git remote add origin https://gitee.com/limy718/git-test.git
- 在本地查看是否添加成功
  - git remote -v

- 从远程仓库获取代码
  - git pull



- 获取不成功
  - 告诉git fetch 需要获取那个分支的代码
    - git fetch origin master
  - 并且需要设置跟踪是代码的上游分支
    - git branch --set-upstream-to=origin/master
    - upstream : 上游

配置完成之后, 再次获取远程仓库代码



- 从远程仓库获取最新的代码
  - git fetch

- 获取到代码后默认并没有合并到本地仓库

  - 需要通过merge来合并

  - git merge

并且需要将那些不相关的历史文件合并

- git merge --allow-unrelated-histories



# 分支不同时 , 怎么样上传

前提是没有修改push.default的默认行为

- 上传指定分支

  - git push origin master:main
    - git push origin head:main
      - head默认指定当前分支
      - main指定的远程分支

- 如果不指定远程分支

  - git push origin master

  - git push origin head
    - 会自动在远程分支中创建当前分支的名称
      - 并且上传成功 

 push.default设置默认行为

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



- 切换分支
  - git checkout

