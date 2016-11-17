#Github初学练习#

>备注快速指令一览：

- git add readme.md
- git commit -m "update some code"
- git reset --hard HEAD^  head可以用小写
- 想恢复到之前最新的话，需要把head 变成对应版本的数字前几位
- git log --pretty=oneline 一行显示一次信息
- git reflog是git用来记录每一次命令的，在这里可以看到之前最新版本的数字代码
- $ git push origin master 提交到github
- $ git clone git@github.com:帐户名/aa.git
- git branch查看分支
- git branch <neme> 创建分支
- git checkout <name>切换分支
- git checkout -b <name>创建+切换分支
- git merge <name> 合并某分支到当前分支
- git branch -d <name>删除分支

- 2016.11.17

---
###第一步 安装git###
>首先配置git环境。

- 从 https://git-for-windows.github.io 下载msysgit;
- 默认安装
- 从安装路径中打开 "Git"->"Git Bash"，弹出一个命令行，说明git安装完成
- 然后声明自己的信息：
    + git config --global user.name "myname"
    + git config --global user.email "web@web.com"

>创建版本库repository

- pwd 显示当前目录 cd 打开目录 mkdir filename新建目录
- 注意如果遇到问题，有可能是目录的属性设置为只读，修改就可以。
- 初始化git目录 git init,会显示Initialized empty Git repository in <file>/.git/
- 新建一个readme.txt文件，输入第一行文字
- git add readme.txt 
- git commit -m "输入更新内容的概要，用以表述更新内容和作用"

- - - 
-  修改readme.txt
-  git status 会得到提示，修改了那些内容
-  git diff 会得到提示，上次修改了什么内容
-  修改完成后，需要git add
-  再 git commit -m"" 

- - -
###时光机回退###
>版本回退

- 版本控制系统会留有log，可以回退
- git log 显示最近修改内容
- git log --pretty=oneline 一行显示一次信息
- 例如：
- b0b74bf937a2ee026f848de18df0e7f018e2b953 恢复了最佳状态
- de68f6577d571109110e52c4d76a13699c780b67 delete some code
 
- 如果需要回退的话，有以下操作
- 首先HEAD表示当前版本，HEAD^ 表示上个版本 HEAD~100表示前100个版本
- 回退需要用到git reset
- git reset --hard HEAD^  head可以用小写
- 想恢复到之前最新的话，需要把head 变成对应版本的数字前几位
- git reflog是git用来记录每一次命令的，在这里可以看到之前最新版本的数字代码

>工作区和暂存区

- 工作区Working Directory概念是指在硬盘上创建的git文件夹
- 工作区里有一个.git隐藏目录，这个称之为git版本库
- Git版本库里存了很多东西，比较重要的是stage或者index的暂存区
- 已经git自动穿件的第一个分支master，指向master的一个指针head
- 因为我们存在唯一一个master分支，所以，git add,git commit是往master分支上提交修改
- 需要提交的文件先放在暂存区，咱后暂存区一次性提交所有修改

>管理修改

- 先add，在commit。如果先add了，继续修改，在commit，不会增加修改内容，原因是暂存区里没有修改后的add

- - -
>撤销修改

- git checkout --file可以discard changes in working directory丢弃工作区的修改

对于文件 myfile.txt

- 修改后 未add（添加到暂存区） 需要撤销修改时：
        git checkout -- myfile.txt 或 手动删除工作区修改
        工作区 ： clean  暂存区： clean
- 修改后 add了（未commit） 再次修改文件  要撤销第二次修改时：
        git checkout -- myfile.txt (将暂存区恢复到工作区)
        暂存区有第一次的修改需要commit
- 修改后 add了（未commit），需要撤销修改时：
        git reset HEAD myfile.txt (将暂存区修改删除)
        此时工作区的修改还未撤销
        git checkout -- myfile.txt (撤销工作区修改)
- 修改后 add并commit了，需要撤销修改时：
        git reset --hard HEAD^  (版本回退)

- - - 
>删除文件

- 将待删除文件 rm test.txt
- 通过git status可以看到以下两个选项
- git rm test.txt 从版本库中也删除
- git checkout -- test.txt 从版本库中恢复到最新版本

---
###远程仓库###

>远程仓库，连接github

- 在C盘user文件,打开用户名文件夹，寻找是否含有.ssh目录，该目录下有没有id_rsa,id_rsa.pub文件
- 如果没有的话，在shell中创建ssh key
- $ ssh-keygen -t rsa -C "a@a.com"
- 一路回车，默认
- 此时在.ssh目录下会有这两个文件，其中id.rsa.pub是公钥，复制其中内容
- 登录github中，打开个人设置里的ssh keys,"Add SSH Kye",在文本框里粘贴。
- 名字可以设定为你当前办公环境，用以区分。
 
- - -

>添加远程库

- 在github中新建仓库 create a new repo
- 输入相关信息，点击新建仓库
- 接下俩把本地仓库推送到github
 
```
$ git remote add origin git@github.com:github用户名/learningGithub.git
```
- 关联后使用，来第一次推送master所有分支内容
```
git push -u origin master
```
以后每次使用一下代码来同步：
```
$ git push origin master
```

###yeah~我的文字在github上出现啦~###

- - -
>从远程库克隆

- 现在github上新建仓库 aa
- 在本地使用
```
$ git clone git@github.com:帐户名/aa.git
```
- git clone的地址可以使用Clone or download 来找到
- git支持多种协议，ssh比https速度更快

---
###分支管理###

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作

>创建与合并分支

- 创建 dev分支，然后切换到dev分支

```
git checkout -b dev
```

checkout -b 表示创建并切换，相当于两条命令：
```
git branch dev
git checkout dev
```
- 用 git branch 来查看当前分支

```
git branch
*dev
master
```
- git branch命令会列出所有分支，当前分支会标一个'*'
- 此时可以正常code
- dev分支完成之后，可以切回master分支
```
git checkout master
Switched to branch 'master'
```
master分支此刻的提交点还没有变化，还需要把dev的成果合并到master分支上
```
git merge dev
```
- git merge命令用于合并，并指定分支到当前分支。此时有一个 fast-forward 此次合并是快进模式
- 此时可以删除dev分支了 git branch -d dev
- 查看git branch，只剩下master了

总结：
- git branch查看分支
- git branch <neme> 创建分支
- git checkout <name>切换分支
- git checkout -b <name>创建+切换分支
- git merge <name> 合并某分支到当前分支
- git branch -d <name>删除分支

---
我在dev分支内容里追加了这条信息。

> bug分支

正在dev分支上进行工作，bug出现，需要尽快解决问题。这时候需要修改新分支上的内容，此时的分支还不完整，也不能提交。
这时候需要用到
```
git stash
```
通过建立新分支解决问题，修复完成之后，
```
git stash list
```
查看临时存储的内容，两个方法进行恢复。

- git stash apply进行恢复，同时还需要销毁临时存储的东西，git stash drop

- git stash pop 恢复的同时，也删除内容

总结：git stash ==>  git stash pop

> 强制删除分支

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。


>引入tag，代替无意义的代号

git tag -a [tagname] -m [tag-content] [id]
git show [tagname]
git tag -d [tagname] 删除
git push origin <tagname> 推送一个tag
git push origin --tags

美化版git log
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

