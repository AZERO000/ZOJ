## git核心原理

![git核心原理](https://raw.githubusercontent.com/AZERO000/Upload-picture/master/git%E6%A0%B8%E5%BF%83%E5%8E%9F%E7%90%86.jpg)

## git常见命令

* 配置基本用户信息

  >git config --global user.name <用户名>
  >
  >git config --global user.emial <你的邮箱地址>
  >
  >git config --global http.proxy socks5://127.0.0.1:7890  （配置自己的代理地址和端口）
  
* 初始化一个仓库

  > git init

* 从远程服务器克隆一个仓库

  > git clone <远程仓库的url>

* 显示当前工作目录下的文件状态

  > git status

* 将指定文件Stage（标记为将要被提交的文件）

  > git add <文件路径>

* 将指定文件Unstage（取消标记为要提交的文件）

  > git reset <文件路径>

* 创建一个提交并提供信息

  > git commit -m "提交信息"

* 显示提交历史

  > git log

* 向远程仓库推送

  > git push

* 从远程仓库拉取

  > git pull

* 从远程仓库拉到本地版本库

  > git fetch

* 隐藏文件

  > touch .gitignore  （创建一个Git Ignore源文件，在里边添加想要隐藏文件的路径即可）

* 查看分支

  > git branch

* 创建分支

  > gt branch <分支名>

* 切换分支

  > git checkout <分支名>
  >
  > git checkout -b <分支名> （创建并切换分支）

* 删除分支

  > git branch -d <分支名>

* 合并分支（把选定的分支合并到当前所处的分支上）

  > git merge <分支名>

* 查看与本地仓库有联系的远程仓库

  > git remote -v
