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
-  git status

- - -

sdfadf
