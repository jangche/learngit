Git is a distributed version control system.

Git is free software distributed under the GPL.

I love you!

把一个文件放到Git仓库只需要两步：
1、用命令git add 告诉git，把文件添加到仓库
  $git add readme.txt

2、用命令git commit告诉Git，把文件提交到仓库。
  $git commit -m "wrote a readme file"

  -m后面输入的是本次提交的说明

 git add即是把文件修改添加到暂存区
 git commit 提交更改，实际上就是把暂存区的所有内容提交到当前分支。


为什么git添加文件需要add、commit两步呢？因为commit 可以一次提交很多文件。
	
小结：
	要随时掌握工作区的状态，使用git status命令
	如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

使用git log命令查看提交日志。
若显示信息太多，可用--pretty=oneline参数查看



使用git reset命令回退版本.当前版本用HEAD表示。上一个版本为HEAD^,上上个版本为HEAD^^,往上一百个版本HEAD~100

test  test  test reset

git提供了一个命令git reflog来记录你的每一次命令


小结：
	HEAD指向的版本就是当前版本，因此，git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id
	穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本
	要重返未来，用git reflog查看命令历史


每次修改，如果不用git add到暂存区，那就不会加入到commit 中。
git追踪的是修改，而不是文件。

撤销修改
git checkout --filename
意思是，将filename文件在工作区的修改全部撤销，有两种情况：
1、文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态
2、文件已经添加到暂存区后，又做了修改，现在，撤销修改就回到添加到暂存区后得状态。

该命令中--很重要，如没有，就变成了“切换到另一个分支”命令

================================================================================================================================================================================================================================================================================================================================================================================================


场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。


======================
git rm 命令用于删除一个文件。


分支管理
	创建与合并分支
	主分支叫master分支。
	$git checkout -b dev
	git checkout 命令加上-b参数表示创建并切换，相当于
	$git branch dev
	$git checkout dev
	两条命令。

	然后用git branch命令查看当前分支。git branch命令会列出所有分支，当前分支前面会表一个*号.

	git merge 命令用于合并指定分支到当前分支
	git branch -d dev可用于删除分支


小结
	查看分支:git branch
	创建分支：git branch <name>
	切换分支：git checkout <name>
	创建+切换分支：git checkout -b <name>
	合并某分支到当前非分支：git merge <name>
	删除分支:git branch -d <name>


当Git无法自动合并分支时，需要先解决冲突。解决冲突后，再提交，合并完成。
可用命令 git log --graph查看分支合并图。

分支策略：
	master分支应该是非常稳定的，仅用于发布新版本，平时不能在上面干活。

Bug分支
	Git提供了一个stash功能，可以将当前工作现场“储藏“起来，等以后恢复现场后继续工作。

	如：需要修复一个bug时，先将当前工作储藏
	$git stash
	再切换至master分支上修复
	$git checkout master
	$git checkout -b issue-101
	修复bug后合并至master分支
	$git merge 

	再返回工作区
	$git checkout dev
	恢复工作区
	$git stash apply
	删除保存的stash
	$git stash drop

	或者直接恢复的同时删除stash
	$git stash pop


bug branch test ,test test

	删除一个没有被合并过的分支，可以通过git branch -D <name>命令删除。


查看远程仓库信息
	$git remote -v


标签管理
	创建标签
	$git tag <name>
	默认标签是打在最新提交的commit上的。
	可以指定对某次commit后打标签
	$git tag <name> <commit_id>

	$git tag查看标签

	$git show <tagname>查看标签信息



使用github
	在github上，可以任意Fork开源仓库
	自己拥有Fork后得仓库的读写权限
	可以推送pull request给官方仓库来贡献代码
