# git 基础命令

## 使用前配置

```shell
#配置用户信息
git config --global user.name="Janssen"
git config --global user.email="xxxxx@qq.com"
#配置编辑器
git config --global core.editor vim
#查看配置
git config --list
git config <key>
#获取帮助
git help <verb>
git <verb> --help
```

## 开始使用git

### 仓库创建

```shell
#仓库初始化,在项目路径下执行
git init
#文件跟踪
git add *.c
git add <file>
#提交
git commit -m 'comment'
#克隆 clone
git clone [url]
```

### 仓库文件状态

* untracked
* unmodified
* modified
* staged

```shell
#文件状态查看
git status
#文件跟踪、缓存
git add README
```

### 忽略文件

> 对于项目中不希望跟踪的文件，创建.gitignore文件列出忽略文件

```shell
 #例如忽略log文件
$cat .gitignore
 *.log
```

### 提交

```shell
#提交
git commit
#提交，带说明
git commit -m 'comment'
#跳过缓存，直接提交
git commit -a -m 'comment'
```

### 移除、移动文件

```shell
git rm filename
git rm --chaced filename
git mv filefrom fileto
```

### 查看提交历史

```shell
git log
#查看最近两次
git log -p 2
#格式化
git log --pretty=oneline
git log --pretty=format:"%h - %an, %ar : %s"
git log --graph

#仅显示添加或移除了某个关键字的提交
git log -S <keyword>
#其他输出选项
--author
--grep
--before
--after 等等
```

### 撤销操作

>重新提交  
如下命令第二次提交取代第一次提交

```shell
git commit -m 'amend test'
git add *.md
git commit --amend
```

>取消暂存的文件  

`git reset HEAD <file>`

>取消对文件的修改  

`git checkout -- <file>`

### 远程仓库的使用

* 查看已配置远程仓库 `git remote -v`
* 克隆远程仓库 `git clone [url]`
* 添加远程仓库 `git remote add <shortname> <url>`
* 抓取远程仓库 `git fetch [remote-name]`
* 拉取远程仓库 `git pull [remote-name]`
* 推送到远程仓库 `git push [remote-name] [brantch-name]`
* 查看远程仓库 `git remote show [remote-name]`
* 重命名远程仓库 `git remote rename [old-name] [new-name]`
* 删除远程仓库 `git remote rm [remote-name]`

>`git fetch` 是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。  
而 `git pull` 则是将远程主机的最新内容拉下来后直接合并，即：`git pull = git fetch + git merge`，这样可能会产生冲突，需要手动解决

### 标签

>查看标签

* 列出标签 `git tag`
* 列出指定的标签 `git tag -l 'v1.2.3*'`

>添加标签  
标签分为轻量标签 `lightweight` 和附注标签 `annotated`

* 附注标签 `git tag -a v1.4 -m 'my version 1.4'`
* 查看标签信息 `git show v1.4`
* 轻量标签 `git tag v1.4-lw`
* 补打标签 `git tag -a v1.2 9fceb02` 9fceb02 是提交的部分校验和， `git log`获取
* 共享标签 `git push origin v1.4` 或 `git push origion --tags` 更新全部标签到远程仓库

### Git 别名

```shell
git config --global alias.co checkout
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
```

## Git分支

### 分支新建与合并

`git branch test` 创建分支 `test`  
`git checkout -b iss53` 新建并切换到分支 `iss53`  
`git checkout master` 切回 `master` 分支  
`git merge hotfix` 合并 `hotfix` 到 `master` 分支

>合并遇到冲突，需要手动解决后缓存提交

`git branch -d hotfix` 删除 `hotfix` 分支

### 分支管理

`git branch`  
`git branch [-v|-vv]`  
`git branch [--merged|--no-merged]` 查看已合并|未合并分支  
`git branch -d hotfix` 删除 `hotfix` 分支

### 远程分支

查看远程分支 `git ls-remote`  `git remote show origin`  
新建远程分支 `git push branch origin/branch`  
跟踪远程分支 `git checkout -b [branch] [remotename]/[branch]`  
 `git checkout --track origin/serverfix`  
拉取远程分支 `git fetch`  
删除远程分支 `git push origin --delete newtest`

### 变基

```shell
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
$ git checkout master
$ git merge experiment
 ```

`git rebase --onto master server client`  
> “取出 client 分支，找出处于 client 分支和 server 分支的共同祖先之后
的修改，然后把它们在 master 分支上重演一遍”