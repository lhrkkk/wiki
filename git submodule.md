

git submodule 是 git 的模块工具



### 修改submodule 
git submodule foreach git checkout master   //如果不切换到master分支.  
修改之后, git commit,  git push.  



### 主项目
主项目, git commit. git push. 只是push标号, 但是并不会push子项目.  

主项目标号和submodule真实目录是不同步的. git submodule, 以及commit的时候, commit的是真实子项目. 
要git add 

主项目标号commit 之后, 是和commit过的submodule是同步的.  


### update
每次pull的时候, 要更新submodule. 
git pull 
git submodule foreach git submodule update 

update会搞出来新的分支. 临时分支会丢失掉. 所以本地要想修改必须保存分支.  

!!! submodule 

 update的时候, 会不会覆盖掉本地修改. 这样要试一下. 答案: 不会, 只会更新git树.

git submodule 列出当前的submodule. 都是基于commit的.  

### 循环
只是检出到 server 的最新版本
git submodule foreach --recursive git submodule init 
git submodule foreach --recursive git submodule update 

直接更新到每个 submodule 的最新版本. 
git submodule foreach --recursive git checkout master
git submodule foreach --recursive git pull

如果你动了 submodule, 你在 push labkit 的时候就会有问题. 
必须是一个 push 过的submodule, 并且, 通过整体测试. 

---- 
### 不用 submodule
labkit 不管 submodule 呢, submodule 只是用来 push 的?

git submodule foreach --recursive git checkout master
git submodule foreach --recursive git pull
方法

### 结论
还是使用 submodule, 但是实际用的时候不用太关注 submodule. submodule 作为 labkit 官方发布的包的版本管理用. 各个包可以自己管理. 另外, 还是用 packages 的这个形式, 这个插件系统使得用户可以自己维护自己的用到的模块. labkit 可以不需要合并它们进入主分支. 

这个插件系统和 python 库有啥区别? managed. 一个大的包叫还叫包或模块, 一个文件叫vi函数. 
用 python 包标准结构的两层目录, 可以让每个包也包含自己的文件. 可也有包自己的文档, 以后也可以抓取文档去生成. 所以 labkit 插件的基本单元还是包. 

