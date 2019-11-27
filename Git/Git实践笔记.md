# Git实践笔记

## 第一章 git 介绍

### 第一节 git 的作用

- 项目版本控制
- 项目多人协作
- 项目管理
- 获取和分享开源项目 

### 第二节 git的安装


> https://git-scm.com/   // 官网下载
>



### 第三节 git的基本配置

> 因为Git是分布式版本控制系统，所以，每台电脑必须自报家门，包括开发者的名字与Email地址， 否则版本库不知道是哪位开发者贡献的代码。

```shell
$ git config --global user.name "Your Name"           // 配置用户名
$ git config --global user.email "email@example.com"  // 配置邮箱 
$ git config --global --list  // 查看当前git的配置信息 
```



## 第二章 提交代码

### 第一节 创建仓库

```shell
git init
```

### 第二节 获取项目

```shell
git clone https://github.com/didi/mpx.git
```

### 第三节 提交代码


* 工作区：就是文件目录, 这里存放项目的所有文件;  
* 暂存区:  我们需将工作区文件提交到版本库，才能实现对文件的版本控制，而暂存区时文件从工作区到版本库的一个临时存储区域; 
* 本地版本库：工作区有一个隐藏目录.git，就是Git的版本库, 只有提交到版本库的文件才能被git追踪;    


![图片](images/git_03.png)

```shell
git add README.md
git commit -m '完成版本1.0的开发'
```

#### 1. 批量添加

```shell
git add *
```

#### 2. 文件忽略 `.gitignore`



#### 3. 添加后修改




#### 4. 删除文件



### 第四节 查看提交日志

```shell
git log
git log --pretty=oneline
```



### 第五节 提交到远程仓库

```shell
git push
```



### 第六节 创建个人网站

hexo



## 第三章 版本管理

### 第一节 查看历史

```shell
git log
```



### 第二节 文件比较 

```shell
git diff
```



### 第三节 回滚与版本切换

#### 从暂存区恢复

![](images\basic-usage.svg.png)


```shell
git checkout


git add readme.md
// edit readme.md
git checkout -- readme.md
```



#### 从仓库恢复


```shell
git reset -- readme.md
git checkout -- readme.md
```



![](images\basic-usage-2.svg)



```shell
git checkout HEAD readme.md
```



#### 从指定的版本恢复

```shell
git checkout fdafdsa readme.md
```

```
git checkout HEAD readme.md
git checkout HEAD^^ readme.md
git checkout HEAD~4 readme.md
```



## 第四章 多人协同 代码同步

### 第一节 提交远程仓库

```
git push
```



### 第二节 更新代码

```shell
git pull

git fetch
git merge
```



### 第三节 冲突

#### 造成冲突

如果pull获取的文件，当前正在修改，将无法pull，需要先保存（commit 或 stash）。 

- 不同文件合并
- 同文件不同修改合并
- 同文件对同一行代码修改合并

#### 解决冲突

合并冲突，重新提交。



### 第四节 使用stash

#### 保存

```shell
$ git stash
```

#### 恢复

```shell
$ git stash pop
```



## 第五章 使用分支做项目管理

### 第一节 分支作用

案例：

- 开发定制版
- 发布大版本

### 第二节 查看分支

```shell
$ git branch
```

### 第三节 创建分支

```shell
$ git branch dev
```

### 第四节 切换分支 

```shell
$ git checkout dev
$ git swich dev
```

 创建并切换到`dev`分支：

```shell
$ git checkout -b dev
```



- checkout 会修改工作区中的代码

checkout小结

- 从stage恢复到工作区
- 从HEAD恢复到工作区
- 从History恢复到工作区
- 切换分支



### 第五节 推送分支

```shell
$ git push origin dev
```



### 第六节 合并分支

#### 1. 查看分支合并图

显示git分支图的命令是：

```shell
git log --oneline --graph --all
```

#### 2. 合并分支

```shell
$ git merge dev
```



### 第七节 删除分支 

```shell
$ git branch -d dev
```



## 第六章 git在项目管理中的应用 gitflow

### 第一节 分支管理

