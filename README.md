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

git reset --soft [commit_id] :

--soft 模式 会在重置 HEAD 和 branch 的指针位置 的同时，保留工作区和暂存区中的内容，并把重置 HEAD 指针位置 所带来的新的差异放进暂存区（将已 commit 到仓库的内容放到暂存区）

git reset 不带参数则默认使用--mixed模式。
git reset [commit_id] : 只保留工作区内容，并将已 commit 到仓库的内容和暂存区放到工作区
--mixed模式 会在重置 HEAD 和 branch 的指针位置 的同时，会保留工作目录，并将已 commit 到仓库的内容和暂存区放到工作区，并且清空暂存区。
```



