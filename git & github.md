[toc]

# git & github

## 版本控制

### 为什么需要版本控制

#### 个人开发改进迭代

自己需要修改一个类中的东西，如果前面的版本代码更好修改但是没有储存的话，那么就只能覆盖导致不方便修改，所以需要版本控制。

#### 团队协作

两个或多个人需要修改同一个类内容的话，也会有覆盖的副作用，所以也需要版本控制。

### 版本控制简介过程

1.  版本控制

    工程设计领域中使用版本控制管理工程蓝图的设计过程。在IT开发过程中也可以使用版本控制思想管理代码的版本迭代

2. 版本控制工具

    思想：版本控制

    实现：版本控制工具

    集中式版本控制工具：

    ​		CVS、SVN、VSS等

    ​		服务器损坏，那就没有了（有点像CS模型，有单点故障）

    分布式版本控制工具：

    ​		Git、Mercurial、Bazaar、Darcs

    ​		本地进行版本控制（P2P？可以避免单点故障）

### 版本控制工具介绍

### 具备功能

1.   协同修改 

     多个人并行不悖的修改服务器段的同一个文件。

2.   数据备份

     不仅保存目录和文件的当前状态，还能保存每一个提交过的历史状态。

3.   版本管理

     在保存每一个版本的文件信息的时候要做到不保存重复数据，以节约存储控件，提高运行效率。SVN采用的是增量式管理（做的改动保存起来，需要的时候将改动和之前的版本拼起来）的方式，Git采取了文件系统快照的方式。

4.   权限控制

     -   对团队中参与开发的人员进行权限控制。
     -   对团队外开发者贡献的代码进行审核--Git独有。

5.   历史记录

     -   查看修改人、修改时间、修改内容、日志信息。
     -   将本地文件恢复到某一个历史状态。

6.   分支管理

     允许开发团队在工作过程中多条生产线同事推进任务，进一步提高效率。

## Git简介

### Git发展历史

### Git的优势

1. 大部分操作在本地完成
2. 完整性保证（Hash）
3. 尽可能添加数据而不是删除或修改数据
4. 分支操作非常快捷流畅
5. 与Linux命令全面兼容

### Git结构

![截图 2022-07-02 09-57-37](/home/yuuki/资料/git and github/截图 2022-07-02 09-57-37.png)

### Git和代码托管中心

​		代码托管中心的任务：维护远程库

局域网环境下

-   GitLab

外网环境下

-   GitHub
-   码云

### Git安装

### 本地库和远程库

1. 团队内部协作
2. 跨团队协作

## Git命令行操作

### 本地库初始化

​	命令：

~~~bash
git init
~~~

​	效果：

![截图 2022-07-02 10-13-38](/home/yuuki/资料/git and github/截图 2022-07-02 10-13-38.png)

​	注意：.git目录中存放的是本地库相关的子目录和文件，不要删除，也不要胡乱修改。

### 设置签名

1. 形式：

    用户名：Tom

    Email地址：goodMorning@qq.com

2. 作用：区分不同开发人员的身份

3. 辨析：这里设置的签名和登录远程库（代码托管中心）的账号，密码没有任何关系。

4. 命令

    -   项目级别/仓库级别：仅在当前本地库范围内有效

        -   ~~~bash
            git config user.name tom_pro
            ~~~

        -   ~~~bash
            git config user.email goodMornin  g_pro@qq.com
            ~~~

        -   信息保存位置：./.git/cofig 文件

            ![](/home/yuuki/资料/git and github/截图 2022-07-02 10-30-02.png)

    -   系统用户级别：登录当前操作系统的用户范围

        -   ~~~bash
            git config --global user.name tom_glb
            ~~~

        -   ~~~bash
            git config --global goodMorning_pro@qq.com
            ~~~
    
        -   信息保存位置：~/.gitconfig 文件
    
            ![](/home/yuuki/资料/git and github/截图 2022-07-02 10-33-57.png)
    
    -   优先级
    
        -   就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名
        -   如果只有系统级别的签名，就以系统用户级别的签名为准
        -   二者都没有不允许

### 基本操作

#### 状态查看操作

~~~bash
git status
~~~

查看工作区、暂存区状态

#### 添加操作

~~~bash 
git add [filename]
~~~

将工作区的“新建/修改”添加到暂存区

#### 提交操作

~~~bash
git commit -m "commit message" [filename]
~~~

将暂存区的内容提交到本地库

#### 查看历史记录

~~~bash
git log
~~~



![](/home/yuuki/资料/git and github/截图 2022-07-02 11-30-26.png)

​	多屏显示控制方式：

​		空格向下翻页

​		b向上翻页

​		q退出

~~~bash
git log --pretty=oneline
~~~

![](/home/yuuki/资料/git and github/截图 2022-07-02 11-32-28.png)

~~~bash
git log --oneline
~~~

![](/home/yuuki/资料/git and github/截图 2022-07-02 11-33-26.png)

~~~bash
git reflog
~~~

![截图 2022-07-02 11-34-54](/home/yuuki/资料/git and github/截图 2022-07-02 11-34-54.png)

​	HEAD@{移动到当前版本需要多少步}

#### 前进后退历史版本

1.   本质

     HEAD指针

