# Git





## 1.` Linux` 操作系统的常用命令

`cd`  进入磁盘目录的命令

> cd ../上级目录
>
> cd ./当前目录
>
> cd /根目录
>
> cd xxx
>
> cd d:

`ls` 查看当前目录的信息

> ls -l 查看详细信息
>
> ls -a 查看隐藏信息
>
> ls -la/-al 插卡详细信息和隐藏信息

`clear` 清屏

`kdir` 创建文件夹

> mkdir newFolder  创建**newFolder**文件夹

`touch` 创建文件

> touch a.txt 创建**a.txt**文件
>
> touch .lc 创建**.lc**这样的无文件名文件

`echo` 创建文件并向文件中插入内容

> echo hello world > a.txt 向**a.txt**文件中插入**hello world**这句话
>
> 注意： 如果**a.txt**不存在，则新建**a.txt**;如果**a.txt**文件已经存在，则用**helloworld**替换掉**a.txt **中之前所有的内容
>
> echo nextContent  >> a.txt        向**a.txt**文件中追加内容 

`vi` 编辑文件

> vi a.txt    执行此命令会进入**a.txt** 文件的命令模式
>
> - 然后  按**i**键----进入编辑模式
> - 编辑完成后
> - 按**ESC**退出编辑模式
> - 1> 编辑完想要保存退出命令模式
>   - 输入 **:wq**
> - 2> 编辑完不想保存，直接强制退出
>   - 输入 **:q！**

`cat` 查看文件内容

> cat a.txt   查看**a.tx**文件中的内容

`cp` 文件拷贝

> cp a.txt b.txt  把a.txt中的内容拷贝一份给 b.txt
>
> 注意: 被拷贝的文件必须存在，如果不存在将报错
>
> 如果拷贝出的文件**不存在**，将新建
>
> 如果拷贝出的文件**存在**，将被覆盖

`rm` 删除

> 删除文件
>
> - rm a.txt 删除**a.txt**这个文件
>
> 删除文件夹
>
> - rm xxx -r 递归删除**xxx**文件夹中所有的子代文件
> - rm xxx - f 强制删除
> - rm xxx -rf/-fr 强制删除**xxx**文件夹及其里边的所有内容

## 2. Git的工作原理和流程 

### 2.1 配置git基础信息

**只需要配置一次就可以了**

`查看配置信息`

> git config  -l

`配置基础信息`

> git config --global user.name = xxx
>
> git config --global user,email = xx@xx.com



### 2.2 Git工作流程

> 1. `git `是分布式版本控制系统，每一台客户端都是独立的`git仓库`（拥有git仓库的全套机制） > 
>
>    . 一个`git`分为三个区域 	
>
>    - 2.1 `工作区`: 平时写代码的地方（只有这个区域可见） 
>    - 2.2 `暂存区`：把一些写好的代码临时存储的区域 	
>    - 2.3 `历史区`：生成一个个版本记录的地方 	
>
>     **`暂存区` 和`历史区`都在`.git文件夹中`以不可见的形式存储**   

#### 2.2.1 Git 基本工作流程

**第一步：创建一个git仓库** 

> `$ cd  myGitDemo`     进入`myGitDemo`文件目录中 
>
> `$ git init` 以当前这个目录作为`git仓库`(默认会在当前目录下创建一个`.git`文件夹) 

**第二步：把工作区的内容提交到暂存区** 

> `$ git add xxx`  把工作区的某个内容提交到暂存区
> `$ git add .`   把工作区的所有内容提交到暂存区
> `$ git add -u` 把所有修改的文件（包含修改和删除的，**但不包含新增的**）
> `$ git add -A` 是`.`和`-u`的结合体，所有的修改、删除、新增都会提交到暂存区 （真是效果跟`.`差不多）
>
> `$ git status ` 查看当前文件的状态

- 红色： 在工作区中还没有提交到暂存区
- 绿色： 在暂存区中，还未提交到历史区



