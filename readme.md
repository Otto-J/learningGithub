Github初学练习

###第一步 安装git###
####首先配置github环境。####
- 从 https://git-for-windows.github.io 下载msysgit;
- 默认安装
- 从安装路径中打开 "Git"->"Git Bash"，弹出一个命令行，说明git安装完成
- 然后声明自己的信息：
    + git config --global user.name "myname"
    + git config --global user.email "web@web.com"

####创建版本库####
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
####时光机回退####
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

- - -
####工作区和暂存区####
- 工作区Working Directory概念是指在硬盘上创建的git文件夹
- 工作区里有一个.git隐藏目录，这个称之为git版本库
- Git版本库里存了很多东西，比较重要的是stage或者index的暂存区
- 已经git自动穿件的第一个分支master，指向master的一个指针head
- 因为我们存在唯一一个master分支，所以，git add,git commit是往master分支上提交修改
- 需要提交的文件先放在暂存区，咱后暂存区一次性提交所有修改

####管理修改####
- 先add，在commit。如果先add了，继续修改，在commit，不会增加修改内容，原因是暂存区里没有修改后的add

- - -
####撤销修改####
- git checkout --file可以discard changes in working directory丢弃工作区的修改

对于文件 myfile.txt

① 修改后 未add（添加到暂存区） 需要撤销修改时：
        git checkout -- myfile.txt 或 手动删除工作区修改
        工作区 ： clean  暂存区： clean
② 修改后 add了（未commit） 再次修改文件  要撤销第二次修改时：
        git checkout -- myfile.txt (将暂存区恢复到工作区)
        暂存区有第一次的修改需要commit
③ 修改后 add了（未commit），需要撤销修改时：
        git reset HEAD myfile.txt (将暂存区修改删除)
        此时工作区的修改还未撤销
        git checkout -- myfile.txt (撤销工作区修改)
④ 修改后 add并commit了，需要撤销修改时：
        git reset --hard HEAD^  (版本回退)

- - - 

