
[buildout][1]是一个 python 程序打包工具, 有很多项目使用 buildout 打包.

### 拿到一个 buildout 的项目的 buildout用法
	python bootstrap.py  根据环境生成bin/buildout
	bin/buildout  根据配置生成独立的python解释器和脚本.

### 安装 buildout
	pip install zc.buildout

如果是使用 virtualenv

	virtualenv --no-site-packages newproject 
	cd newproject 
	bin/pip install zc.buildout 
	bin/buildout init 

以上不提供bootstrap.py 文件, 还要手动下载一下.  

	wget -O bootstrap.py https://bootstrap.pypa.io/bootstrap-buildout.py 


### 对于新项目的 buildout 使用
从零开始生成buildout.cfg 初始配置文件和 buildout

	buildout init

或者是从已有项目 buildout.cfg 生成 buildout

	buildout bootstrap 或 python bootstrap.py
两者功能一样, 都是生成 buildout或 bin/buildout, 建立本地环境, 并安装依赖. 

buildout.cfg是配置文件，类似于maven的pom文件，而bin/buildout是build脚本。
当共享代码的时候，只有buildout.cfg需要加入版本控制。checkout之后，只需要运行buildout bootstrap，就可以再次生成这些文件夹和文件。

buildout.cfg 以及 buildout 的具体使用, 参见[https://jacobian.org/writing/django-apps-with-buildout/][2]



[1]:	http://www.buildout.org/en/latest/index.html
[2]:	https://jacobian.org/writing/django-apps-with-buildout/