**第三步：把暂存区的内容提交到历史区**

> `$ git commit`
> 这种方式会进入命令行模式，然后进行编写提交历史版本的说明信息（一般这么操作：点击`i`， 然后进入输入内容模式，输入内容后，点击`esc`,然后点击`:wq`保存并退出命令行模式）
> `$ git commit -m 'xxx'` 
> 这种方式直接 在`-m` 后边跟上提交到历史区的版本说明



**工作区直接到历史区**

> `$ git commit -a -m "xxx"`
> 这种方式适合已经提交过至少一次到历史区的文件，被修改后，可以直接这样提交
>
> 对于新增减的文件，一次都没有提交过，是不允许这样操作的





#### 2.2.2 Git 的版本查看

> `$ git log `
>
> 查看历史提交记录（相当于查看历史版本号），在没有版本回退的时候使用`git log`，因为`git log`只能查看当前回退版本之前的版本 
>
> `$ git reflog` 
>
> （在有版本回退的时候）可以查看所有每一步回退的版本号 



## 3.  团队协作模式

每一个人是一个单独的本地仓库，有一个中央仓库，与欧诺个来汇总所有开发者的编码信息（中央仓库一般由leader创建，而且是最先创建的）

### 3.1  创建中央仓库

在GitHub或Coding或公司自己的服务器上创建中央仓库

【在`GitHub`上创建中央仓库】

> 1. new repository 新仓库名称
> 2. 按照提示创建仓库
>    ...
> 3. 基于GitHub得到一个中央仓库地址



现在有两种玩中央仓库的玩法

#### 3.1.1 `第一种`：基于本地提交的方式，把基础内容提交到中央仓库中

> 1. 把新增加的基础信息教教到本地仓库的历史区中
>    `$ git add .`
>     `$ git commit -m "提交信息说明"`
> 2. 让本地仓库和远程库建立连接
>    `$ git remote add origin 远程仓库地址`
>    `$ git remote rm 远程仓库的名字`-----移除跟远程库的关联
>    `$ git rm -v ` ----查看当前仓库和那些远程仓库关联
>
>

> 1. 把本地仓库历史区的信息推送（同步）到远程仓库上
>    `$ git push origin master` 把本地的历史区master主分支推送到远程仓库
>      `$ git pull origin master` 把远程仓库拉去到本地

#### 3.1.2 `第二种`：直接克隆远程仓库的方式

> `$ git clone 【远程仓库地址】 【新建自己本地仓库的名称】`
>
> 简单的方式
>
> 1. `$ git clone https://github.com/BigSpinach/gitTest.git newLocalRepository`
> 2. 操作本地仓库`newLocalRepository`去吧
>    ...
>    `$ git add.`
>    `$ git commit -m "基于克隆的方式操作..."`
>    `$ git push origin master`

### 3.2 团队协作

#### 3.2.1 无分支模式管理

所有人都使用`master`主分支，每天上班第一件事就是先拉去远程库的数据
`git pull origin master`
....
writed code...
...
`git add .`
`git commit -m "xxx"`
`git push origin master`

再提交给远程库的时候可能会发生冲突（自己提交的跟别人的文件冲突了）

> 1.远程仓库和自己本地仓库`不是`同一个文件同一行代码
>
> - git会自动的采用 `fast-foward`模式合并
> - 合并的结果就是：先将远程库和本地仓库进行合并，再将本地不同的文件提交到远程库
>
> 2.远程仓库和自己本地仓库`是`同一个文件同一行代码
>
> - **[git bash]**会报错
> - 错误信息是：我自己使用 `fast-forward`模式处理不了了，你自己来吧
> - 然后自己来
>   - 第一步：找到冲突的文件
>   - 第二步：打开冲突文件，选择保存
>   - 第三步：再次添加到历史区，并提交到远程库
>   - ok~~

#### 3.2.2 分支模式管理





####  







