###git pull push没有指定branch报错的解决方法 2015/07/17

>[原文](https://www.netroby.com/view.php?id=3203)感谢提供答案。

###git执行git push或git pull的操作时候，经常看到下面的英文提示：

	You asked me to pull without telling me which branch 
	you want to merge with,and 'branch.dev.merge'in you configuration 
	file does not tell me,either.Please specify which branch you want 
	to use on the command line an try 
	again(e.g.'git pull <repository><refspec>').
	See git-pull(1) for details.

	if you often merge with the same branch,
	you may want to use something like the 
	following in your configuration file.

	[branch "dev"]
	remote=<nickname>
	merge=<remote-ref>
	[remote"<nickname>"]
	url=<url>
	fetch=<refspec>

###在高级版的git下面，也许会看到这样的提示：
	There is no trackling information for the current branch.
	Please specify which branch you want to merge with.
	See git-pull(1)for details
	git pull<remote><branch>
	if you wish to set tracking information for this branch 
	you can do so with
	git branch --set-upstream master origin/<branch>

###看到第二个提示，我们现在知道了一种解决方案。也就是指定当前工作目录工作分支，跟远程的仓库，分支之间的链接关系。

>比如我们设置master对应远程仓库的master分支

	git branch --set-upstream master origin/master

>这样我们每次想push或者pull的时候，只需要输入git push或者git pull即可。
在此之前，我们必须指定想要push或者pull的远程分支。

	git push origin master
	git pull origin master