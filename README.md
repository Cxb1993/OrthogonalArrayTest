# OrthogonalArrayTest
OrthogonalArrayTest. 使用正交实验法设计测试用例，生成测试集。


### 1.简介
正交试验法是研究多因素、多水平的一种试验法，它是利用正交表来对试验进行设计，通过少数的试验替代全面试验，根据正交表的正交性从全面试验中挑选适量的、有代表性的点进行试验，这些有代表性的点具备了“均匀分散，整齐可比”的特点。

正交实验法设计测试用例，基本步骤如下：
1. 提取测试需求功能说明,确定因素数和水平数
2. 根据因素数和水平数确定n值
2. 选择合适的正交表
3. 根据正交表把变量的值映射到表中，设计测试用例数据集

本文参考如上步骤，使用Python实现了使用正交表自动设计测试用例的完整流程。

### 2.示例demo
输入case1,case2,case3,分别计算m（水平数）,k（因素数目）,n（实验次数），然后查询选择合适的正交表，裁剪最终生成相关测试集


```
from OAT import *
import json

if __name__ == "__main__":
    oat = OAT ()
    case1 = OrderedDict ( [ ('K1', [ 0, 1 ]),
                            ('K2', [ 0, 1 ]),
                            ('K3', [ 0, 1 ]) ] )

    case2 = OrderedDict ( [ ('A', [ 'A1', 'A2', 'A3' ]),
                            ('B', [ 'B1', 'B2', 'B3', 'B4' ]),
                            ('C', [ 'C1', 'C2', 'C3' ]),
                            ('D', [ 'D1', 'D2']) ] )

    case3 = OrderedDict ( [ (u'对比度', [ u'正常', u'极低', u'低', u'高', u'极高' ]),
                            (u'色彩效果', [ u'无', u'黑白', u'棕褐色', u'负片', u'水绿色' ]),
                            (u'感光度', [ u'自动', 100, 200, 400, 800 ]),
                            (u'白平衡', [ u'自动', u'白炽光', u'日光', u'荧光', u'阴光' ]),
                            (u'照片大小', [ '5M', '3M', '2M', '1M', 'VGA' ]),
                            (u'闪光模式', [ u'开', u'关' ]) ] )

    print json.dumps(oat.genSets(case1))
    print json.dumps(oat.genSets(case2))
    print json.dumps(oat.genSets(case3))

```

执行结果如下：

