
完整开发流程, 要做的步骤
-----------------------------


## labkit模块开发
### labkit是面向开发者的
当然你可以只使用labkit已经提供的功能进行计算. 但是labkit是面向开发者的, 不只是一个供你简单计算的软件. 你可以用其中的工具和框架快捷编写或搭建你想要的计算.
### labkit是一个函数库
除了可以计算, labkit更是一系列函数库. 你可以扩展和完善这个函数库.

### 开发流程: run函数.



### 编写一个模块
在相应目录下面建立文件, 使用如下模板:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

from general import gs
log=gs.get_logger(__name__,debug=False)

def test():
    pass


def run(args):
    return True

def selfrun(args={}):
    import labkit.init_gs
    from general.interpreter.loader import callrun
    callrun(__file__,args)
if __name__ == '__main__':
    # test()
    selfrun()

```

调用模块的时候, 就会调用run函数. 作用于向量的每一个元素.

调试执行之后, 编写文档,


----

## labkit与软件工程
其实之前调整结构重命名的时候有想过叫labstudio, 一个studio什么东西都在里面了, 你在里面玩就行了. 之所以不叫labstudio, 是因为它提供的最终是一个函数库给你用的, 你也可以开发, 而不是只是仅仅使用. 你在里面开发也是很便捷的, 它是为了让开发者便捷而设计的. 所以叫labkit


它解决了一些实验室领域软件工程上的问题. 引入了一些现代的理念和技术, 解决实验室开发的规范, 功能复用, 合作开发的问题. 它是一个快捷开发的框架. 可以类比ruby on rail等网站开发框架所起的作用. 所以叫做labkit, 而不是labstudio. labstudio是一个具体功能性产品, 而labkit是一个优秀框架, 它恰巧已经提供了一般情况下你想要实现的功能, 你还可以在这个基础上便捷开发自己想要的功能.

labkit提供的是机制, 而不是具体的方针.


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

#### labkit的版本控制流程
1. 下载并新建分支. `gy clone, gy dev`
2. 修改, 提交到本地分支.  `gy commit`
3. 拉取主分支最新版本, 合并到本地分支. `gy sync`
4. 推送到主分支. `gy push; pull-request`

```
master 0-->1-->2-->3-\ ------>merged  
           |          ↘     ↗           
       dev |-->4-->5-->sync-/
```

#### 整合过的过程

因为每天都要同步, git有很多命令, 这里不介绍, 合并成一个命令gy, 然后有三条子命令: 本地commit, 获取最新版本sync(并解决冲突), 提交到远程push

### 步骤
#### 抓取最新分支
```
gy clone https://github.com/lhrkkk/labkit
gy dev
```

#### 编写代码, 执行, 编写文档
编写代码, 调试执行, 测试通过, 编写文档, 然后提交到主分支.
以编写一个模块为例:

![](images/新模块.png)

----

### 编写一个模块
在相应目录下面建立文件, 使用如下模板:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

from general import gs
log=gs.get_logger(__name__,debug=False)

def test():
    pass


def run(args):
    return True

def selfrun(args={}):
    import labkit.init_gs
    from general.interpreter.loader import callrun
    callrun(__file__,args)
if __name__ == '__main__':
    # test()
    selfrun()

```

调用模块的时候, 就会调用run函数. 作用于向量的每一个元素.

调试执行之后, 编写文档,

### 提交
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


<!-- ### 编写文档

### 提交 -->

----


3. 合作和wiki
-------------

### 需要保留成果==>仓库

----

#### 代码仓库: git

![](images/github截图.png)

----

![](images/gitlab截图.png)

----

#### 知识仓库: wiki, 公开wiki和私有wiki

文本化的wiki, 像普通文件一样编辑, 用git提交, 或者网页上面直接编辑.

![](images/wiki截图.png)

实际上就是这样的一个文件夹:

![](images/文件夹截图.png)

markdown格式. 可以自行打开编辑, 同时网页上面也可以编辑.


----

#### markdown语法

markdown是一种标记语言.
例如latex里面用`\section{第一章}` 指定文字`第一章`是一个section, 这就是一种标记.

```
# 一级标题
## 二级标题
### 三级标题
- item1
- item2


这是一个链接[百度](http://www.baidu.com)

这是一个wiki词条[各种计算方法比较](), ()里面不填东西即可

```
显示如下



# 一级标题
## 二级标题
### 三级标题
- item1
- item2

这是一个链接 [百度](http://www.baidu.com)

这是一个wiki词条 [各种计算方法比较](), ()里面不填东西即可

----

----

### 流动的过程==>专门工具

需要达成同步, 交流, 任务列表的功能, 是典型需求, 使用已有的工具.

todo-list, 团队管理有很多, tower, Teambition, Worktile, Fengche.co, 瀑布IM

经过一一试用之后, 得到结论:

----

#### 任务计划和分发, 共享文档: quip
- 作用是共同编辑文档, 对应word, excel格式. 放在一个窗口里.
- 可以合作编辑任务列表.
- 可以\@人, \@文档

![](images/quip截图1.png)

----

![](images/quip截图2.png)

----

#### 即时通讯: slack
- 功能类似群
- 可以保留讨论记录, 可以保留传输的文档.
- 可以帖代码, 有代码高亮
- 可以分频道讨论
- 和quip融合, 聊天中可以@quip中的文档

![](images/slack截图.png)

----
