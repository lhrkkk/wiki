
完整开发流程, 要做的步骤
----


## labkit模块开发
### labkit是面向开发者的
当然你可以只使用labkit已经提供的功能进行计算. 但是labkit是面向开发者的, 不只是一个供你简单计算的软件. 你可以用其中的工具和框架快捷编写或搭建你想要的计算.
### labkit是一个函数库
除了可以计算, labkit更是一系列函数库. 你可以扩展和完善这个函数库.

### 编写一个新模块
在相应目录下面建立文件, 使用如下模板:

```python
# !/usr/bin/env python
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
