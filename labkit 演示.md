# labkit workflow

---

## labkit, 实验室工作站

labkit内部的逻辑, 组织, 构造原则是基于语言, 函数库, 模块库, 算法库, 四个层级.

在这四层上的, 我们实际工作和打交道的, 便是labkit的约定的目录结构.

这个框架并不只是做某种特殊计算, 可以作为实验室工作的通用组织形式.

---

## 1. 加入讨论组, 看通知, 下载安装labkit
```
git clone https://github.com/lhrkkk/labkit
cd labkit
./install.sh
```

---

## 2. 目录结构剖析

最外层目录结构

```
labkit
├── CHANGELOG.md    项目平庸文件
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── TODO
├── backup  备份和恢复
├── bin 可执行文件
├── databank  好的结果的数据库
├── deploy  部署labkit的相关代码
├── docs  文档
├── frontend   labkit前端, 包括labkit网站, wiki系统
├── packages  主体代码, python库, 包括general和labkit
├── sbin  管理员可执行文件
├── wiki  wiki笔记
└── workspace 工作区
```

---

labkit包目录结构

```
labkit/packages/labkit/labkit
├── algorithm 算法
├── api 对前端开放的api
├── cmd labkit命令行
├── compute 量化计算, 分子力场等计算
├── conformer 构型相关操作
├── databank  databank相关操作
├── ensemble  集合相关操作
├── module_settings 模块默认设置值
├── sample  采样
├── scheduler 任务调度器
├── tests 测试
├── labkit.conf labkit系统配置文件
```

---


## 3. 开始计算

还是使用以前的版本演示

启动

```
labkit worker
labkit front
```

提交计算

```
cd workplace/example
准备好输入文件
labkit push
```

当前目录查看结果

---

## 4. 开发

labkit/compute/example.py文件

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
from general import gs
log=gs.get_logger(__name__,debug=False)

def run(args):
    print "!!!!! hello "+args['name']+ ", I like you!!!!"
    print "current code is " + str(args['code'])
    return True
```

---

如果有需要, 可以加入以下内容, selfrun可以让脚本自身独立运行. 方便调试和独立使用.

```python
def test():
    pass
def selfrun(args={}):
    import labkit.init_gs
    from general.interpreter.loader import callrun
    callrun(__file__,args)
if __name__ == '__main__':
    # test()
    selfrun()

```

---

综合起来的模板就是:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
from general import gs
log=gs.get_logger(__name__,debug=False)

def test():
    pass

def run(args):
    print "!!!!! hello "+args['name']+ ", I like you!!!!"
    return True

def selfrun(args={}):
    import labkit.init_gs
    from general.interpreter.loader import callrun
    callrun(__file__,args)
if __name__ == '__main__':
    # test()
    selfrun()

```

---

模块中的run函数将作用于当前构型. run函数可以访问上下文, 使用args['code'], args['xyz']等访问当前构型.  

然后就可以在输入文件里面用使用这个模块名了

---

## 5. 测试

最简单的测试:

labkit/test/unit/compute/test_example.py


`self.assertEqual(example.add(1,2), 1+2)` 来测试add函数是否是我们所期待的结果.


---

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import unittest
import labkit.init_gs
from labkit.compute import example

class TestExample(unittest.TestCase):
    def setUp(self):
        pass

    def tearDown(self):
        pass

    def test_add(self):
        self.assertEqual(example.add(1,2), 1+2)

if __name__ == '__main__':
    unittest.main()
```

---

# 6. 小结
labkit包含所有所需要的东西, 以及一间安装脚本.

安装脚本会安装并配置: python virtualenv环境, 安装相应的库, 设置环境变量和相关配置. 另外labkit计算需要的软件会列出在readme中, 需要用户自行安装.

cluster也一样, 有一个cluster系统, 包含所有所需要的文件, 配置, 以及一键配置的脚本.
