#Git教程 笔记
> 教程链接：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

##创建版本库
+ git init:将当前目录变为Git管理的仓库
+ git add <filename>：把文件添加到仓库（stage中）
+ git commit -m "版本描述"：把文件按提交到仓库

##时光机穿梭
+ git status：显示仓库当前状态
+ git diff <filename>：展示文件详细修改内容
###版本回退
+ git log：显示从最近到最远的提交日志
	+ --pretty=oneline：以单行形式显示提交日志
+ git reset --hard commit_id:回退/前进到commit_id指向的版本
+ git reset --hard HEAD^:回退到上一版本
+ git log:查看提交历史
+ git reflog:查看各个版本的commit_id

###管理修改
+ git 管理的是修改，而非文件。
+ 第一次修改 -> git add -> 第二次修改 -> git commit

###撤销修改
+ git checkout -- <filename>：丢弃工作区的修改，返回最近一次add/commit时的文件状态
+ git reset HEAD <filename>：丢弃暂存区的修改

###删除文件
+ git rm <filename>：从版本库中删除文件
----------------------------------
##远程仓库

###添加远程库
1. 登陆GitHub，“Create a new repository”
2. 添加远程库：git remote add origin git@github.com:<username>/<repository name>.git
3. 推送并关联本地master分支git push -u origin master
4. git push origin master:提交master分支修改到远程库

###从远程库克隆
+ git clone git@github.com:<username>/<repository name>.git
+ GitHub支持ssh/https协议
---------------------
##分支管理

###创建和合并分支
+ `git branch <name>`:创建分支
+ `git branch`:查看分支
+ `git checkout <name>`:切换分支
+ `git checkout -b <name>`:创建+切换分支
+ `git merge <name>`:合并某分支到当前分支
+ `git branch -d <name>`:删除分支

###解决冲突
+ 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成
+ `git log --graph`:看到分支合并图

###分支管理策略
1. `git merge <name>`:`fast forward`模式合并，删除分支，分支信息被丢弃
2. `git merge --no-ff`:普通模式合并，合并后历史有分支，可通过`git log --graph`看到分支合并记录

###Bug分支
+ `git stash`:储存当前工作现场
+ `git stash list`:列出所有stash
+ `git stash apply`:恢复最近一次储存的stash
+ `git stash drop`:删除最近一次储存的stash
+ `git stash pop`:恢复+删除最近一次stash
+ `git stash stash@{num}`:恢复指定stash

###feature分支
+ `git branch -D <name>`:强行删除没有被合并的分支
------------------
