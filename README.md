# github

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目

## 集中式 与 分布式

![avatar](https://www.runoob.com/wp-content/uploads/2015/02/0D32F290-80B0-4EA4-9836-CA58E22569B3.jpg)

## git 三大区

工作区(红色)

暂存区（绿色）

版本区(白色)

## command

### diff

```sql

比较工作区和暂存区的差异
git diff

比较暂存区和版本区的差异
git diff --cached

比较
git diff master
```

### 常用命令

```
git reset HEAD <file> : 暂存区与版本区保持一致

git checkout <file> : 暂存区覆盖工作区的内容

git rm <file> --cached : 删除暂存区文件

git commit -a -m <msg>: git add .

git reset --hard <version> : 恢复版本区指定版本的内容到工作区

git reflog : 查看引用版本号

git cherry-pick :将已经提交的 commit，复制出新的 commit 应用到分支里

git revert :将现有的提交还原，恢复提交的内容，并生成一条新的还原记录。

```

### 分支命令

```
git branch : 查看分支

git branch dev : 创建dev分支

git checkout dev : 切换到dev分支

git checkout -b dev : 创建并切换到dev分支

git branch -d dev : 删除dev分支
```

### 合并分支

```
git merge test : 把test分支合并到当前分支
git log --oneline --graph ： 展示历史操作图

```

### git Stash

```
# stash 命令能够将还未 commit 的代码存起来，让你的工作目录变得干净。
git stash

# 保存当前未commit的代码并添加备注
git stash save "备注的内容"

# 列出stash的所有记录
git stash list

# 删除stash的所有记录
git stash clear

# 应用最近一次的stash
git stash apply

# 应用最近一次的stash，随后删除该记录
git stash pop

# 删除最近的一次stash
git stash drop
```

### git reset

```
三种模式：hard soft mixed

git reset --hard [commit_id] : 重置 暂存区 和 工作区

git reset --soft [commit_id] : 暂存区和工作区都不会被重置

--soft 模式 会在重置 HEAD 和 branch 的指针位置 的同时，保留工作区和暂存区中的内容，并把重置 HEAD 指针位置 所带来的新的差异放进暂存区（将已 commit 到仓库的内容放到暂存区）

git reset 不带参数则默认使用--mixed模式。 重置暂存区

git reset [commit_id] : 只保留工作区内容，并将已 commit 到仓库的内容和暂存区放到工作区
--mixed模式 会在重置 HEAD 和 branch 的指针位置 的同时，会保留工作目录，并将已 commit 到仓库的内容和暂存区放到工作区，并且清空暂存区。
```

# git pull 和 git fetch 的区别
- git fetch 只是将远程仓库的变化下载下来，并没有和本地分支合并。

也就是 fetch 的时候本地的 master 没有变化，但是与远程仓关联的那个版本号被更新了，接下来就是在本地 merge 合并这两个版本号的代码
  
- git pull 会将远程仓库的变化下载下来，并和当前分支合并。



# git merge 与 git rebase 的区别？

## 例子

1. 我们从master分支里拉出一条新分支为dev分支
   
![Alt text](assert/merge-rebase/1.png)

2. 在dev分支上开发，并且完成了三次commit,目前指针指向C5

![Alt text](assert/merge-rebase/2.png)


3. 在准备第四次提交的时候，另外一个同事在master主分支上进行了一次提交，master的提交已经向前走了

![Alt text](assert/merge-rebase/3.png)

此时我们知道B同事开发的dev分支是基于C2提交点切出来的，而这个时候master分支已经被更新了

如果B同学开发完毕，需要将其所作的功能合并到master分支 ，他可以有两种选择：

## 直接git merge，那么这个时候会这么做

（1）找到master和dev的共同祖先，即C2

（2）将dev的最新提交C5和master的最新提交即C6合并成一个新的提交C7，有冲突的话，解决冲突

（3）将C2之后的dev和master所有提交点，按照提交时间合并到master

![Alt text](assert/merge-rebase/4.png)

## 直接git rebase

切换分支到需要rebase的分支，这里是dev分支

执行git rebase master，有冲突就解决冲突，解决后直接git add . 再git rebase --continue即可

发现采用rebase的方式进行分支合并，整个master分支并没有多出一个新的commit，原来dev分支上的那几次（C3，C4，C5）commit记录在rebase之后其hash值发生了变化，不在是当初在dev分支上提交的时候的hash值了，但是提交的内容被全部复制保留了，并且整个master分支的commit记录呈线性记录

![Alt text](assert/merge-rebase/5.png)


## git merge

优点：能记录真实的commit情况，包括每个分⽀的详情
缺点：由于每次merge会⾃动产⽣⼀个commit，因此在使用⼀些可视化的git工具时会看到这些自动产生的commit，这些commit对于程序员来说没有什么特别的意义，多了反而会影响阅读。

## git rebase

git rebase会合并之前的commit历史。

优点：可以得到更简洁的提交历史，去掉了merge 产生的commit
缺点：因为合并而产生的代码问题，就不容易定位，因为会重写提交历史信息

- 相同：git merge和git rebase两个命令都⽤于从⼀个分⽀获取内容并合并到当前分⽀。

- 不同点：git merge会⾃动创建⼀个新的commit，如果合并时遇到冲突的话，只需要修改后重新commit。
- 场景：
当需要保留详细的合并信息，建议使⽤git merge, 尤其是要合并到master上
当发现⾃⼰修改某个功能时提交比较频繁，并觉得过多的合并记录信息对自己来说没有必要，那么可尝试使用git rebase




# git冲突场景，如何解决？

## 1. 多个分值代码合并到一个分支时

## 2. 多个分支向同一个远端分支推送

## 快速合并

 如果当前分支的每一个commit都已经存在另一个分支里面，git就会执行一个fast-forward合并操作，这种情况下，git会直接把当前分支指向另一个分支的commit，而不会创建新的commit。

## 冲突

<<<<<<<< 和 =====之前的区域就是当前更改的内容
========= 和 >>>>>>>>>就是传入进来更改的内容

# fork clone 和 branch 的区别？

fork 就是复制了一个仓库的所有内容，如分支，tag，提交，如果想将你的修改合并到原项目中，可以通过Pull Request

clone 从远程代码仓下载到本地，形成本地代码仓库，可以对本地代码进行修改，提交，推送等操作

branch 开启新的分支