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

### 撤销提交

```shell
git commit --amend
```