| 分支     | 功能         | 克隆分支 | 临时 | 说明                                                         |
| -------- | ------------ | -------- | ---- | ------------------------------------------------------------ |
| master   | 主分支       | -        | 否   | 产品的功能全部实现后，最终在master分支对外发布。             |
| develop  | 开发分支     | master   | 否   | 编码工作在此分支进行。                                       |
| release- | 测试分支     | delevop  | 是   | 测试过程中发现的bug直接在本分支进行修复，修复完成后合并回develop分支。 |
| hotfix-  | 热修复分支   | master   | 是   | 用于修复对外发布的分支，收到客户的Bug反馈后，在此分支进行修复，修复完毕后分别合并到develop分支和master分支。 |
| feature- | 功能特征分支 | develop  | 是   | 用于多人协助开发场景或探索性功能验证场景，功能开发完毕后合并到develop分支。 |

![git主要分支](images/git%E4%B8%BB%E8%A6%81%E5%88%86%E6%94%AF.png)

```shell
git branch
git branch dev
git checkout dev
```



### 第二节 开发新版本

#### 2.1 切换到本地工作区

```shell
cd /home/workspace
```



#### 2.2 从远程仓库克隆代码到本地仓库

```shell
$git clone https://xxxx@xxx:xxx/xxx.$git
```



#### 2.3 基于master分支，创建develop分支

```shell
/* 切换到master分支 */
$git checkout master
/* 基于master分支克隆develop分支，并在克隆完毕后直接跳转到develop分支 */
$git checkout -b develop
/* 推送develop分支到远程仓库 */
$git push origin develop
```



#### 2.4 在本地仓库进行开发

```shell
/* 提交修改到缓冲区 */
$git add *
/* 提交修改到本地仓库 */
/* 如果是修复的BUG，应该在修改说明的最开始添加Bug#ID，多个Bug用逗号分隔，例如Bug#002,003 */
/* 如果是完成了一个指派的任务，应该在修改说明的最开始添加Task#TaskID,例如Task#165 */
$git commit -m "Bug#123 修改说明"
/* 每完成一个功能点可以对代码进行打包 */
$git tag -m "简要说明增加/修复/删除了什么功能" v0.0.0.170718
```

> 不是每一个Tag都需要提交到远程仓库，比如可以在完成一个功能点的编码工作后未编译就打一个包，仅存储于本地仓库，在编译成功&测试通过后，再打一个新的Tag包（里程碑Tag包），仅将里程碑Tag包推送到远程仓库。



#### 2.5 推送代码到远程仓库

> 当完成一个功能点或阶段工作时，将代码推送到远程仓库develop分支。

```shell
/* 执行代码拉取操作，防止代码冲突 */
$git pull
/* 解决代码冲突后，推送代码到远程仓库*/
$git push origin develop
```

> 禁止将未编译或编译不通过的代码提交到远程仓库，如果编码工作进行未完成可以提交到本地仓库中，等待该功能点全部实现后再将代码推送到远程仓库中。



#### 2.6 将代码发布到测试分支



#### 2.7 测试工程师提交Bug后修复



#### 2.8 测试工作完成后，合并代码到develop分支

```shell
/* 切换到develop分支 */
$git checkout develop
/* 执行合并操作,将release分支代码合并到develop分支 */
$git merge release
/* 如果合并报错，则解决冲突，冲突解决后继续再次执行合并 */
```



#### 2.9 开发工作和测试工作都完毕后，发布时将develop分支合并到主线

```shell
$git checkout master
$git merge develop
```



#### 2.10 阶段开发完毕，打一个里程碑Tag包

```shell
/* 创建里程碑Tag */
$git tag -m "Task#003 v1.0.0 首版发布" v1.0.0.170718
/* 推送里程碑Tag到远程仓库 */
$git push origin v1.0.0.170718
```



### 第三节 发布后产品Bug修复



### 第四节 githubflow

https://guides.github.com/introduction/flow/



[Git工作流指南：Gitflow工作流](https://www.cnblogs.com/jiuyi/p/7690615.html)

[GitFlow工作流常用操作流程](https://blog.csdn.net/zsm180/article/details/75291260)

[Git教程](http://www.runoob.com/git/git-branch.html)



## 第七章 git常用配置

使用beyond compare

gui



## git 常用命令总结

