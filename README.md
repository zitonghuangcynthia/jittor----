# jittor大规模无监督语义分割

## 简介

本项目包含了三届计图挑战赛计图 - 赛道二大规模无监督语义分割赛题的代码实现。本项目的特点是：采用了 PASS模型的 方法对 ImageNet-S50 数据集进行语义分割 处理，取得了 mIoU (Mean Intersection over Union)达到31.0511 的效果。

## 安装 

本项目可在 1 张 Titan RTX 上运行，训练时间约为 50 小时。

#### 运行环境
- ubuntu 20.04 LTS
- python >= 3.7
- jittor >= 1.3.0

#### 安装依赖
执行以下命令安装 python 依赖
```
python -m pip install scikit-learn
python -m pip install pandas
python -m pip install munkres
python -m pip install tqdm
python -m pip install pillow
python -m pip install opencv-python
python -m pip install faiss-gpu
```

#### 预训练模型
预训练模型模型下载地址为 https://dl.fbaipublicfiles.com/segment_anything/sam_vit_b_01ec64.pth，下载后放入目录 `<root>/pass-jittor/weights/pass50/` 下。与此同时修改segment-anything文件中run.sh中的checkpoint为预训练模型的位置。

## 数据预处理

将数据下载解压到 `<root>/pass-jittor/data/ImageNetS/ImageNetS50/` 下。

## 训练

单卡训练可运行以下命令：
```
bash ./test.sh
```

## 推理，测试，评估

将上述基本步骤按照指引操作完成后，您可以运行 bash ./test.sh 指令对数据集进行训练，推理，验证。

如果想要运用随机初始化的resnet model进行训练，请将main_pretrain.py文件中的import resnet部分更改为import src.resnet_original as resnet_model。 
如果想要用sam backbone进行训练，则请将main_pretrain.py文件中的import resnet部分更改为import src.resnet as resnet_model。 

如果想要对数据集进行推理，则运行inference.py文件达到效果。

如果想要对数据的推理结果进行评估，则运行evaluator.py得到评估结果


## 致谢

此项目基于论文 *Large-scale Unsupervised Semantic Segmentation* 实现，部分代码参考了 [PGSmall](https://github.com/PGSmall/segment-anything-jittor)。


