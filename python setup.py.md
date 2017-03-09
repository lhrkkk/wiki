

打包和安装: 
	python setup.py sdist 
	python setup.py install 
上传至pypi: 
	python setup.py sdist upload -r testpypi 
	python setup.py register -r testpypi 


---- ------ 
python setup.py develop 
python setup.py build 
python setup.py test 
---- --------- 
pbr: 生成setup.py  
subunit.run 自动测试 -\> testr 分析结果 -\> setup.py testr —coverage 和setup.py集成并测试覆盖, 以及更多参数 
tox: 虚拟环境, 安装依赖, 并运行testr测试 

