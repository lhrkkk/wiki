
### 介绍

labkit可以使用一张图来表示:

![][image-1]

中的缩写解释如下:
vi: vector interpreter 并行计算框架,
ms: molecular simulation 分子模拟模块, 目前包括构型操作, 量化计算等我们实验室的氨基酸和多肽计算需要的内容.

基本功能原型和模块结构: 站在vi上的模块, 例如ms等, 可以被vi并行解释执行, 然后是其他不用并行的内容例如文档, 样例, 网站, 所有内容打包在一起叫做labkit

workplace是工作空间, 我们在workplace目录里面工作.

### 从零开始安装labkit
Linux命令行下, 复制并运行命令 
	curl -L  https://git.ustclug.org/lhrkkk/labkit/raw/master/setup/setup_labkit_from_zero.sh | bash
即可下载并安装labkit

安装后我们得到 labkit 文件夹和配置文件夹 $HOME/.labkit, 前者是 labkit 的主程序, cd 进这个目录即可激活 labkit 然后运行 labkit 相应命令, 后者用于配置labkit. 

cd 进 labkit 目录后, 
	./show.sh
可以启动labkit的网站

如果有问题或需求, 请阅读[安装labkit]()和[配置文件]().

### 运行

终端下面敲 `labkit --help` 可以获得帮助

labkit有如下命令:

| 命令                           | 功能                   |        |
| --------                       | -----:                 | :----: |
| labkit --help                  | 获得帮助               |        |
| labkit service  xxx start/stop | 启动和停止labkit的服务 |        |
| labkit new                     | 创建新项目             |        |
| labkit calc                    | 提交计算项目           |        |
| labkit new\_module             | 创建新模块             |        |

labkit的配置文件$HOME/.labkit/vi/vi.conf管理labkit自身的相关事宜.


@todo:
旧命令参考
```
前端上启动 labkit front
节点上启动 labkit worker
```

启动labkit的服务端和工作端.

前端上运行`labkit pbs_start`同时启动front和worker并且通过pbs管理. 

---- 

### 输入输出
输入是yaml格式的算法文件, 包含算法步骤, 以及参数. 运行用labkit calc, 输出结果每步在result文件夹下.

<!-- 用yaml格式写好你要计算的体系和算法, 用labkit push命令提交, 然后等待结果 -->

输入文件样例:

