# model-compression
基于pytorch实现模型压缩（1、量化：8/4/2 bits、三值/二值；2、剪枝：正常、规整、针对分组卷积结构的剪枝；3、分组卷积结构；4、针对特征A二值的BN融合）

## 目前提供
1、普通卷积和分组卷积结构\<br>
2、权重W和特征A的训练中量化，W（32/8/4/2bits，三/二值） 和A（32/8/4/2bits，三/二值）任意组合\<br>
3、针对三/二值的一些tricks：W二值/三值缩放因子，W/grad（ste、saturate_ste、soft_ste）截断，W三值_gap(防止参数更新抖动)，W/A二值时BN_momentum(<0.9)，A二值时采用B-A-C-P可比C-B-A-P获得更高acc\<br>
4、多种剪枝方式：正常剪枝、规整剪枝（比如可剪枝为剩余filter个数为16的倍数）、针对分组卷积结构的剪枝（剪枝后仍保证分组卷积结构）\<br>
5、batch normalization的融合及融合前后model测试：普通融合（BN层参数 —> conv的权重w和偏置b）、针对特征A二值的融合（BN层参数 —> conv的偏置b）\<br>

## 使用（注意剪枝率和量化率平衡）
1、剪枝 —> 量化
2、分组+剪枝 —> 量化

## 可尝试
1、渐进式量化：FP32—>8—>4—>三/二值
2、对冗余度更高的模型做压缩

## 后续补充
1、使用示例及说明
2、模型压缩前后详细数据对比
3、参考论文及工程
4、调整格式~~

## 后续扩充
1、Nvidia、Google的INT8量化方案
2、对常用检测模型做压缩
3、部署（1、针对4bits/三值/二值等的量化卷积；2、终端DL框架（如MNN，NCNN，TensorRT等））