```
[{"K1": 0, "K2": 0, "K3": 0}, {"K1": 0, "K2": 1, "K3": 1}, {"K1": 1, "K2": 0, "K3": 1}, {"K1": 1, "K2": 1, "K3": 0}]
[{"A": "A1", "B": "B1", "C": "C1", "D": "D1"}, {"A": "A1", "B": "B2", "C": "C2", "D": "D2"}, {"A": "A1", "B": "B3", "C": "C3", "D": null}, {"A": "A1", "B": "B4", "C": null, "D": null}, {"A": "A2", "B": "B1", "C": "C2", "D": null}, {"A": "A2", "B": "B2", "C": "C1", "D": null}, {"A": "A2", "B": "B3", "C": null, "D": "D1"}, {"A": "A2", "B": "B4", "C": "C3", "D": "D2"}, {"A": "A3", "B": "B1", "C": "C3", "D": null}, {"A": "A3", "B": "B2", "C": null, "D": null}, {"A": "A3", "B": "B3", "C": "C1", "D": "D2"}, {"A": "A3", "B": "B4", "C": "C2", "D": "D1"}, {"A": null, "B": "B1", "C": null, "D": "D2"}, {"A": null, "B": "B2", "C": "C3", "D": "D1"}, {"A": null, "B": "B3", "C": "C2", "D": null}, {"A": null, "B": "B4", "C": "C1", "D": null}]
[{"\u5bf9\u6bd4\u5ea6": "\u6b63\u5e38", "\u8272\u5f69\u6548\u679c": "\u65e0", "\u611f\u5149\u5ea6": "\u81ea\u52a8", "\u767d\u5e73\u8861": "\u81ea\u52a8", "\u7167\u7247\u5927\u5c0f": "5M", "\u95ea\u5149\u6a21\u5f0f": "\u5f00"}, {"\u5bf9\u6bd4\u5ea6": "\u6b63\u5e38", "\u8272\u5f69\u6548\u679c": "\u9ed1\u767d", "\u611f\u5149\u5ea6": 200, "\u767d\u5e73\u8861": "\u8367\u5149", "\u7167\u7247\u5927\u5c0f": "VGA", "\u95ea\u5149\u6a21\u5f0f": "\u5173"}, {"\u5bf9\u6bd4\u5ea6": "\u6b63\u5e38", "\u8272\u5f69\u6548\u679c": "\u68d5\u8910\u8272", "\u611f\u5149\u5ea6": 800, "\u767d\u5e73\u8861": "\u767d\u70bd\u5149", "\u7167\u7247\u5927\u5c0f": "1M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6b63\u5e38", "\u8272\u5f69\u6548\u679c": "\u8d1f\u7247", "\u611f\u5149\u5ea6": 100, "\u767d\u5e73\u8861": "\u9634\u5149", "\u7167\u7247\u5927\u5c0f": "2M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6b63\u5e38", "\u8272\u5f69\u6548\u679c": "\u6c34\u7eff\u8272", "\u611f\u5149\u5ea6": 400, "\u767d\u5e73\u8861": "\u65e5\u5149", "\u7167\u7247\u5927\u5c0f": "3M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u4f4e", "\u8272\u5f69\u6548\u679c": "\u65e0", "\u611f\u5149\u5ea6": 800, "\u767d\u5e73\u8861": "\u8367\u5149", "\u7167\u7247\u5927\u5c0f": "2M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u4f4e", "\u8272\u5f69\u6548\u679c": "\u9ed1\u767d", "\u611f\u5149\u5ea6": 100, "\u767d\u5e73\u8861": "\u767d\u70bd\u5149", "\u7167\u7247\u5927\u5c0f": "3M", "\u95ea\u5149\u6a21\u5f0f": "\u5f00"}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u4f4e", "\u8272\u5f69\u6548\u679c": "\u68d5\u8910\u8272", "\u611f\u5149\u5ea6": 400, "\u767d\u5e73\u8861": "\u9634\u5149", "\u7167\u7247\u5927\u5c0f": "5M", "\u95ea\u5149\u6a21\u5f0f": "\u5173"}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u4f4e", "\u8272\u5f69\u6548\u679c": "\u8d1f\u7247", "\u611f\u5149\u5ea6": "\u81ea\u52a8", "\u767d\u5e73\u8861": "\u65e5\u5149", "\u7167\u7247\u5927\u5c0f": "VGA", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u4f4e", "\u8272\u5f69\u6548\u679c": "\u6c34\u7eff\u8272", "\u611f\u5149\u5ea6": 200, "\u767d\u5e73\u8861": "\u81ea\u52a8", "\u7167\u7247\u5927\u5c0f": "1M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u4f4e", "\u8272\u5f69\u6548\u679c": "\u65e0", "\u611f\u5149\u5ea6": 400, "\u767d\u5e73\u8861": "\u767d\u70bd\u5149", "\u7167\u7247\u5927\u5c0f": "VGA", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u4f4e", "\u8272\u5f69\u6548\u679c": "\u9ed1\u767d", "\u611f\u5149\u5ea6": "\u81ea\u52a8", "\u767d\u5e73\u8861": "\u9634\u5149", "\u7167\u7247\u5927\u5c0f": "1M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u4f4e", "\u8272\u5f69\u6548\u679c": "\u68d5\u8910\u8272", "\u611f\u5149\u5ea6": 200, "\u767d\u5e73\u8861": "\u65e5\u5149", "\u7167\u7247\u5927\u5c0f": "2M", "\u95ea\u5149\u6a21\u5f0f": "\u5f00"}, {"\u5bf9\u6bd4\u5ea6": "\u4f4e", "\u8272\u5f69\u6548\u679c": "\u8d1f\u7247", "\u611f\u5149\u5ea6": 800, "\u767d\u5e73\u8861": "\u81ea\u52a8", "\u7167\u7247\u5927\u5c0f": "3M", "\u95ea\u5149\u6a21\u5f0f": "\u5173"}, {"\u5bf9\u6bd4\u5ea6": "\u4f4e", "\u8272\u5f69\u6548\u679c": "\u6c34\u7eff\u8272", "\u611f\u5149\u5ea6": 100, "\u767d\u5e73\u8861": "\u8367\u5149", "\u7167\u7247\u5927\u5c0f": "5M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u9ad8", "\u8272\u5f69\u6548\u679c": "\u65e0", "\u611f\u5149\u5ea6": 200, "\u767d\u5e73\u8861": "\u9634\u5149", "\u7167\u7247\u5927\u5c0f": "3M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u9ad8", "\u8272\u5f69\u6548\u679c": "\u9ed1\u767d", "\u611f\u5149\u5ea6": 800, "\u767d\u5e73\u8861": "\u65e5\u5149", "\u7167\u7247\u5927\u5c0f": "5M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u9ad8", "\u8272\u5f69\u6548\u679c": "\u68d5\u8910\u8272", "\u611f\u5149\u5ea6": 100, "\u767d\u5e73\u8861": "\u81ea\u52a8", "\u7167\u7247\u5927\u5c0f": "VGA", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u9ad8", "\u8272\u5f69\u6548\u679c": "\u8d1f\u7247", "\u611f\u5149\u5ea6": 400, "\u767d\u5e73\u8861": "\u8367\u5149", "\u7167\u7247\u5927\u5c0f": "1M", "\u95ea\u5149\u6a21\u5f0f": "\u5f00"}, {"\u5bf9\u6bd4\u5ea6": "\u9ad8", "\u8272\u5f69\u6548\u679c": "\u6c34\u7eff\u8272", "\u611f\u5149\u5ea6": "\u81ea\u52a8", "\u767d\u5e73\u8861": "\u767d\u70bd\u5149", "\u7167\u7247\u5927\u5c0f": "2M", "\u95ea\u5149\u6a21\u5f0f": "\u5173"}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u9ad8", "\u8272\u5f69\u6548\u679c": "\u65e0", "\u611f\u5149\u5ea6": 100, "\u767d\u5e73\u8861": "\u65e5\u5149", "\u7167\u7247\u5927\u5c0f": "1M", "\u95ea\u5149\u6a21\u5f0f": "\u5173"}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u9ad8", "\u8272\u5f69\u6548\u679c": "\u9ed1\u767d", "\u611f\u5149\u5ea6": 400, "\u767d\u5e73\u8861": "\u81ea\u52a8", "\u7167\u7247\u5927\u5c0f": "2M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u9ad8", "\u8272\u5f69\u6548\u679c": "\u68d5\u8910\u8272", "\u611f\u5149\u5ea6": "\u81ea\u52a8", "\u767d\u5e73\u8861": "\u8367\u5149", "\u7167\u7247\u5927\u5c0f": "3M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u9ad8", "\u8272\u5f69\u6548\u679c": "\u8d1f\u7247", "\u611f\u5149\u5ea6": 200, "\u767d\u5e73\u8861": "\u767d\u70bd\u5149", "\u7167\u7247\u5927\u5c0f": "5M", "\u95ea\u5149\u6a21\u5f0f": null}, {"\u5bf9\u6bd4\u5ea6": "\u6781\u9ad8", "\u8272\u5f69\u6548\u679c": "\u6c34\u7eff\u8272", "\u611f\u5149\u5ea6": 800, "\u767d\u5e73\u8861": "\u9634\u5149", "\u7167\u7247\u5927\u5c0f": "VGA", "\u95ea\u5149\u6a21\u5f0f": "\u5f00"}]


```



### 3.后续计划
1. 判定表查询逻辑优化
2. 测试用例集裁剪优化

### 4.参考
1. 测试用例设计-正交实验法详解：
https://wenku.baidu.com/view/a54724156edb6f1aff001f79.html
2. 用正交实验法设计测试用例：http://blog.csdn.net/fangnannanf/article/details/52813498
3. Dr. Genichi Taguchi 设计的正交表：http://www.york.ac.uk/depts/maths/tables/orthogonal.htm
4. Technical Support com：http://support.sas.com/techsup/technote/ts723_Designs.txt
