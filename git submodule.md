

git submodule 是 git 的模块工具. 本文介绍命令都是 git 标准命令, gy 的包装请参见[gy]().

## git submodule 的使用
### 克隆带有 submodule 的项目

	git clone --recursive https://git.ustclug.org/lhrkkk/labkit

`--recursive`会递归的获取并更新 submodule, 或者

	git clone https://git.ustclug.org/lhrkkk/labkit
	git submodule init
	git submodule update

会建立 submodule 目录, 并获取 submodule.

### 主项目和子项目的关系
submodule 是一个 git 子项目. 每个 submodule 都是一个独立的 git 项目. submodule 只是主项目对子项目的引用关系.

包含 submodule 的主项目, 不包含子项目的文件, 只记录 submodule 的标号. 

`git submodule` 命令会列出**当前**的submodule的commit标号状态. 因为 submudole 可能已经有修改, 当前的标号和主项目记录的 submodule 标号可能不一样.

主项目 git commit; git push 的时候, 会更新主项目的记录的 submodule 标号到当前状态. 不会push子项目. 


### 更新子项目到主项目记录的版本: git submodule update
主项目更新后, 如果其依赖的 submodule 版本更新了, 这样在主项目用`git pull`更新的时候, 并不会主动更新 submodule 目录的文件. 请运行`git status`命令查看当前分支状态, 如果发现要更新 submodule, 则需要运行

	git submodule update

来更新子项目

update 会在使 submodule 获取主项目引用的版本到新的**游离分支**(临时分支)上. 如果当前submodule 处在游离分支, 会丢失掉. 所以在 update 之前, 要想保存本地的修改, 必须
提前 checkout 到主分支上, 或用`git branch`命令基于当前状态新建一个分支. 下一节中也有详细说明. 

### 修改submodule
git submodule update 命令, 会获取主项目中记录的 submodule 版本.

默认 git submodule update 并不会将 submodule 切到任何 branch，所以，默认下 submodule 的 HEAD 是处于游离状态的 (‘detached HEAD’ state)。所以在修改前，记得一定要用 git checkout master 将当前的 submodule 分支切换到 master，然后才能做修改和提交。

	git submodule update
	# cd 进 submodule 目录, 之后
	git checkout master  

修改之后, 想要提交对子项目的修改, 则正常运行`git commit`, `git push`. 

注意, update 只是更新子项目到主项目记录的版本, 并且是游离分支. 如果 submodule已经在master 分支上面工作, 想要直接更新到 submodule 到最新版本, 而不是主项目记录的版本, 可以在子项目目录直接运行 

	git pull
  
如果你不慎忘记切换到 master 分支，又做了提交，可以用 cherry-pick 命令挽救。具体做法如下： 
 
- 用 `git checkout master` 将 HEAD 从游离状态切换到 master 分支 , 这时候，git 会报 Warning 说有一个提交没有在 branch 上，记住这个提交的 change-id（假如 change-id 为 aaaa)
- 用 `git cherry-pick aaaa` 来将刚刚的提交作用在 master 分支上
- 用 `git push` 将更新提交到远程版本库中

### 最后一点说明: 主项目和子项目的 push
主项目引用的 submodule 必须是一个公共仓库, 引用的是 submodule 的指定版本在公共仓库里的地址. 

如果你修改了 submodule, 并仅仅在本地 commit 了, 你在 push 主项目的时候会更新主项目中 submudule 的标号, 如果 submodule 没有 push 到公共仓库, 主项目引用就会不存在, 所以如果要 push 主项目, 则必须保证主项目引用的子项目都要是 push 到公共仓库上的. 

如果你的 submudole 已经编写完成, 通过测试, 那么就先 push submodule, 再 push 主项目. 

如果你的 submodule 还没修改完成, 但是想要 push 主项目的一些修改, 可以先保证 submodule 在一个普通分支上, 然后用`git submodule update`先讲本地目录切换到主项目记录的稳定submodule 版本, 然后 push 主项目. 之后记得主动进入 submodule 目录再把分支切回来. 

### 对每一个 submodule 进行同样的操作: foreach 

直接更新每个 submodule 到最新版本. 
	git submodule foreach  git checkout master
	git submodule foreach  git pull

如果子项目中还包含子项目, 则

	git submodule foreach --recursive git checkout master
	git submodule foreach --recursive git pull


如果是想要切换所有的子项目到主项目引用的版本

	git submodule foreach --recursive git submodule update 

或

	git submodule foreach --recursive git submodule init 
	git submodule foreach --recursive git submodule update 


## labkit 的 submodule 讨论
labkit 的 submodule 只是用于管理官方支持的 packages 和它们的版本, 而在使用的过程中, 你可以在 package 目录使用自己的版本, 它们都是是独立的项目, 都可以修改和提交. 另外, 你还可以在`$HOME/.labkit/packages/`目录下, 使用自己的包.

除了方便管理和添加包之外, labkit 使用 submodule 是为了使得包的编辑和修改以及版本的变化不会影响到 labkit 发布版本的稳定, 并且不会影响到 labkit 的代码库. 

另外, 除了包是 submodule 之外, wiki, 网站等, 也都是以 submodule 的形式存在在 labkit 中的. 

## 结论
虽然 submodule 的理解和使用有一定复杂性, 请理解 submodule 的使用, 但是实际用的时候可以不用太操心 submodule. 记住 submodule 只是作为 labkit 官方发布的包的版本管理用, 各个包自己本身是独立的. 


