
## 安装labkit
### 从零开始安装labkit
Linux命令行下, 复制并运行命令 
	curl -L  https://git.ustclug.org/lhrkkk/labkit/raw/master/setup/setup_labkit_from_zero.sh | bash

即可下载并安装labkit

安装后我们得到 labkit 文件夹和配置文件夹 $HOME/.labkit, 前者是 labkit 的主程序, cd 进这个目录即可激活 labkit 然后运行 labkit 相应命令, 后者用于配置labkit. 

cd 进 labkit 目录后, 
	./show.sh

可以启动labkit的网站

### 手动安装
也可以到这里[labkit的代码仓库][1]查看labkit 代码, 用

	git clone --recursive git@git.ustclug.org:lhrkkk/labkit.git
	cd labkit & ./install.sh

命令下载labkit, 并运行安装. 如果遇到问题, 可以阅读 install.sh 以及下面章节. 

### labkit 的安装过程详解

@todo: 加入链接
bootstrap, 作用是安装最小系统, 然后生成安装程序所需的配置文件. 然后安装文件根据配置安装.  

最小系统包括, virtualenvwrapper, autoenv. mini-sys配置文件, 自己的加载项. 

labkit 的安装程序会安装 mongodb, beanstalkd. 以及 labkit, labkit 的前端界面, 文档.  并生成labkit 运行所用的配置文件. 

### 安装完成后得到了什么?

最小系统会被加入到用户路径. 最小系统提供最基本的命令. cd 进 labkit 目录会自动激活 labkit 环境. 会有提供 labkit 命令以及其他更高级的命令. `deactivate`可以退出 labkit 环境. 

labkit 应用程序包括 labkit daemon(启动mongodb, beanstalkd),  services(front worker), create(template)


### 问题解答

如果不小心删除了`~/.labkit` 配置文件, 可以运行下面命令从模板重新安装配置文件
	setup.sh  do install_config

如果想要立刻设置环境变量, 可以运行下面命令立刻设置环境变量
	setup.sh  do setup_env




 




[1]:	https://git.ustclug.org/lhrkkk/labkit