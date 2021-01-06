# 中文命名实体识别


## 数据集

本项目尝试使用了多种不同的模型（包括HMM，CRF，Bi-LSTM，Bi-LSTM+CRF）来解决中文命名实体识别问题，数据集用的是论文ACL 2018[Chinese NER using Lattice LSTM](https://github.com/jiesutd/LatticeLSTM)中收集的简历数据，数据的格式如下，它的每一行由一个字及其对应的标注组成，标注集采用BIOES，句子之间用一个空行隔开。

```
美	B-LOC
国	E-LOC
的	O
华	B-PER
莱	I-PER
士	E-PER

我	O
跟	O
他	O
谈	O
笑	O
风	O
生	O 
```

该数据集就位于项目目录下的`ResumeNER`文件夹里。

## 运行结果

下面是四种不同的模型以及这Ensemble这四个模型预测结果的准确率（取最好）：

|      | HMM    | CRF    | BiLSTM | BiLSTM+CRF | Ensemble |
| ---- | ------ | ------ | ------ | ---------- | -------- |
| 召回率  | 91.22% | 95.43% | 95.32% | 95.72%     | 95.65%   |
| 准确率  | 91.49% | 95.43% | 95.37% | 95.74%     | 95.69%   |
| F1分数 | 91.30% | 95.42% | 95.32% | 95.70%     | 95.64%   |

最后一列Ensemble是将这四个模型的预测结果结合起来，使用“投票表决”的方法得出最后的预测结果。

（Ensemble的三个指标均不如BiLSTM+CRF，可以认为在Ensemble过程中，是其他三个模型拖累了BiLSTM+CRF）

具体的输出可以查看`output.txt`文件。



## 快速开始

首先安装依赖项：

```
pip3 install -r requirement.txt
```

安装完毕之后，直接使用

```
python3 main.py
```

即可训练以及评估模型，评估模型将会打印出模型的精确率、召回率、F1分数值以及混淆矩阵，如果想要修改相关模型参数或者是训练参数，可以在`./models/config.py`文件中进行设置。

训练完毕之后，如果想要加载并评估模型，运行如下命令：

```shell
python3 test.py
```













