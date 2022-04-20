# ML

- [ML](#ml)
  - [分类算法](#分类算法)
    - [贝叶斯分类 Naive Bayes Classifier](#贝叶斯分类-naive-bayes-classifier)
    - [决策树 Decision Tree](#决策树-decision-tree)
    - [支持向量机 SVM Support Vector Machine](#支持向量机-svm-support-vector-machine)
    - [K近邻 KNN](#k近邻-knn)
    - [逻辑回归 Logistic Regression](#逻辑回归-logistic-regression)
    - [神经网络 Neural Network](#神经网络-neural-network)
  - [聚类算法](#聚类算法)
    - [K-Means(K均值)聚类](#k-meansk均值聚类)
    - [均值漂移聚类](#均值漂移聚类)
    - [基于密度的聚类方法(DBSCAN)](#基于密度的聚类方法dbscan)
    - [高斯混合模型 GMM](#高斯混合模型-gmm)
  - [CNN中卷积在图像处理中作用](#cnn中卷积在图像处理中作用)
  - [池化Pooling](#池化pooling)
  - [模型评价指标](#模型评价指标)
    - [混淆矩阵](#混淆矩阵)
    - [Precision、Recall、Accuracy、F1 Score](#precisionrecallaccuracyf1-score)
      - [Accuracy准确率](#accuracy准确率)
      - [Precision精确率或者精度](#precision精确率或者精度)
      - [Recall召回率](#recall召回率)
      - [F1 Score，Accuracy和Recall的调和指标](#f1-scoreaccuracy和recall的调和指标)
    - [ROC（Receiver Operating Characteristic）曲线](#rocreceiver-operating-characteristic曲线)
    - [ROC-AUC（arear-under-curve)](#roc-aucarear-under-curve)
    - [PR曲线](#pr曲线)
  - [特征工程](#特征工程)
    - [遇到缺值如何处理](#遇到缺值如何处理)
    - [样本不均衡解决办法](#样本不均衡解决办法)
    - [样本数据量少解决办法](#样本数据量少解决办法)

- [主页](README.md)

## 分类算法

### 贝叶斯分类 Naive Bayes Classifier

步骤：

1. 计算先验概率和条件概率。先验概率：P(好瓜)、P(坏瓜)。条件概率：每个属性估计条件概率。P(青绿|好瓜)、P(清晰|好瓜)、P(青绿|坏瓜)、P(清晰|坏瓜)

2. 计算预测概率

   P(y = 好瓜) = P(好瓜)\*P(青绿|好瓜)\*P(清晰|好瓜)

   P(y = 坏瓜) = P(坏瓜)\*P(青绿|坏瓜)\*P(清晰|坏瓜)

3. 确定类别

   max(P(y = 好瓜)，P(y = 坏瓜))

### 决策树 Decision Tree

### 支持向量机 SVM Support Vector Machine

训练集
$$T = \left\{ \left( \overrightarrow{x1},y1 \right),\left( \overrightarrow{x2},y2 \right),\left( \overrightarrow{x3},y3 \right)  \right\} $$

几何间距

$$ l_{i} = y_{i}( \frac{\overrightarrow{\omega} }{\left\| \overrightarrow{\omega}  \right\|} x_{i} + \frac{b}{\left\| \overrightarrow{\omega}  \right\|}) $$

$$ l_{i} = \frac{ y_{i} }{\left\| \overrightarrow{\omega}  \right\|} (\overrightarrow{\omega} x_{i} + b) $$

取超平面关于所有样本点最小值即为支持向量到超平面距离。因此SVM模型解决距离l最大.即 ||$\overrightarrow{\omega}$|| 最小

核函数

线性核、sigmoid核、多项式核、指数核

### K近邻 KNN

选取K个最近的元素，哪个类多就归为哪个类

### 逻辑回归 Logistic Regression

利用softmax表示逻辑回归预测函数

$$ h_{\theta}(x) = g(\theta^{T}x)=\frac{1}{1+e^{-\theta^{T}x}} $$

利用对其对数似然函数求导，运用梯度下降法找到极值。

### 神经网络 Neural Network

## 聚类算法

### K-Means(K均值)聚类

### 均值漂移聚类

在未被标记的数据点中随机选一个作为中心，找出以center为中心的所有据点作为一个簇C，将所有到据点向量相加得到向量shift，延shift方向移动||shift||距离，直到shift值很小。如果与其他簇C2中心距离小于某个阈值则把两个簇合并，数据点出现的次数也合并。重复上述过程直到每个点都标记为已访问。

### 基于密度的聚类方法(DBSCAN)

1. 确定半径r和minPoints
2. 以这个点为中心，r为半径的圆内包含的点的数量是否大于或等于minPoints，如果大于或等于minPoints则改点被标记为central point,反之则会被标记为noise point
3. 重复1的步骤，如果一个noise point存在于某个central point为半径的圆内，则这个点被标记为边缘点，反之仍为noise point。直到每个点访问到。

### 高斯混合模型 GMM

1. 选择簇的数量（与K-Means类似）并随机初始化每个簇的高斯分布参数（均值和方差）。
2. 给定每个簇的高斯分布，计算每个数据点属于每个簇的概率。
3. 基于这些概率我们计算高斯分布参数使得数据点的概率最大化。
4. 重复上述步骤。

## CNN中卷积在图像处理中作用

图像与不同卷积核卷积可用来执行边缘检测、锐化、模糊等操作。

基本参数：卷积大小、卷积核步长（Stride）、填充方式（Padding）、输入通道数、输出通道数

## 池化Pooling

平均池化、最大池化、随机池化

## 模型评价指标

### 混淆矩阵

|| Postive | Negative |
|---| --- | --- |
| True | TP 将正类预测为正类 | TN 将负类预测为负类|
| False | FP 将负类预测为正类的数目 | FN 将正类预测为负类的数目 |

### Precision、Recall、Accuracy、F1 Score

precision = TP / (TP + FP)

recall = TP / (TP + FN)

accuracy = (TP + TN) / (TP + FP + TN + FN)

F1 Score = precision*recall/2(precision+recall)

#### Accuracy准确率

指的是预测正确的样本数/样本数总数

准确率的优点是比较简单直观,缺点是不适用于不平衡数据.

#### Precision精确率或者精度

在我们预测为True的样本里面，有多少确实为True的。

如果我们把一封正常（False）的邮件标记为垃圾邮件（True），这个错误的代价对我们来说太高了,但是如果有一些垃圾邮件没有被标记出来，这个的成本非常低。

#### Recall召回率

实际上为True的样本有多少被我们挑出来了。

#### F1 Score，Accuracy和Recall的调和指标

F1 Score为Accuracy和Recall的调和指标

### ROC（Receiver Operating Characteristic）曲线

受试者工作特征曲线。它的横坐标为TPR（true positive rate），它的纵坐标为FPR（false positive rate）。

### ROC-AUC（arear-under-curve)

ROC曲线与横轴构成的面积。

### PR曲线

纵轴为Precision，横轴为Recall。

改变判区分Positive和Negative的threshold，我们可以得到一系列的Precision和Recall的值。

通过PR曲线来观察在recall多大的时候，precision开始加速下降。这样我们可以利用PR曲线来选择最佳的threshold。

## 特征工程

### 遇到缺值如何处理

- 直接使用含缺值的特征
- 删除含缺值的特征
- 插值补全：均值、总数、中位数、回归、决策树

### 样本不均衡解决办法

- 扩大数据集
- 数据重采样
- 类别均衡采样
  
  根据最多样本对每个样本产生一个随机列表，将其他样本对这个随机列表取余，整合后打乱顺序。最后得到每个样本数目均等。

- 加样本权重

### 样本数据量少解决办法

- 在预处理模型基础上进行微调
- 交叉校验 cross validation
