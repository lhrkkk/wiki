
git使用简要
git 使用方法简介:

删除一个分支

	git branch -d <branch name>


### .gitignore的注意点
.gitignore文件只是ignore没有被staged(cached)文件，对于已经被staged文件，加入ignore文件时一定要从staged移除。下面是来自github的一段话：
If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal: $ git rm --cached
因此，要想用gitignore忽略文件，必须先把它们从staged中移除：commit你已有的改变，保存当前的工作。git rm --cached file/path/to/be/ignored。git add .git commit -m "fixed untracked files"

commit, push, pull, 

branch

###  观察区别 diff:
	# 显示工作目录和索引的不同
	$ git diff
	
	# 显示索引和最近一次提交的不同
	$ git diff --cached
	
	# 显示工作目录和最近一次提交的不同
	$ git diff HEAD
	
	git diff xxx..xxx
	

### 重置head指针 reset (谨慎使用)
将当前的头指针复位到一个特定的状态。这样可以使你撤销merge、pull、commits、add等 这是个很强大的命令，但是在使用时一定要清楚其所产生的后果

reset: 用来移动HEAD, 查看以前的提交用checkout, 要建立分支用checkout -b

	# 使 staging 区域恢复到上次提交时的状态，不改变现在的工作目录
	$ git reset
	
	# 使 staging 区域恢复到上次提交时的状态，覆盖现在的工作目录
	$ git reset --hard
	
	# 将当前分支恢复到某次提交，不改变现在的工作目录
	# 在工作目录中所有的改变仍然存在
	$ git reset 31f2bb1
	
	# 将当前分支恢复到某次提交，覆盖现在的工作目录
	# 并且删除所有未提交的改变和指定提交之后的所有提交
	$ git reset --hard 31f2bb1

撤销reset: git reflog 查看操作历史，找到之前 HEAD 的 hash 值，然后 git reset --hard 到那个 hash 即可。



### 合并 merge/rebase
把一个分支中的修改整合到另一个分支的办法有两种：merge 和 rebase
rebase (谨慎使用)
将一个分支上所有的提交历史都应用到另一个分支上 不要在一个已经公开的远端分支上使用rebase.
	# 将experimentBranch应用到master上面
	# git rebase <basebranch> <topicbranch>
	$ git rebase master experimentBranch
	
### 移除 rm
和add相反，从工作空间中去掉某个文件
	# 移除 HelloWorld.c
	$ git rm HelloWorld.c
	
	# 移除子目录中的文件
	$ git rm /pather/to/the/file/HelloWorld.c

### 查找 grep
	可以在版本库中快速查找
	可选配置： git config 相当于直接改~/.gitconfig文件
	# 感谢Travis Jeffery提供的以下用法：
	# 在搜索结果中显示行号
	$ git config --global grep.lineNumber true
	
	# 是搜索结果可读性更好
	$ git config --global alias.g "grep --break --heading --line-number"
	# 在所有的java中查找variableName
	$ git grep 'variableName' -- '*.java'
	
	# 搜索包含 "arrayListName" 和, "add" 或 "remove" 的所有行
	$ git grep -e 'arrayListName' --and \( -e add -e remove \) 
	
