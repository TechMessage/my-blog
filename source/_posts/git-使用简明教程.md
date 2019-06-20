---
title: git 使用简明教程
date: 2019-06-20 19:55:55
tags: git
categories: tutorials
---


# Git 快速上手教程
> 旨在快速上手使用开发

## git 的由来和理念
[分布式vs集中式](https://www.liaoxuefeng.com/wiki/896043488029600/896202780297248)



## 1 安装和配置git
[安装配置](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)


## 2 使用步骤

1. 本地开启git版本管理库，简单的立即为本地版本库，该库管理目录下所有文件的修改记录，可以回退。
>  ***在目标目录下  git init***

2. 需要明确一点，git版本控制系统只能追踪 ***文本类型的文件*** 的变化，比如某个.js文件的修改，第10行添加了一行代码，第5行注释等等，对于媒体等2进制文件是不能追踪到文件的变化的。不幸的是office文件都是二进制的文件。

3. 文件修改后，提交git仓库 三步走  
```
git add xxx      //xxx 表示文件名 ( git add . 表示添加所有文件 )  表示添加文件到仓库 

git commit -m '优化图片上传代码'  // 文件提交到仓库，并且带上本次提交的日志信息，方便之后查看历史记录以及版本恢复
 
```
    
4. 查看本仓库下文件的修改情况和 提交情况
> ***git status*** 如果有文件修改没有 添加 和 提交到 仓库 那么会有提示信息


5. 查看文件的具体修改情况
> ***git diff xxx***


6. 多次提交之后，想要查看历史提交的记录以及回退
> ***git log --pretty=oneline***
![历史记录](/images/Snipaste_2019-06-14_23-11-14.png)
前面的sha1算法生成的唯一id，HEAD标记当前版本库的所在状态
``` 
    版本回退
    
    git reset --hard bd9efa // 回到上一个版本，回到过去

    穿越未来，如果回到过去版本，又想回来现在，那么
    git reflog  显示所有的版本id
    git reset --hard xxxx // xxx是版本id，不用写全，一般前几位就可以

```

7. 工作区和版本库 -- 概念
[工作区和版本库](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)

> 工作区  git add ====>  暂存区  git commit =====>    主分区


8. 文件修改回退操作   
```
    文件的回退操作 根据文件的状态 git status

    1. 文件修该了，目前状态在工作区，没有git add
       git checkout -- test.js // 直接撤销修改
    
    2. 文件已经在git add操作过，在暂存区 
       git reset HEAD test.js  // 将该文件修改从暂存区 踢出去到 工作区
       git checkout -- test.js // 撤销修改

    3. 文件修改过，且git commit 了，那么只能版本库回退了

```

## 3 远程仓库
> 本地的仓库可以和远程仓库关联同步，这样远程仓库就可以作为一个中心库
![远程仓库同步](/images/Snipaste_2019-06-15_00-09-30.png)



## 4 分支管理
> git的分支功能非常灵活而且高效，推荐多使用分支开发
``` 
    基本流程
    1. 新需求， 开一个新分支，开发完后合并到dev分支，
    2. 该bug,  开一个bug分支， 改完后合并到dev
    ....

    分支的开销很小
```

1. 分支的创建 和 合并

> Git 仓库初始状态只有一master 主分支， 每次提交会形成一条时间线，记录版本，HEAD指针指向当前的版本

[分支的工作原理](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)


2. 分支的冲突解决
> 不同的分支对同一个文件的修改提交有可能会造成 冲突，需要手动修改后再次提交


3. 分支的合并，默认是快速模式，这样合并后，分支的信息会丢失

> git merge --no-ff 普通模式 保留分支信息


4. bug分支
> 当你正在开发时，需要在创建一个bug分支来修改某个bug，但是你的开发还没完成，暂时不能commit， git stash 将现在的开发储存起来，之后在恢复
[stash操作](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)

5. feature分支
> 添加新功能的时候，不想把master分支搞乱掉，所有新建分支来做是比较好的方式。如果不想开发完后又不想要了，那么不合并就删除,git会发出警告



## 5 版本发布
> 打包发布一个版本时，给版本库一个标签号tag,用来追溯发布历史，是非要有效的。默认打标签就是在最近的一次commit上
```
git tag v1.x    // 默认打标签就是在最近的一次commit 上

git tag v1.2 f52c633 //对之前的一次commit 打标签


```
1. 标签打错了，可以删除 git tag -de v1.0

2. 推送本地标签 git push origin v1.0

3. 推送所有 git push origin --tags

4. 本地和远程删除标签
```
   git tag -d v0.9
   git push origin :refs/tags/v0.9
```

## 6 git 忽略文件
1. 项目的一些配置文件，包括编译文件，是不需要被git管理的，配置.gitignore

```
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa

```


## 7 git 命令配置别名
> git 命令太长容易敲错，可以添加别名

``` 
    //配置别名
    git config --global alias.xx commit 

    //查看全局配置
    git config -l

    //

    alias.s=status  // 
    alias.a=!git add . && git status
    alias.au=!git add -u . && git status
    alias.aa=!git add . && git add -u . && git status
    alias.c=commit
    alias.cm=commit -m
    alias.ca=commit --amend
    alias.ac=!git add . && git commit
    alias.acm=!git add . && git commit -m
    alias.l=log --graph --all --pretty=format:'%C(yellow)%h%C(cyan)%d%Creset %s %C(white)- %an, %ar%Creset'
    alias.ll=log --stat --abbrev-commit
    alias.lg=log --color --graph --pretty=format:'%C(bold white)%h%Creset -%C(bold green)%d%Creset %s %C(bold green)(%cr)%Creset %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
    alias.llg=log --color --graph --pretty=format:'%C(bold white)%H %d%Creset%n%s%n%+b%C(bold blue)%an <%ae>%Creset %C(bold green)%cr (%ci)' --abbrev-commit
    alias.d=diff
    alias.master=checkout master
    alias.spull=svn rebase
    alias.spush=svn dcommit
    alias.alias=!git config --list | grep 'alias\.' | sed 's/alias\.\([^=]*\)=\(.*\)/\1\     => \2/' | sort
```


## 8 git服务器搭建
> github是开源的公开的，商业项目应该自己搭建一个远程仓库服务器

[步骤搭建](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)


