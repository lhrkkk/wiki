
git使用简要
git 使用方法简介:

删除一个分支

	git branch -d <branch name>


### .gitignore的注意点
.gitignore文件只是ignore没有被staged(cached)文件，对于已经被staged文件，加入ignore文件时一定要从staged移除。下面是来自github的一段话：
If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal: $ git rm --cached
因此，要想用gitignore忽略文件，必须先把它们从staged中移除：commit你已有的改变，保存当前的工作。git rm --cached file/path/to/be/ignored。git add .git commit -m "fixed untracked files"
