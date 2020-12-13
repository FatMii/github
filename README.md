# github

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目

## 集中式 与 分布式

![avatar](https://www.runoob.com/wp-content/uploads/2015/02/0D32F290-80B0-4EA4-9836-CA58E22569B3.jpg)


## git三大区

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