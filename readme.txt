Git is a distributed version control system.
Git is free software.


把一个文件放到Git仓库只需要两步：
1、用命令git add 告诉git，把文件添加到仓库
  $git add readme.txt

2、用命令git commit告诉Git，把文件提交到仓库。
  $git commit -m "wrote a readme file"

  -m后面输入的是本次提交的说明


为什么git添加文件需要add、commit两步呢？因为commit 可以一次提交很多文件。
	