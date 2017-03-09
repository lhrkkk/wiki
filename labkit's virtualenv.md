
[virtualenv](), setup.py, pip 的基本使用, 请查阅相关文档. 
要想使自己的包给别人使用, 必须打包. 

## python 打包基础知识
### python 环境
python 的程序不是独立的 exe 文件, 而是运行在一个环境中. 
python 环境是一个 python 命令加上 lib 包路径. 所有的 python 程序执行, 都有一个环境. 

### pip
pip 命令可以到 pypi 上面获取并安装一个包到本地 python 环境.

### setup.py
在自己写的程序目录下, 按照 python 的规则写好 setup.py 文件, 可以用于将自己的包安装到别人的 python 环境中. 

### 上传自己的包到 pypi 服务器
到 pypi 网站上面注册帐号, 然后用
`python setup.py register -r pypi` 和 
`python setup.py sdist upload -r pypi`
 命令可以把自己的包上传到 pypi 服务器上. 以后别人就可以使用 `pip install` 命令安装你的包

## labkit 的 virtualenv 环境
#### python 打包方式
自己写的 python 程序, 可以做成独立的库发布, 用以安装到别人的python 环境中供别人使用, 并可以安装 console\_scropt 到别人的 bin 目录中. 供别人使用. 

如果做成独立程序, 则 python 程序打包方式有两种, 一种是virtualenv, 一种是利用buildout. 
virtualenv 是创建一个独立的 python 环境, 适合多个package共用一个环境.
buildout 是创建一个脚本, 当程序迁移到别人的环境中的时候, 运行这个脚本, 它会根据环境安装相应依赖在本地, 相当于嫁接到别人的环境中. 适合一个package打包到别的环境去使用. 

#### virtualenv 使用方法
virtualenvwrapper和autoenv

#### setup.py develop 和 pip install  -e
pip install -e
setup.py develop

#### 环境变量
labkit 修改环境变量
通过 virtualenvwrapper 的



---- 

详细说明:
setup.py develp, pip install -e 只是安装在当前环境的site-packages中, 并用egg-link的形式. 
buildout是系统python+include当前安装egg包路径. 只能执行console_script用. buildout develop 也是如此. buildout只是给最后执行的脚本内部生成路径. 把所有依赖的包都加到生成路径里面了. 适用于只是需要提供给用户一个运行脚本的时候用. 使用场合有点像打包成exe. sdk需要选择生成的python. 脚本都要用生成的python来运行.  
console_script 可以直接运行, 所有脚本要用生成的python来运行.  
virtualenv是改变环境变量. 运行的时候用一个独立的python, 依赖包必须安装到env中, 这样文件不用修改, 每个脚本都可以运行. 所有脚本都必须激活env运行. 要用setup.py develop或者修改路径的方式来开发. 适合labkit. 

virtualenvwrapper管理env环境, 可以提前加载一些路径. autoenv自动激活env.   