```yaml
# rule:  # :分割的是字典, 没有参数的键值会被忽略, 可以用来起名字
# - list:   # -开头的是列表
# - 列表就是任务, 每一个列表会自动执行
# - 第二项会接续执行
# dict: 字典如果是一个模块名, 则调用它, 如果是个新的名字且有单一参数, 则赋值.
#
# labkit的自身的配置文件用ini格式, 全局统一, 请不要操心.
#


# 正文样例:
algorithm:
- sys:  # 只是名字, 忽略
    - sample.generate: {ensemble_name: cggg}  # 调用sample.generate模块的run函数, 传入参数列表是{ensemble_name: cggg}
    - compute.gaussian: {method: "hf/3-21G\* opt"} # 同上
    - compute.gaussian: {method: hf, energy_cut: 10} # 同上


config:
- conformer.conformer:
##### 以下是固定的常量, 不循环
##### 序列
# SEQ:
  # CGGG
xyz: cggg.xyz

##### 自由度模板, 分别指定主链和侧链的可转角度
BACKBONE_TEMPLATE:
# - [RESIDUE,    RESIDUE_NUMBER,   DIHEDRAL_NAME,    DIHEDRAL_LIST]
  - [  CYS ,          1,             PSI,            [0,90,180,270]]
  # - [  CYS ,          1,             PHI,            [0,90,180,270]]
  # - [  GLY ,          2,             PHI,            [0,90,180,270]]

  - [  GLY ,          2,             PSI,            [0,90,180,270]]


  # - [  GLY ,          3,             PHI,            [0,90,180,270]]

  # - [  GLY ,          3,             PSI,            [0,90,180,270]]

  # - [  GLY ,          4,             PHI,            [0,90,180,270]]
  # - [  GLY ,          4,             PSI,            [0,90,180,270]]


SIDE_TEMPLATE:
    # - [ CYS, 1, CHI1, [0,120,240]]
    -[]

# USE_BOND_TEMPLATE: template_test.xyz3

###### 以下是默认值
###### 侧链二面角的定义(主链的定义是固定的)
DIHEDRAL_DEFINITION:
# [DIHEDRAL_NAME, RESIDUE,   ATOM1, ATOM2, ATOM3, ATOM4 ]

    # - [PSI,        ARG,        N,   CA,   C,   N  ]
    # - [PHI,        ARG,        C,    N,  CA,   C  ]

    - [CHI1,        ARG,        N,   CA,   CB,   CG  ]
    - [CHI1,        ASN,        N,   CA,   CB,   CG  ]
    - [CHI1,        ASP,        N,   CA,   CB,   CG  ]
    - [CHI1,        CYS,        N,   CA,   CB,   SG  ]
    - [CHI1,        GLN,        N,   CA,   CB,   CG  ]
    - [CHI1,        GLU,        N,   CA,   CB,   CG  ]
    - [CHI1,        HIS,        N,   CA,   CB,   CG  ]
    - [CHI1,        ILE,        N,   CA,   CB,   CG1 ]
    - [CHI1,        LEU,        N,   CA,   CB,   CG  ]
    - [CHI1,        LYS,        N,   CA,   CB,   CG  ]
    - [CHI1,        MET,        N,   CA,   CB,   CG  ]
    - [CHI1,        PHE,        N,   CA,   CB,   CG  ]
    - [CHI1,        PRO,        N,   CA,   CB,   CG  ]
    - [CHI1,        SER,        N,   CA,   CB,   OG  ]
    - [CHI1,        THR,        N,   CA,   CB,   OG1 ]
    - [CHI1,        TRP,        N,   CA,   CB,   CG  ]
    - [CHI1,        TYR,        N,   CA,   CB,   CG  ]
    - [CHI1,        VAL,        N,   CA,   CB,   CG1 ]
    - [CHI2,        ARG,        CA,  CB,   CG,   CD  ]
    - [CHI2,        ASN,        CA,  CB,   CG,   OD1 ]
    - [CHI2,        ASP,        CA,  CB,   CG,   OD1 ]
    - [CHI2,        GLN,        CA,  CB,   CG,   CD  ]
    - [CHI2,        GLU,        CA,  CB,   CG,   CD  ]
    - [CHI2,        HIS,        CA,  CB,   CG,   ND1 ]
    - [CHI2,        ILE,        CA,  CB,   CG1,  CD  ]
    - [CHI2,        LEU,        CA,  CB,   CG,   CD1 ]
    - [CHI2,        LYS,        CA,  CB,   CG,   CD  ]
    - [CHI2,        MET,        CA,  CB,   CG,   SD  ]
    - [CHI2,        PHE,        CA,  CB,   CG,   CD1 ]
    - [CHI2,        PRO,        CA,  CB,   CG,   CD  ]
    - [CHI2,        TRP,        CA,  CB,   CG,   CD1 ]
    - [CHI2,        TYR,        CA,  CB,   CG,   CD1 ]
    - [CHI3,        ARG,        CB,  CG,   CD,   NE  ]
    - [CHI3,        GLN,        CB,  CG,   CD,   OE1 ]
    - [CHI3,        GLU,        CB,  CG,   CD,   OE1 ]
    - [CHI3,        LYS,        CB,  CG,   CD,   CE  ]
    - [CHI3,        MET,        CB,  CG,   SD,   CE  ]
    - [CHI4,        ARG,        CG,  CD,   NE,   CZ  ]
    - [CHI4,        LYS,        CG,  CD,   CE,   NZ  ]
    - [CHI5,        ARG,        CD,  NE,   CZ,   NH1 ]



INTER_RESIDUE_BONDING_TEMPLATE:
# - [RESIDUE_NUMBER, ATOM1, RESIDUE_NUMBER, ATOM2 ] TODO: 再检查一遍

  - []



INNER_RESIDUE_BONDING_TEMPLATE:
# - [RESIDUE, ATOM1, ATOM2 ] TODO: 再检查一遍
  - ['ALA', 'C', 'O']
  - ['ALA', 'CA', 'C']
  - ['ALA', 'CA', 'HA']
  - ['ALA', 'CA', 'N']
  - ['ALA', 'CB', 'CA']
  - ['ALA', 'CB', 'HB2']
  - ['ALA', 'CB', 'HB3']
  - ['ALA', 'HB1', 'CB']
  - ['ALA', 'N', 'HT1']
  - ['ALA', 'N', 'HT2']
  - ['ALA', 'N', 'HT3']
  - ['ARG', '1HH1', 'NH1']
  - ['ARG', 'C', 'O']
  - ['ARG', 'CA', 'C']
  - ['ARG', 'CA', 'CB']
  - ['ARG', 'CA', 'HA']
  - ['ARG', 'CD', 'HD1']
  - ['ARG', 'CD', 'HD2']
  - ['ARG', 'CD', 'NE']
  - ['ARG', 'CG', 'CB']
  - ['ARG', 'CG', 'CD']
  - ['ARG', 'CG', 'HG2']
  - ['ARG', 'CZ', 'NH2']
  - ['ARG', 'HB1', 'CB']
  - ['ARG', 'HB2', 'CB']
  - ['ARG', 'HE', 'NE']
  - ['ARG', 'HG1', 'CG']
  - ['ARG', 'HN', 'N']
  - ['ARG', 'N', 'CA']
  - ['ARG', 'NE', 'CZ']
  - ['ARG', 'NH1', '2HH1']
  - ['ARG', 'NH1', 'CZ']
  - ['ARG', 'NH2', '1HH2']
  - ['ARG', 'NH2', '2HH2']
  - ['ASN', '1HD2', 'ND2']
  - ['ASN', 'C', 'O']
  - ['ASN', 'CA', 'C']
  - ['ASN', 'CA', 'CB']
  - ['ASN', 'CB', 'HB1']
  - ['ASN', 'CB', 'HB2']
  - ['ASN', 'CG', 'CB']
  - ['ASN', 'HA', 'CA']
  - ['ASN', 'N', 'CA']
  - ['ASN', 'N', 'HN']
  - ['ASN', 'ND2', '2HD2']
  - ['ASN', 'ND2', 'CG']
  - ['ASN', 'OD1', 'CG']
  - ['ASP', 'C', 'O']
  - ['ASP', 'CA', 'C']
  - ['ASP', 'CA', 'HA']
  - ['ASP', 'CB', 'CA']
  - ['ASP', 'CB', 'HB1']
  - ['ASP', 'CG', 'CB']
  - ['ASP', 'CG', 'OD1']
  - ['ASP', 'CG', 'OD2']
  - ['ASP', 'HB2', 'CB']
  - ['ASP', 'N', 'CA']
  - ['ASP', 'N', 'HN']
  - ['CYS', 'C', 'O']
  - ['CYS', 'CA', 'C']
  - ['CYS', 'CB', 'CA']
  - ['CYS', 'CB', 'HB1']
  - ['CYS', 'CB', 'HB2']
  - ['CYS', 'HA', 'CA']
  - ['CYS', 'HG', 'SG']
  - ['CYS', 'N', 'CA']
  - ['CYS', 'N', 'HN']
  - ['CYS', 'SG', 'CB']
  - ['GLN', '1HE2', 'NE2']
  - ['GLN', 'CA', 'C']
  - ['GLN', 'CA', 'CB']
  - ['GLN', 'CB', 'CG']
  - ['GLN', 'CD', 'CG']
  - ['GLN', 'CD', 'OE1']
  - ['GLN', 'CG', 'HG1']
  - ['GLN', 'HA', 'CA']
  - ['GLN', 'HB1', 'CB']
  - ['GLN', 'HB2', 'CB']
  - ['GLN', 'HG2', 'CG']
  - ['GLN', 'HN', 'N']
  - ['GLN', 'N', 'CA']
  - ['GLN', 'NE2', '2HE2']
  - ['GLN', 'NE2', 'CD']
  - ['GLN', 'O', 'C']
  - ['GLU', 'C', 'O']
  - ['GLU', 'CA', 'C']
  - ['GLU', 'CB', 'CA']
  - ['GLU', 'CB', 'HB2']
  - ['GLU', 'CD', 'CG']
  - ['GLU', 'CD', 'OE1']
  - ['GLU', 'CD', 'OE2']
  - ['GLU', 'CG', 'CB']
  - ['GLU', 'CG', 'HG2']
  - ['GLU', 'HA', 'CA']
  - ['GLU', 'HB1', 'CB']
  - ['GLU', 'HG1', 'CG']
  - ['GLU', 'N', 'CA']
  - ['GLU', 'N', 'HN']
  - ['GLY', 'C', 'O']
  - ['GLY', 'CA', 'C']
  - ['GLY', 'CA', 'HA1']
  - ['GLY', 'CA', 'HA2']
  - ['GLY', 'CA', 'N']
  - ['GLY', 'HN', 'N']
  - ['HIS', 'C', 'O']
  - ['HIS', 'CA', 'C']
  - ['HIS', 'CA', 'CB']
  - ['HIS', 'CB', 'HB1']
  - ['HIS', 'CB', 'HB2']
  - ['HIS', 'CG', 'CB']
  - ['HIS', 'CG', 'CD2']
  - ['HIS', 'HA', 'CA']
  - ['HIS', 'HD2', 'CD2']
  - ['HIS', 'HD2', 'O']
  - ['HIS', 'HE1', 'CE1']
  - ['HIS', 'N', 'CA']
  - ['HIS', 'N', 'HN']
  - ['HIS', 'ND1', 'CE1']
  - ['HIS', 'ND1', 'CG']
  - ['HIS', 'ND1', 'HD1']
  - ['HIS', 'NE2', 'CD2']
  - ['HIS', 'NE2', 'CE1']
  - ['ILE', '1HD1', 'CD1']
  - ['ILE', '1HG2', 'CG2']
  - ['ILE', '2HG1', 'CG1']
  - ['ILE', '2HG2', 'CG2']
  - ['ILE', '3HD1', 'CD1']
  - ['ILE', '3HG2', 'CG2']
  - ['ILE', 'C', 'O']
  - ['ILE', 'CA', 'C']
  - ['ILE', 'CA', 'CB']
  - ['ILE', 'CA', 'HA']
  - ['ILE', 'CB', 'CG2']
  - ['ILE', 'CB', 'HB']
  - ['ILE', 'CD1', '2HD1']
  - ['ILE', 'CD1', 'CG1']
  - ['ILE', 'CG1', '1HG1']
  - ['ILE', 'CG1', 'CB']
  - ['ILE', 'N', 'CA']
  - ['ILE', 'N', 'HN']
  - ['LEU', '1HD1', 'CD1']
  - ['LEU', '1HD2', 'CD2']
  - ['LEU', '2HD2', 'CD2']
  - ['LEU', 'C', 'O']
  - ['LEU', 'CA', 'C']
  - ['LEU', 'CA', 'CB']
  - ['LEU', 'CB', 'HB1']
  - ['LEU', 'CB', 'HB2']
  - ['LEU', 'CD1', '2HD1']
  - ['LEU', 'CD1', '3HD1']
  - ['LEU', 'CD1', 'CG']
  - ['LEU', 'CD2', '3HD2']
  - ['LEU', 'CD2', 'CG']
  - ['LEU', 'CG', 'CB']
  - ['LEU', 'HA', 'CA']
  - ['LEU', 'HG', 'CG']
  - ['LEU', 'N', 'CA']
  - ['LEU', 'N', 'HN']
  - ['LYS', 'CA', 'C']
  - ['LYS', 'CA', 'HA']
  - ['LYS', 'CA', 'N']
  - ['LYS', 'CB', 'CA']
  - ['LYS', 'CB', 'HB1']
  - ['LYS', 'CD', 'HD1']
  - ['LYS', 'CD', 'HD2']
  - ['LYS', 'CE', 'CD']
  - ['LYS', 'CE', 'HE1']
  - ['LYS', 'CE', 'HE2']
  - ['LYS', 'CG', 'CB']
  - ['LYS', 'CG', 'CD']
  - ['LYS', 'CG', 'HG2']
  - ['LYS', 'HB2', 'CB']
  - ['LYS', 'HG1', 'CG']
  - ['LYS', 'HZ2', 'NZ']
  - ['LYS', 'HZ3', 'NZ']
  - ['LYS', 'N', 'HN']
  - ['LYS', 'NZ', 'CE']
  - ['LYS', 'NZ', 'HZ1']
  - ['LYS', 'O', 'C']
  - ['MET', 'C', 'O']
  - ['MET', 'CA', 'C']
  - ['MET', 'CA', 'CB']
  - ['MET', 'CB', 'HB2']
  - ['MET', 'CE', 'HE2']
  - ['MET', 'CE', 'SD']
  - ['MET', 'CG', 'CB']
  - ['MET', 'CG', 'HG2']
  - ['MET', 'CG', 'SD']
  - ['MET', 'HA', 'CA']
  - ['MET', 'HB1', 'CB']
  - ['MET', 'HE1', 'CE']
  - ['MET', 'HE3', 'CE']
  - ['MET', 'HG1', 'CG']
  - ['MET', 'N', 'CA']
  - ['MET', 'N', 'HN']
  - ['PHE', 'C', 'O']
  - ['PHE', 'CA', 'C']
  - ['PHE', 'CA', 'CB']
  - ['PHE', 'CA', 'HA']
  - ['PHE', 'CB', 'CG']
  - ['PHE', 'CB', 'HB1']
  - ['PHE', 'CB', 'HB2']
  - ['PHE', 'CD1', 'CE1']
  - ['PHE', 'CD1', 'CG']
  - ['PHE', 'CD2', 'CE2']
  - ['PHE', 'CE1', 'CZ']
  - ['PHE', 'CE1', 'HE1']
  - ['PHE', 'CE2', 'CZ']
  - ['PHE', 'CG', 'CD2']
  - ['PHE', 'CG', 'HD1']
  - ['PHE', 'HD1', 'CD1']
  - ['PHE', 'HD2', 'CD2']
  - ['PHE', 'HE2', 'CE2']
  - ['PHE', 'HZ', 'CZ']
  - ['PHE', 'N', 'CA']
  - ['PHE', 'N', 'HN']
  - ['PRO', 'CA', 'C']
  - ['PRO', 'CA', 'CB']
  - ['PRO', 'CA', 'HA']
  - ['PRO', 'CB', 'CG']
  - ['PRO', 'CB', 'HB1']
  - ['PRO', 'CB', 'HB2']
  - ['PRO', 'CD', 'CD2']
  - ['PRO', 'CD', 'CG']
  - ['PRO', 'CG', 'HG2']
  - ['PRO', 'HD1', 'CD']
  - ['PRO', 'HD1', 'CD2']
  - ['PRO', 'HD2', 'CD']
  - ['PRO', 'HG1', 'CG']
  - ['PRO', 'N', 'CA']
  - ['PRO', 'N', 'CD']
  - ['PRO', 'O', 'C']
  - ['SER', 'C', 'O']
  - ['SER', 'CA', 'C']
  - ['SER', 'CA', 'CB']
  - ['SER', 'CA', 'N']
  - ['SER', 'HA', 'CA']
  - ['SER', 'HB1', 'CB']
  - ['SER', 'HB2', 'CB']
  - ['SER', 'HG', 'OG']
  - ['SER', 'HN', 'N']
  - ['SER', 'OG', 'CB']
  - ['THR', '3HG2', 'CG2']
  - ['THR', 'C', 'CA']
  - ['THR', 'CA', 'CB']
  - ['THR', 'CA', 'HA']
  - ['THR', 'CB', 'CG2']
  - ['THR', 'CB', 'HB']
  - ['THR', 'CB', 'OG1']
  - ['THR', 'CG2', '1HG2']
  - ['THR', 'CG2', '2HG2']
  - ['THR', 'HG1', 'OG1']
  - ['THR', 'HN', 'N']
  - ['THR', 'N', 'CA']
  - ['THR', 'O', 'C']
  - ['TRP', 'C', 'CA']
  - ['TRP', 'CB', 'CA']
  - ['TRP', 'CB', 'HB2']
  - ['TRP', 'CD1', 'CG']
  - ['TRP', 'CD1', 'HD1']
  - ['TRP', 'CD2', 'CG']
  - ['TRP', 'CE2', 'CD2']
  - ['TRP', 'CE3', 'CD2']
  - ['TRP', 'CE3', 'CZ3']
  - ['TRP', 'CG', 'CB']
  - ['TRP', 'CH2', 'CZ3']
  - ['TRP', 'CZ2', 'CE2']
  - ['TRP', 'CZ2', 'CH2']
  - ['TRP', 'HA', 'CA']
  - ['TRP', 'HB1', 'CB']
  - ['TRP', 'HE1', 'NE1']
  - ['TRP', 'HE3', 'CE3']
  - ['TRP', 'HH2', 'CH2']
  - ['TRP', 'HZ2', 'CZ2']
  - ['TRP', 'HZ3', 'CZ3']
  - ['TRP', 'N', 'CA']
  - ['TRP', 'N', 'HN']
  - ['TRP', 'NE1', 'CD1']
  - ['TRP', 'NE1', 'CE2']
  - ['TRP', 'O', 'C']
  - ['TYR', 'CA', 'C']
  - ['TYR', 'CA', 'CB']
  - ['TYR', 'CA', 'N']
  - ['TYR', 'CB', 'HB1']
  - ['TYR', 'CB', 'HB2']
  - ['TYR', 'CD2', 'CE2']
  - ['TYR', 'CD2', 'HD2']
  - ['TYR', 'CE1', 'CD1']
  - ['TYR', 'CE1', 'CZ']
  - ['TYR', 'CE2', 'HE2']
  - ['TYR', 'CG', 'CB']
  - ['TYR', 'CG', 'CD1']
  - ['TYR', 'CG', 'CD2']
  - ['TYR', 'CZ', 'CE2']
  - ['TYR', 'CZ', 'OH']
  - ['TYR', 'HA', 'CA']
  - ['TYR', 'HD1', 'CD1']
  - ['TYR', 'HE1', 'CE1']
  - ['TYR', 'HN', 'N']
  - ['TYR', 'O', 'C']
  - ['TYR', 'OH', 'HH']
  - ['VAL', '1HG2', 'CG2']
  - ['VAL', '2HG2', 'CG2']
  - ['VAL', '3HG2', 'CG2']
  - ['VAL', 'C', 'O']
  - ['VAL', 'CA', 'C']
  - ['VAL', 'CA', 'HA']
  - ['VAL', 'CA', 'N']
  - ['VAL', 'CB', 'CA']
  - ['VAL', 'CB', 'CG2']
  - ['VAL', 'CG1', '1HG1']
  - ['VAL', 'CG1', '2HG1']
  - ['VAL', 'CG1', '3HG1']
  - ['VAL', 'CG1', 'CB']
  - ['VAL', 'HB', 'CB']
  - ['VAL', 'N', 'HN']

```

结果分析, 和计算原理是一样的, 只是运行的程序不同而已. 也可以并行化.

---- 

### 运行
通过`labkit calc`提交运行, 在result文件夹下面看到结果

---- 

### 输出
计算的每一步的和最终的输出都会以单独的文件夹的形式出现在当前文件夹下.

![][image-2]



---- 





[image-1]:	images/labkit%E7%AB%8B%E6%96%B9%E4%BD%93%E7%A4%BA%E6%84%8F%E5%9B%BE.svg
[image-2]:	images/%E7%BB%93%E6%9E%9C%E6%88%AA%E5%9B%BE.png