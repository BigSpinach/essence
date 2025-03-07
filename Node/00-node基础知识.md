

## node基础知识



### 1 常用的DOS命令

`ping www.baidu.com -t`：测试网速
`Ctrl+c`：结束当前正在运行的操作
`exit`：退出当前窗口
`ipconfig -all`：查看当前电脑的 物理地址/IP地址/子网掩码/DNS等信息
`cls`：清屏
`cd`：进入到指定的文件目录（windows电脑需要先进入到对应的磁盘 `E:`）
`cd ../`：返回上级目录
`cd ./`：当前目录
`cd /`：根目录
`dir`：查看当前目录下所有的文件
`mkdir`：创建文件夹
`copy con xxx.xx`：创建文件并且给文件中输入内容，输入完成后，用Ctrl+c结束并保存
`del xxx.xx`：删除文件
`rmdir xxx`：删除文件夹
...

### 2 NPM模块管理

安装完成node后，基本上自带npm模块管理器

我们需要一个第三方（别人写的）模块、插件、类库或者框架等，需要提前下载安装才可以使用
- 百度搜索，找到下载地址，然后基于浏览器下载即可（资源比较混乱，不好搜索）
- 也可以基于npm等第三方包管理器下载（yarn / bower ... 都是第三方模块管理器）

#### 2.1 NPM (node package manager)

`npm install xxx`：把资源或者第三方模块下载到当前目录下
`npm install xxx -g (--global)`：把资源或者第三方模块安装到全局环境下（目的：以后可以基于命令来操作一些事情）
`npm uninstall xxx / npm uninstall xxx -g`：从本地或者全局卸载

> 基于npm安装的一些细节点：
> - 需要连网（基于npm是从国外服务器上下载资源，所以下载速度较慢）
> - 下载成功后，当前目录中多增加一个 node_modules文件夹，在这个文件夹中找到我们安装的模块
> - 一般来说，下载下来的内容包含源码和最后供开发者使用的压缩版本

#### 2.2 解决下载慢的问题
**`基于npm切换到国内下载源（一般是淘宝镜像）`**
首先安装nrm，而且是把它安装到全局环境下（因为我们需要使用命令）

> npm install npm -g
>
> 安装完成后，我们可以使用 nrm 命令
> - nrm ls 查看当前可用源
> - nrm use xxx 使用某个源
>
> 切完源，还是基于npm安装操作

**`可以基于yarn来安装管理`**
首先还是需要先安装yarn，安装到全局，然后基于yarn安装我们需要的模块
> npm install yarn -g
>
> 基于yarn安装（只能安装在本地，不能安装到全局）
> yarn add xxx
> yarn remove xxx

**`安装cnpm淘宝镜像来处理`**
+ 1.安装`cnpm`
```
npm install --global cnpm
```
+ 2.从此以后
```
npm install xxx
//改写为
cnpm install xxx
```

**`不安装cnpm,配置npm的代理项来实现从cnpm下载资源`**
`第一种比较麻烦的方式`
```
npm install jquery --registry=https://registry.npm.taobao.org

//此方式麻烦就在与每次都要配置注册淘宝的源
```

`第二种方式：直接将淘宝的地址配置到npm的配置文件中`
```
npm config set registry https://registry.npm.taobao.org
//配置成功后，以后使用npm其实走的就是淘宝的服务器下载了（跟安装了cnpm一样）
```

`验证是否配置成功`
```
npm config list
```

#### 2.3 解决安装版本的问题

> 首先查看当前模块的历史版本信息
> `npm view jquery > jquery.version.json` ：把当前模块的历史信息输出到具体的某个文件中（文件名自己随便起的）
>
> 安装指定的版本模块
> `yarn add jquery@1.11.3`：npm和yarn都是这样来指定安装具体版本模块的



### 3 Git

> Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

`Git 与 SVN 区别`

> GIT不仅仅是个版本控制系统，它也是个内容管理系统(CMS),工作管理系统等。
> 如果你是一个具有使用SVN背景的人，你需要做一定的思想转换，来适应GIT提供的一些概念和特征。

**Git 与 SVN 区别点：**

+ 1、GIT是分布式的，SVN不是：这是GIT和其它非分布式的版本控制系统，例如SVN，CVS等，最核心的区别。
+ 2、GIT把内容按元数据方式存储，而SVN是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn,.cvs等的文件夹里。
+ 3、GIT分支和SVN的分支不同：分支在SVN中一点不特别，就是版本库中的另外的一个目录。
+ 4、GIT没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比GIT缺少的最大的一个特征。
+ 5、GIT的内容完整性要优于SVN：GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。

#### 3.1 git的基础知识

