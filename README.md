 
## GIT常用命令整理

@(基础)

### 概念
工作目录--add--》暂存区--commit--》本地repository--push--》远端repository

### 参考文档

[GIT中文文档](https://git-scm.com/book/zh/v2)

[GIT简明指南](http://www.runoob.com/manual/git-guide/)


### 基础操作
```powershell
git clone ... #克隆git repository到本地
git config --global user.name "张三"
git config --global user.email "zhangsan@asd.com"
git add . #添加文件到缓存区(待commit)
git commit -m "提交说明" #将缓存区文件加到git repository
git push [remote-name] [branch-name] #推送master分支的commit内容到remote服务器，如:
git push origin master

git pull (<远程主机名> <远程分支名>:<本地分支名>)# 从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支
git fetch (<远程主机名> <远程分支名>:<本地分支名>)# 从远端仓库中获得数据（不会自动合并或修改你当前的工作，需手动merge）

```
### Reset操作
```powershell
git reset --hard origin/master #回退到某一版本origin/master
git reset --hard commitID #回退到某一commit状态，commitID可以使用git log 看到，很长的hash字符串
git rest HEAD file #file路径(支持正则),取消文件的暂存(add) 
git checkout -- file #file路径(支持正则),放弃对文件的修改，类似revert(danger:你对那个文件做的任何修改都会消失 - 你只是拷贝了另一个文件来覆盖它)  
```
### 查看当前更改
```powershell
git status #查看是否有更改， -s查看简要
git diff #查看更改，只显示尚未暂存（add）的改动
git diff <source_branch> <target_branch> #比较两个分支(target_branch默认为当前分支) 
git diff --cached <source_branch> <target_branch> # (同--staged)查看已暂存(add)的将要添加到下次提交里的内容
```

### 日志相关
```powershell
git show #默认查看上一次commit内容
git log #查看commit记录，-p显示详细diff，-2显示最近两条，--state显示提交文件详情，--shortstate显示增删改条数，--pretty=online在一行显示
git log --oneline --decorate #查看各个分支当前所指的对象
git log --pretty=format:"%an %ad %cn %cd %s"查看提交记录，只显示作者、修改日期、提交者、提交日期和提交说明
```

### 分支操作:

```powershell
git branch #查看当前本地所有分支， --merged查看已合并到当前分支的分支，--no-merged查看未合并到当前分支的分支
git branch -v #查看当前所有分支及最后一次提交记录
git branch -r #查看远端分支
git branch a #创建a分支
git checkout a #切换到master分支
git checkout -b a #创建aaa并切换到aaa 
git branch -d aaa #删除aaa分支，如有未处理的更改将会失败
git branch -D aaa #强制删除aaa分支
git push origin mybranch #推送分支到远端(可供协同工作)
```

### Remot操作
```powershell
git remote #查看远端名称(默认为orign)
git remote -v #查看remote名及对应url
git remote add test https://url.com #添加一个远端仓库,test为仓库名，后面为仓库地址
git remote show [remote-name]  #显示远端仓库详情
git remote rename oldName newName #重命名
git remote rm  name #移除远端仓库
```

### 变基操作
**只对尚未推送或分享给别人的本地修改执行变基操作清理历史，从不对已推送至别处的提交执行变基操作，这样，你才能享受到两种方式带来的便利**
```powershell
#将 targetBranch的基改为baseBranch(会merge修改)，若baseBranch为 targetBranch的祖先，则无变化，targetBranch默认为当前分支
git rebase baseBranch targetBranch
```
### 标签操作
```powershell
git tag #查看已有标签
git tag v1.1 #打标签
git show v1.1 #查看标签详情
```

### Q&A
####  fetch和pull区别
[详解git fetch与git pull的区别](https://blog.csdn.net/riddle1981/article/details/74938111)
git fetch 命令会将远端数据拉取到你的本地仓库，它并不会自动合并。
基本情况下git pull = git fetch + git merge
如果需要有选择的合并git fetch是更好的选择。效果相同时git pull将更为快捷。


