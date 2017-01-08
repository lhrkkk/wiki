
本篇包括使用版本控制合作开发, 代码仓库和知识仓库, 协同交流工具.

---- 

## labkit多人合作开发
### 版本控制

#### git分支示意图

分支和合并的概念:

```
0-->1-->2-->3-->merge
    |          ↗
    |-->4-->5-/
```

---- 
#### labkit的版本控制基本流程
1. 下载并新建分支. `gy clone, gy dev`
2. 修改, 提交到本地分支.  `gy commit`
3. 拉取主分支最新版本, 合并到本地分支. `gy sync`
4. 推送到主分支. `gy push; pull-request`

```
master 0-->1-->2-->3-\ ------>merged  
           |          ↘     ↗  
       dev |-->4-->5-->sync-/
```

---- 

### 详解
---- 
#### 整合过的过程

labkit使用git作为版本控制工具. git中有很多陷阱, 对于初学者会有很多困惑和易犯的错误. labkit将git常用的使用流程, 整合成gy命令, 避免直接使用git出错.

gy常用的有三条子命令: 本地commit, 获取最新版本sync(并解决冲突), 提交到远程push
gy 别名 h
hcd 命令, 切换到子项目

#### 步骤
#### 抓取最新分支
```
gy clone https://github.com/lhrkkk/labkit
gy dev
```

#### 编写代码, 执行, 编写文档
编写代码, 调试执行, 测试通过, 编写文档, 然后提交到主分支.
#### 提交
完成修改后,
```
# 1. 提交到本地
gy commit
# 2. 拉合并最新的主分支  
gy sync
# 3. 提交到主分支, 自动发起pull-request
gy push

```
代码仓库管理员会审核提交, 并决定是否接受.

#### gy详解
gy的几条子命令等价于git的
gy commit = git …


---- 


合作

---- 

### 需要保留成果==\>仓库

---- 

#### 代码仓库: git

![][image-1]

---- 

![][image-2]

---- 

#### 知识仓库: wiki, 公开wiki和私有wiki

文本化的wiki, 像普通文件一样编辑, 用git提交, 或者网页上面直接编辑.

![][image-3]

实际上就是这样的一个文件夹:

![][image-4]

markdown格式. 可以自行打开编辑, 同时网页上面也可以编辑. 参见[markdown语法]()



---- 

### 流动的过程==\>专门工具

需要达成同步, 交流, 任务列表的功能, 是典型需求, 使用已有的工具.

todo-list, 团队管理有很多, tower, Teambition, Worktile, Fengche.co, 瀑布IM

经过一一试用之后, 得到结论:

---- 

#### 任务计划和分发, 共享文档: quip
- 作用是共同编辑文档, 对应word, excel格式. 放在一个窗口里.
- 可以合作编辑任务列表.
- 可以\@人, \@文档

![][image-5]

---- 

![][image-6]

---- 

#### 即时通讯: slack
- 功能类似群
- 可以保留讨论记录, 可以保留传输的文档.
- 可以帖代码, 有代码高亮
- 可以分频道讨论
- 和quip融合, 聊天中可以@quip中的文档

![][image-7]

---- 

#### 参考文献
http://www.ruanyifeng.com/blog/2015/08/git-use-process.html
http://backlogtool.com/git-guide/cn/
http://www.ruanyifeng.com/blog/2015/12/git-workflow.html

[http://www.ruanyifeng.com/blog/2012/07/git.html][2]

[2]:	http://www.ruanyifeng.com/blog/2012/07/git.html

[image-1]:	images/github%E6%88%AA%E5%9B%BE.png
[image-2]:	images/gitlab%E6%88%AA%E5%9B%BE.png
[image-3]:	images/wiki%E6%88%AA%E5%9B%BE.png
[image-4]:	images/%E6%96%87%E4%BB%B6%E5%A4%B9%E6%88%AA%E5%9B%BE.png
[image-5]:	images/quip%E6%88%AA%E5%9B%BE1.png
[image-6]:	images/quip%E6%88%AA%E5%9B%BE2.png
[image-7]:	images/slack%E6%88%AA%E5%9B%BE.png