> git是一个分布式代码版本管理控制系统
> - 记录当前产品代码的所有版本信息（历史修改信息）,而且方便快速回退到某一个具体的版本
> - 方便团队协作开发，能够检测代码冲突，能够合并代码等

`svn`：在git诞生前就已经存在的版本控制系统，不过它是“集中式”管理
`git`：是分布式版本管理体统

1.集中式版本控制系统

2.分布式版本控制系统

#### 3.2 git的工作管理和基础操作

**`在本地创建git仓库管理我们的代码`**

> 初次使用git，先在本地配置一些基础信息
> \$ git config -l
> \$ git config --global user.name  xxx
> \$ git config --global user.email  xxx
> 建议大家配置的用户名和邮箱和gitHub保持一致（这样以后在本地向gitHub推送内容的时候，能够展示出是谁推荐的）

1. `git init`
> 会在当前目录中创建一个空的仓库，文件目录中生成一个 “.git” 的隐藏文件，这个文件很重要，我们本地仓库的版本信息等都存储在这里

2. `.gitignore`
> 在当前目录（git仓库根目录）创建一个 “.gitignore” 文件，这个文件中存储了当git提交的时候所忽略的文件
>
> 可以基于WB创建（new -> file -> .gitignore）
> 可以基于linux命令 `$ touch .gitignore` （mac终端、git bash、或者集成了linux的dos，可以使用linux命令）

#### 3.3  GIT工作原理及操作

**在本地创建一个git仓库后，然后就可以基于这个仓库管理本地的代码**
**`git的工作流程`**

> 每一个git仓库都划分为三个区域
> - 工作区：编辑代码的地方
> - 暂存区：临时存储要生成版本代码的地方
> - 历史区：存储的是生成的每一个版本代码

**工作区提交到暂存区`**

> $ git status
> 查看代码或者文件的状态（当前处于哪个区域）:  红色（当前处于工作区，还没有提交到暂存区）绿色（当前处于暂存区，还没有提交到历史区）如果没有文件，代表三个区域代码已经同步，历史版本也在历史区生成了

`$ git add . / $ git add -A`
把当前工作区中所有最新修改的文件，都提交到暂存区

**`暂存区到历史区`**
`$ git commit`
> 这样执行后，会弹出一个提交文本输入界面，需要我们编写本次提交到历史区，给当前版本编写的备注信息
>
> 先按 i 进入编辑插入模式
> 输入备注信息
> 按ESC
> 输入“ :wq ” 保存并退出

`$ git commit -m'自己需要编写的备注信息'`

`$ git log`
查看当前历史区提交的记录（查看版本信息）

`$ git diff`
工作区 VS 暂存区

`$ git diff master`
工作区 VS 历史区（master分支）

`$ git diff --cached`
暂存区 VS 历史区

#### 3.4 git和gitHub同步

1. 让本地的git仓库和远程仓库建立关联

`$ git remote -v`
查看所有的关联信息

`$ git remote add xxx [远程仓库git地址]`
建立关联

`$ git remote remove xxx`
移除关联

我们远程仓库关联在一起的名字默认是：origin，当然自己可以随意修改

2. 把本地的信息推送到远程仓库上，或者从远程仓库上拉取最新的信息到本地仓库
> 我们本地推送和拉取的信息，既有代码也有版本信息，所以说与其说是推送和拉取，不如说是和远程仓库保持信息的同步

在推送之前，我们都应该先拉取
`$ git pull origin（这个名字就是和远程仓库关联的这个名字，以自己设置的为主） master`
从远程仓库的master分支拉取最新的信息

`$ git push origin master`
把自己本地信息推送到远程仓库的master分支下

---------------

以上是操作知识点，真实项目开发流程
1. LEADER会首先创建一个远程仓库（这个仓库可能是空的，也可能是包含了项目需要的基础的结构信息）
2. 作为开发者，我们需要在本地创建一个本地仓库，还需要让当前本地的仓库和远程仓库保持关联
> 原始做法：
> git init 
> git remote add origin [GIT仓库地址]
>
> 简单做法：
> git clone [远程仓库地址] [克隆后的名字：可以不设置，默认是仓库名]

3. 在本地开发产品，需要同步的时候，我们首先把工作区内容在本地仓库中放到历史区，生成版本信息（git add . / git commit -m''），在把本地历史区的信息推送到远程仓库上（git pull / git push）

4. 在团队协作开发的时候，LEADER会在自己的gitHub账号下创建一个远程仓库，那么团队其他成员在向这个远程仓库推送信息的时候，使用自己的账号是没有推送权限的，我们需要把当前这个远程仓库，在github中创建工作群组，让更多人用自己的账号也有操作权限
5. 小组成员在自己的邮箱中收到一封邀请邮件，需要确认同意

### 4. GitHub





