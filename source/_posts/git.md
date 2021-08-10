---
title: git的学习笔记
author: 小燕子
date: 2021-06-25 20:14:10
tags: Git
categories: 学习笔记
readmore: true
---
参考链接：[git学习笔记](https://www.yuque.com/yunyoujun/notes/git-learn-note)  进行补充完整

# 初始化仓库
`git init`

# 本地分支
## 创建分支
`git branch [分支名]`
## 删除本地分支
`git branch -d [分支名]`

`git branch -D [分支名]` &nbsp;#强行删除
## 修改本地分支名
`git branch -m [旧分支名] [新分支名]`
## 查看分支
`git branch`  &nbsp;#查看当前分支（* 表示当前所在分支）

`git branch -a`    &nbsp;#查看本地分支 + 远程分支
## 切换分支
`git checkout [分支名]`（旧版本）

`git switch  [分支名]` （新版本）

`git checkout -` &nbsp;#切换到上一分支
## 创建+切换分支
`git checkout -b [新分支名]`（旧版本）

`git switch -c [新分支名]`（新版本）   
# 操作工作区
## 提交代码
添加文件到git仓库，分两步：
`git add <file>` &nbsp;#可反复多次使用，添加多个文件（暂存）

`git add .` 	 &nbsp;#比较常用

`git commit -m <message>` &nbsp;#提交信息到本地分支
## 修改已经提交的描述
`git rebase -i` &nbsp;#查看修改

`git commit --amend` &nbsp;#修改已经提交的描述（前提是未推送到远程）
> 直接键入`:i`，此时进入了输入模式
  可用键盘上下键转到描述所在的那一行，然后进行修改
  修改完成后，按下 `Esc键` 退出编辑模式，在键入 `:wq` 回车退出并保存修改
  再推送到远程
参考链接：[git 修改已提交的内容](https://blog.csdn.net/sodaslay/article/details/72948722)

## 代码回滚

回退版本，HEAD 表示当前版本  
`git reset --hard HEAD^`

`git reset --hard <commit id>` 

`git reset HEAD^ --soft`

> 说明：上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^`，当然往上100个版本写100个比较容易数不过来，所以写成 `HEAD~100`
`commit id` 为每次提交系统自动生成的一串哈希值，可通过此值回退到指定版本
`--hard` 会使当前源码回到上一次的状态
`--soft` 保留工作现场更改，只回退 commit 信息
清除缓存区中准备提交的内容，只保留修改的状态，可不加参数，或使用 `--mixed`。
 
## 合并指定分支到当前分支
`git merge [指定分支名]`

`git merge --no-ff -m "commit描述信息" [指定分支名]` &nbsp;#强制禁用Fast forward模式，明确地记录本次分支的合并
## 合并部分代码到分支
`git cherry-pick <commit id>`

## 清理缓存
`git rm -r --cached <path>` &nbsp;#清空文件夹的本地缓存 
>`-r` 递归
  `-f` 强制
## 撤销修改
`git checkout -- <file>`
> 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令
`git checkout -- <file>`
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第		一步用命令 `git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提		是没有推送到远程库。
## 删除文件
`git rm <file>`
# 拉取代码
`git clone [git仓库地址][本地目录，可省略]`  &nbsp;#从远程库克隆至本地目录
# 远程分支
## 创建分支
`git checkout -b [新分支名] origin/[远程分支名]` &nbsp;#创建本地和远程对应的分支，切换至该分支，同时同步远程分支至该分支
## 删除分支
`git push origin :[分支名]` &nbsp;#删除远程分支，冒号前有空格
## 建立关联
`git branch --set-upstream [分支名] origin/[分支名]` &nbsp;#建立本地分支和远程分支的关联
## 推送代码
`git push origin [分支名]` &nbsp;#推送代码到远程分支

`git push -u origin master -f` &nbsp;#强制推送

> 推送至远程仓库 master分支下, `-u` 参数可以在推送的同时，将 origin 仓库的 master 分支设置为本地仓库的当前分支的的upstream（上游）。添加这个参数，将来运行`git pull`命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从 origin 的master分支中获取内容

## 拉取代码
`git pull origin [分支名]` &nbsp;#从远程抓取分支到本地

`git fetch`  &nbsp;#将远程分支信息获取到本地，但是不合并代码
# 远程仓库
## 查看远程库的信息
`git remote`

`git remote -v`  	 &nbsp;#显示更详细的信息
## 增加远程仓库地址
`git remote add origin git@github.com:xxx/xxx.git`

`git remote add origin https://github.com/xxx/xxx` &nbsp;#origin 为远程仓库命名
## 删除远程库
`git remote rm <远程库名>` &nbsp;#远程库名默认为 origin
## 关联多个远程仓库
`git remote add github git@github.com:xxx/xxx.git`

`git remote add gitee git@github.com:xxx/xxx.git`

`git remote add coding git@github.com:xxx/xxx.git`
## git仓库操作
### 仓库新增子模块
* 先添加，再推送
  `git rm --cached 【子模块目录】`
  `git submodule add【子模块仓库地址】【目录，可省略】`
  `git status`
  `git commit -am “...”`
  `git push --recurse-submodules=check`

### 仓库克隆（带有子模块）
* 【方法一】：
  `git clone【父仓库地址】【目录，可省略】`
  `git submodule init`
  `git submodule update`

* 【方法二】：
`git clone --recursive【父仓库地址】【目录，可省略】`

### 仓库更新（带有子模块更新）
* 【父仓库更新】：
`git submodule update --remote --merge`
`git pull`
* 【子模块更新】：
`cd 【子模块目录】`
`git fetch`
`git merge origin/master`

### 仓库推送（带有子模块改动）
* 先检查，再推送
`git push --recurse-submodules=check` &nbsp;# 检查子模块是否推送，否则此命令会失败
`git push --recurse-submodules=on-demand` &nbsp;# 检查到子模块没有推送，即自动推送，再推送主模块

# 日志
## 查看日志 
`git log`			 &nbsp;#查看提交日志，按q退出

`git log --pretty=oneline` &nbsp;#只显示提交信息的第一行

`git log <file>`		 &nbsp;#用于查看指定的目录、文件的日志

`git log -p` 		 &nbsp;#查看提交所带来的改动

`git log -p <file>`	 &nbsp;#查看指定文件的改动

`git log --graph`	 &nbsp;#查看分支合并图

`git log --graph --pretty=oneline --abbrev-commit`
## 查看操作日志
 `git reflog` 	 &nbsp;#可以找到所有的 commit id
# 查看工作区状态
`git status`
# 对比工作树
`git diff HEAD -- <file>` 	 &nbsp;#查看某个文件与版本库的区别

`git diff` 			 &nbsp;#可以查看工作树，暂存区，最新提交之间的差别

`git diff HEAD` 		 &nbsp;#查看工作树与最新提交的差别

`git diff [branchA] [branchB] >> xx.txt`  &nbsp;#比较两个分支不同，输出到某文本

`http://github.com/用户名/仓库名/分支1...分支2` &nbsp;#在gitHub上面查看两个分支之间的差别

`http://github.com/用户名/仓库名/master@{7.day.ago}...master` &nbsp;#查看master分支在最近七天内的差别（同样，day，week，month，year都是可以哒）

`http://github.com/用户名/仓库名/master@{xxxx-xx-xx}...master`  &nbsp;#查看与指定日期之间的差别（xxxx-xx-xx代表年月日）
# 标签
`git tag <tagname>`  &nbsp;#新建标签

`git tag  <tagname> <commit id>` &nbsp;#指定标签信息

`git tag -a <tagname> -m "blablabla..." <commit id>` &nbsp;#创建带有说明的标签，用-a指定标签名，-m指定说明文字

`git tag` 		 &nbsp;#查看所有标签

`git show <tagname>`  	 &nbsp;#查看标签的信息

`git push origin <tagname>`  &nbsp;#推送某个标签到远程

`git push origin --tags` &nbsp;#推送全部本地标签

`git tag -d <tagname>` &nbsp;#删除本地标签

`git push origin :refs/tags/<tagname>` &nbsp;#删除远程标签，: 前面有一个空格

# 暂存工作现场
## 保存工作现场
`git stash`
## 查看保存工作现场的信息列表
`git stash list`
## 释放工作现场
方式一：
`git stash apply` &nbsp;#将修改从缓存中释放出来

`git stash drop` &nbsp;#删除stash内容

方式二：
`git stash pop`

# git 代理
## 设置代理
`git config --global http.proxy http://127.0.0.1:1087`

`git config --global https.proxy https://127.0.0.1:1087 ` 
## 取消代理
`git config --global--unset http.proxy` 

`git config --global--unset https.proxy`

# 配置SSH-key
检测是否连接
`git remote add origin [git仓库地址]`
`ssh git@[IP或域名]`
<details>
  <summary>配置ssh-key</summary>

* 生成key  
`ssh-keygen -t rsa -C "个人邮箱"`   
* 添加ssh key 到github上
　　首先登陆github,点击右上角的“▼”→Settings→SSH kyes→Add SSH key。
　　然后在打开 c:/Users/xxxx_000/.ssh 里面的id_rsa.pub文件，全选复制公钥内容
　　也可以在git bush中的命令行输入 `cat ~/.ssh/id_rsa.pub` ，将得到公钥
　　Title自定义，将公钥粘贴到gitHub中Add an SSH key的key输入框，最后“Add Key“
* 配置账户
`git config --global user.name "your_username"` 	 &nbsp;#设置用户名
`git config --global user.email "your_Email"` &nbsp;#设置邮箱地址(建议用注册giuhub的邮箱)
`git config --global color.ui true` 	 &nbsp;#让git显示颜色，会让命令输出看起来更醒目

</details>

# FAQ（常见问题）