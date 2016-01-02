Git学习历程及心得

一.git安装:
	在网上找到git的安装包下载安装完成后，在开始菜单里面找到
	"Git"->"GitBash"，打开蹦出一个类似于命令行的窗口，表示
	git安装成功。
	安装完成后，因为git是分布式版本控制系统，所以必须标明
	name和email来区分:
	$ git config --global user.name "Your name"
	$ git config --global user.email "Your email"

二.创建版本库
	版本库又名仓库，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，git都能追踪，以便追踪历史和还原。

	<第一步:创建版本库>
		创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录:
		$ mkdir learngit
		$ cd learngit
		$ pwd
		/Users/ZJ/learngit

		pwd命令用于显示当前目录，在我的电脑上目录是：
		/c/Users/ZJ/learngit

	<第二步:git init命令把目录变成Git可管理的仓库>
		$ git init
		Initialized empty Git repository in c:/Users/ZJ/learngit/.git/

		这样一个git仓库就建好了

	<第三步:把文件添加到版本库>
		(1).先编写一个readme.txt的文件，文件中随便写一点内容，
		一定要放在learngit目录下(子目录也行)。
		(2).然后用git add命令告诉Git，把文件添加到仓库:
		$ git add readme.txt
		(3).用命令git commit告诉Git，把文件提交到仓库:
		$ git commit -m "wrote a readme file"
		然后会自动蹦出:
		[master (root-commit) 2eebe95] wrote a readme file
 		1 file changed, 2 insertions(+)
 		create mode 100644 readme.txt

 		//说明:commit命令，-m后面输入的是本次提交的说明，
 		可以输入任何内容，相当于备注(注释)
 		git commit命令成功后会告诉你，一个文件被改动，插入了*行的内容

三.正式使用Git版本控制系统
(1).在版本库中添加修改文件

	我们修改了readme.txt里面的内容：
	现在运行git bash，输入命令行git status查看结果:
	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#    modified:   readme.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")
	表明readme.txt文件被修改过，但还没有提交修改

	如果我们需要看看这个文件具体把些地方被修改过，我们可以使用git diff命令：
	$ git diff readme.txt 
	diff --git a/readme.txt b/readme.txt
	index 46d49bf..9247db6 100644
	--- a/readme.txt
	+++ b/readme.txt
	@@ -1,2 +1,2 @@
	-Git is a version control system.
	+Git is a distributed version control system.
	 Git is free software.
	下面我们就可以放心的提交了：
	$ git add readme.txt
	没有提示，表示添加成功，然后我们来提交：
	$ git commit -m "我修改了！"
	提示：
	[master 0141bc2] 我修改了！
	1 file changed, 71 insertions(+), 2 deletions(-)
 	rewrite readme.txt (100%)
 	完成后我们再来查看工作区状态:
 	$ git status
 	On branch master
	nothing to commit, working directory clean

(2).版本回退
	在项目开发过程中，可能会有上百次的修改提交，每commit一次就可以“保存一个快照”，一旦你把文件弄乱了或者是误删了文件，还可以从最近的一次commit恢复，然后继续工作。但是，项目开发中可能会动辄修改上百甚至是上千行代码，我们无法记住我们究竟修改了哪些，所以Git中有一个命令告诉我们历史记录，就是git log：
	$ git log
	commit cb761873d4545df6795b3112671e95ec6fc69462
	Author: GiantDwarf <zhujian1995@outlook.com>
	Date:   Tue Dec 29 18:00:40 2015 +0800

    最近一次修改！

	commit 0141bc280ba4766bdc9f756cfd258acdfe2f2c16
	Author: GiantDwarf <zhujian1995@outlook.com>
	Date:   Tue Dec 29 17:50:16 2015 +0800

    我修改了！

	commit 2eebe95265d27765d8501a3a83f3b9c938aba26e
	Author: GiantDwarf <zhujian1995@outlook.com>
	Date:   Tue Dec 29 16:58:11 2015 +0800

    wrote a readme file

    我们可以看到三次commit记录，如果嫌输出信息太多，我们可以试着加上--pretty=oneline参数

    sdhfuashdu 