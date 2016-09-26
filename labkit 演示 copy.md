## 目录结构, 四层上面的新的一层, 应用层.

## 加入讨论组, 看通知, 下载安装labkit
```
git clone https://github.com/lhrkkk/labkit
cd labkit
./install.sh
```

---

## 目录结构剖析

最外层目录结构

```
labkit
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── TODO
├── backup
├── bin
├── databank
├── deploy
├── docs
├── packages
├── sbin
├── wiki
└── workspace
```

---

labkit包目录结构

```
labkit/packages/labkit/labkit
├── algorithm
├── api
├── cmd
├── compute
├── conformer
├── databank
├── ensemble
├── module_settings
├── sample
├── scheduler
├── tests
├── labkit.conf
```

---


## 开始计算

还是使用以前的版本演示

启动

```
labkit worker
labkit front
```

提交计算

```
cd example
labkit push
```

当前目录查看结果

---

## 开发

---


cluster也一样, 包含所有所需要的东西以及一键配置的脚本.
