
## labkit的git
labkit 的 [git]() 使用, 普通的时候, 使用gy, 另外注意[git submodule]() 的用法


## gy
本章介绍labkit中的git包裹gy的使用方法
主要用法

|    命令   |      功能      |               注释              |
|-----------|----------------|---------------------------------|
| gy switch | 新建或切换分支 | pull, master, checkout -b       |
| gy commit | 提交到本地     | add, commit                     |
| gy push   | 提交到服务器   | add, commit, sync, rebase, push |
| gy drop   | 删除分支       | git branch -d                   |


次要用法

|    命令   |         功能         |                   注释                   |
|-----------|----------------------|------------------------------------------|
| gy sync   | 从服务器获取最新版本 | commit, fetch , rebase (merge)           |
| gy rebase | 去除本地多余提交     | git rebase -i --autosquash origin/master |
| gy merge  | 合并分支             | merge to master                          |
|           |                      |                                          |



### gy 流程

dev1: gy swithc 新分支dev1 ; push; 保持最新
dev2: gy switch dev2 ; push; 


### workflow

[Git 工作流程总览][3]
我们选择[gitlab workflow][4]
关于[rebase][5]的介绍
最后在同步的时候参看[Git flow][6], 但是没有 dev 分支

[3]:	http://www.ruanyifeng.com/blog/2015/12/git-workflow.html
[4]:	https://www.15yan.com/story/6yueHxcgD9Z/
[5]:	http://www.jianshu.com/p/0613d8249863
[6]:	http://www.ruanyifeng.com/blog/2015/08/git-use-process.html