2.   基于索引值操作[推荐]

     ~~~bash
     git reset --hard [局部索引值]
     
     git reset --hard f0af588
     ~~~

3.   使用^：只能后退

     ~~~bash
     git reset --hard HEAD^
     ~~~

     

     注：一个^表示后退一步，n个表示后退n步

4.   使用~

     ~~~bash
     git reset --haed HEAD~n
     ~~~
     
     注：表示后退n步

三种模式

1.   --hard

     全都移动指针

2.   --mixed

     在本地库和暂存区移动指针，不改变工作区

3.   --soft

     仅仅在本地库移动指针，不改变工作区和暂存区

#### 删除文件并找回

前提：删除前，文件存在时的状态提交到了本地库。

操作：

~~~bash
git reset --hard [指针位置]
~~~

-   删除操作以及提交到本地库：指针位置指向历史记录
-   删除操作尚未提交到本地库：指针位置指向HEAD

#### 比较文件差异

-   将工作区的文件和暂存区进行比较

~~~bash
git diff[文件名]
~~~

-   将工作区的文件和本地库中历史版本比较

~~~bash
git diff[本地库中历史版本] [文件名]
~~~

-   比较多个文件

~~~bash
git diff
~~~

### 分支管理

#### 什么是分支

在版本控制过程中，使用多条线同时推动多个任务

![截图 2022-07-02 15-03-39](/home/yuuki/资料/git and github/截图 2022-07-02 15-03-39.png)

#### 分支的好处

1. 同时并行推进多个功能开发，提高开发效率
1. 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

#### 分支操作

1.   创建分支

     ~~~bash
     git branch [分支名]
     ~~~

2.   查看分支

     ~~~bash
     git branch -v
     ~~~

3.   切换分支

     ~~~bash
     git checkot [分支名]
     ~~~

4.   合并分支

     第一步：切换到接受修改的分支（被合并，增加新内容）上

     第二步：执行merge操作

     ~~~bash
     git checkout [被合并的分支名]
     git merge [有新内容的分支名]
     ~~~

5.   解决冲突

     分支的表现

     第一步：编辑文件，删除特殊符号

     第二步：把文件修改到满意的程度，保存退出

     第三步及第四步：

     ~~~bash
     git add [文件名]
     git commit -m "日志信息" (不带文件名)
     ~~~

## Git基本原理

### 哈希

### Git保存版本的机制

#### 集中式版本控制工具的文件管理机制

以文件变更列表的方式存储信息。这类系统将它们保存的信息看做是一组基本文件和每个文件随时间逐步累积的差异。

![截图 2022-07-02 15-37-20](/home/yuuki/资料/git and github/截图 2022-07-02 15-37-20.png)

#### Git的文件管理机制

Git把数据看做是小型文件系统的一组快照。每次提交更新时Git都会对当前的全部文件制作一个快照并保存这个快照的索引。为了搞笑，如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件。所以Git的工作方式可以称之为快照流。

![截图 2022-07-02 15-42-06](/home/yuuki/资料/git and github/截图 2022-07-02 15-42-06.png)

#### Git文件管理机制细节

##### Git的“提交对象”

![截图 2022-07-02 15-44-28](/home/yuuki/资料/git and github/截图 2022-07-02 15-44-28.png)

##### 提交对象及其父对象形成的链条

![截图 2022-07-02 15-48-16](/home/yuuki/资料/git and github/截图 2022-07-02 15-48-16.png)

### Git分支管理机制

#### 分支的创建

![截图 2022-07-02 15-49-51](/home/yuuki/资料/git and github/截图 2022-07-02 15-49-51.png)

#### 分支的切换

![截图 2022-07-02 15-52-24](/home/yuuki/资料/git and github/截图 2022-07-02 15-52-24.png)



![截图 2022-07-02 15-54-57](/home/yuuki/资料/git and github/截图 2022-07-02 15-54-57.png)

![截图 2022-07-02 15-54-38](/home/yuuki/资料/git and github/截图 2022-07-02 15-54-38.png)

## GitHub

### 操作

#### push

起别名 git remote add 别名 网址

git push 别名or网址 master

#### clone

git clone 别名or网址

#### pull

pull = fecth + merge

~~~bash
git fectch[远程库地址别名][远程分支名] 抓取，只是把远程内容下载到本地，没有改变本地文件。

git merge[远程库地址别名/远程分支名] 合并

直接用pull: git pull origin master
~~~

#### 解决冲突

要点：

1.   如果不是基于GitHub远程库最新版所做的修改，不能推送，必须先拉取
2.   拉取下来后如果进入冲突状态，则按照“分支冲突解决”操作解决即可。

类比：
1. 债权人：老王
2. 债务人：小刘
3. 老王说：10天后归还。小刘接受，双方达成一致。
4. 老王媳妇说：5天后归还。小刘不能接受。老王媳妇需要找老王确认后再执行。

#### 跨团队协作

![截图 2022-07-02 22-38-38](/home/yuuki/资料/git and github/截图 2022-07-02 22-38-38.png)

#### SSH登录

git remote add origin_ssh git@github.com:zhy-cx/huashan.git


## Git图形化界面操作

## Gitlab服务器环境搭建

