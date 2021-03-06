# Fashion_AI

## 执行依赖的环境和库

### 在训练模块中需要的库

  random

  math

  PIL

  keras

  numpy

  tensorflow

  os

  pandas

### 在测试模块中需要的库为

  PIL

  numpy

  os

  keras

  pandas

  
## 训练步骤说明
  
先运行preprocess.py生成过渡文件，再运行run.py生成模型权重

### preprocess.py

运行 preprocess.py

1.导入训练数据base与标签label。

2.图像的标签扩展为54位的标签，将原有的标签导入到该标签中设为1，其余为0

3.为避免过拟合现象，将训练数据划分出一部分为测试数据。

4.将图像的路径与54位二进制标签对应保存在csv文件中。

### model模型的建立

该函数为子函数，不需要运行。

1.导入densenet121的模型结构，该模型结构去除了原模型的结尾。

2.在densenet121模型结尾加上两层全连接层，最后一层使用sigmoid作为激活函数，其余使用relu作为激活函数。

3.在初始化模型时保留densenet121与本模型共享层的权重作为初始权重。

### 训练函数生成model

运行run.py

1.导入help.py文件中的帮助函数。

2.设置算法各个参数。

3.生成训练数据与测试数据。

4.导入初始的模型结构以及权重。

5.使用SGD作为学习算法，为增加后期学习效果，使用训练函数model.fit_generator中的callback参数使学习率下降。

6.保存学习后的权重。

### 其余函数

densenet_updated_GN.py 与 groupnorm.py 为获取densenet121结构的辅助函数，其中配套的权重保存在对应目录的desnet_weight文件夹中

## 测试步骤说明

运行run.py直接生成结果文件

### preprocess.py

在测试模块中没有preprocess.py，这是由于在测试阶段只需要载入图像再进行预测即可，不需要额外的preprocess.py程序。

### model模型的建立

该函数为子函数，不需要运行。

1.导入densenet121的模型结构，该模型结构去除了原模型的结尾。

2.在densenet121模型结尾加上两层全连接层，最后一层使用sigmoid作为激活函数，其余使用relu作为激活函数。

3.在初始化模型时保留densenet121与本模型共享层的权重作为初始权重。

4.在测试阶段直接导入已训练好的权重。

### 运行run.py

1.导入初始模型结构。

2.载入由训练程序训练好的模型权重。

3.读取测试数据的数据。

4.将测试数据一一导入到模型中进行预测。

5.提取输出数据中感兴趣的部分并进行归一化，得到每个标签的概率值。

6.将图像名字，标签，以及对应概率保存为csv文件。

### 其余函数

densenet_updated_GN.py 与 groupnorm.py 为获取densenet121结构的辅助函数，其中配套的权重保存在对应目录的desnet_weight文件夹中
