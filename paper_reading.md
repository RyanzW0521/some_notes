## PAPER READING
##### **2021/11/19-2021/11/26**
#### 1. Image Segmentation Techniques Overview
> 图像分割技术广泛应用于医学图像处理、人脸识别、行人检测等领域。目前的图像分割技术包括基于区域的分割、边缘检测分割、基于聚类的分割、基于CNN中的弱监督学习的分割等。本文对这些图像分割算法进行了分析和总结，并比较了不同算法的优缺点。最后，结合这些算法对图像分割的发展趋势进行了预测

* 对于一些图像分割技术做了简略的说明，不过比较多的可能用于物体检测上吧，我个人认为血管分割相对来说更加的细致，但或许又不需要整体的图像目标定位，所以可能更需要 __边缘检测技术__。
* 这里头提到的边缘检测技术中一个很有用的应该是 __基于弱监督的CNN学习__。DCNN的弱监督和半监督学习用于语义分割。相对来说我觉得还是语义分割较好理解，然而语义分割对每个像素点都有要求，全监督学习成本太大，他这里头提出的弱监督和半监督方法我后续可以重点看一看

#### 2.Fully Convolutional Networks for Semantic Segmentation
> 卷积网络是一种功能强大的视觉模型，可以产生层次化的特征。我们证明了卷积网络本身，经过端到端、像素到像素的训练，在语义分割方面超越了目前的先进水平。我们的关键见解是构建“完全卷积”网络，它接受任意大小的输入，并产生相应大小的输出，并具有有效的推理和学习。我们定义并详细说明了全卷积网络的空间，解释了它们在空间密度预测任务中的应用，并将其与之前的模型联系起来。我们将当代分类网络(AlexNet，VGGnet和GoogLeNet)调整为完全卷积网络，并通过微调[3]将学到的表示转移到分割任务中。然后，我们定义了一个askip架构，该架构将深层粗层的语义信息与浅层细层的外观信息相结合，生成准确而详细的分割。
  
* 十分经典的关于语义分割的论文。主要介绍了语义分割的构成、用法以及相关的概念和工作。
* 重点强调了FCN的应用。目前似乎主流为UNet以及SegNet等网络，待比较相关优缺点
*  __Global__ 和 __local__ 在图像识别领域的定义尚不清楚。最近看的一些关于ResNet的论文也有提到他们，待解决。


#### 3.Machine Learning Applications of Convolutional Neural Networks and Unet Architecture to Predict and Classify Demosponge Behavior
> 生物数据集的信息量越来越大，这使得基于计算机科学的分析变得更加有效。我们使用卷积神经网络(CNN)和特定的CNN架构Unet来研究海绵随时间的行为。我们分析了2012年至2015年利用加拿大温哥华岛西海岸外的海王星海底电缆观测站拍摄的、每小时高分辨率的海洋海绵Suberites concinus (Demospongiae, Suberitidae)静止图像的大时间序列。我们对Unet架构进行了一些修改，并应用了语义分割，包括对架构的部分进行了调整，使其更适用于三通道图像(RGB)。使这个模型成功的一些改变是使用了advice -loss系数，Adam优化器和在每个卷积层后的dropout函数，这些函数分别提供了损失，精确度和骰子得分高达0.03,0.98和0.97。对模型进行了5次交叉验证。这项研究是分析在经历了严重的季节和年际气候变化的环境中demosponge行为趋势的第一步。
	
* 很受用的一篇论文，虽然只是简单地使用了UNet，但是对于它应用在具体的实战方面给我的启发还是很多的。提到了很多在实战中需要注意的点，比如提到了掩码的使用，此前我对之了解不多，之前在GitHub上找到的一些UNet做裂缝分割的代码就有联合matlab的mask使用。但是当时不理解用来干啥的，readme里也无详细说明。本文对此进一步解释了一下。
* 很有用的一个角度是，本文通过信号处理的角度来理解了CNN和UNet。以滤波器来看待卷积层，之前很多想不通的地方也能够很好的解释了。

#### 4.SegNet: A Deep ConvolutionalEncoder-Decoder Architecture for SceneSegmentation
> 我们提出了一种新颖实用的深度全卷积神经网络结构，用于基于像素的语义分割，称为SegNet。这个核心可训练的分割引擎由一个编码器网络，一个相应的解码器网络和一个像素分类层组成。编码器网络的结构在拓扑上与vgg16网络[1]中的13个卷积层相同。解码器网络的作用是将低分辨率的编码器特征映射到全输入分辨率特征映射，以便逐像素分类。 __*SegNet的新颖之处在于解码器向上采样其较低分辨率的输入特征图的方式*__ 。具体来说，解码器使用在相应编码器的最大池化步骤中计算的池化指标来执行非线性上采样。这就消除了学习上采样的需要。上采样的地图是稀疏的，然后与可训练的滤波器卷积，产生密集的特征地图。我们将我们提出的架构与广泛采用的FCN，也与著名的deelab-largefov，DeconvNet架构进行比较。这个比较揭示了在实现良好的分割性能时所涉及的内存和准确性之间的权衡。

* SegNet去掉了VGG16的全联接层，显得更为精简，也减少了运算量。
* 不同于其他学习方法，深度编码器网络作为监督学习任务联合训练，解码器在测试的时候是网络的组成部分。别的一些网路在编码器训练后就丢弃了解码器（如Ranzatoet架构）
* 提到了关于图像的一些前期处理，比如边界划定，因为特征图的空间分辨率会下降，越来越多的有损图像不利于分割。
* 提到了很多次sift算法和CRF，这两个概念我的了解还不是很深入。
> 作者在[50]中讨论了学习从低分辨率特征地图向上采样的必要性，这是本文的中心话题ARCHITECTURESegNet有一个编码器网络和一个相应的解码器网络，然后是最后一个像素级分类层。编码器网络由13个卷积层组成，对应于为对象分类而设计的VGG16网络中的第一个13个卷积层。因此，我们可以通过在大数据集上训练权重来初始化分类的训练过程。我们也可以放弃全连接层，以便在编码器输出的最深处保留更高分辨率的特征图。与其他最近的架构相比，这也显著减少了SegNet编码器网络中的参数数量(从134M减少到14.7M)。每个编码器层有一个相应的解码器层，因此解码器网络有13层。最后的解码器输出被输入到一个多类软最大分类器，以独立产生每个像素的类概率。
！[avatar](/Users/jiangdu/Desktop/截屏2021-11-25 下午10.47.18.png)

#### 5.基于卷积神经网络的眼底图像配准研究
> 传统眼底图像配准⽅法提取的特征点分布过于密集，导致配准图像⽆法准确对⻬，⽽眼底⾎管分叉特征点具有分布稀疏和特征稳定等特性，能提⾼图像的配准精度和速度。因此，本⽂针对⾎管分割和分叉特征点提取，提出⼀个基于深度学习的眼底图像配准框架。这个框架由7个深度卷积神经⽹络组成:第⼀个是眼底⾎管分割⽹络SR-UNet，其在UNet的基础上融合通道注意⼒(SE)和残差块，⽤于分割⾎管去辅助提取特征点; 第⼆个是特征点检测⽹络 FD-Net，⽤于从⾎管分割图中提取分叉特征点，提出的配准模型在公共眼底配准数据集FIRE上进⾏实验。与较先进的算法进⾏对⽐，本⽂提出的算法在配准定量和视觉分析上都有较好的性能提升，具有较强的鲁棒性

* 和我的课题方向几乎一致，这个课题组大刀阔斧的对现有的卷积网络进行了改进。着重点在于把ResNet和SeNEt结合了起来，然后引入了改进的UNet左右对称编码解码模型作为基本架构。好处是能够把残差块和注意力通道机制结合，能够实现带通道权重的残差学习。
* 提出了对我很有用的数据预处理方法，因为眼底血管图像比较少，数据集不够大，容易过拟合，他们把眼底图像随机裁剪为48*48像素的图像块，这样可以生成约200k张图像块作为train_dataset。
* 一个疑问是，本文使用特征提取网络是为了最后能够配准，我似乎不需要这一步，但是可以考虑把它和分割网络**结合**一下？只是一个猜想。

#### 6.用于脑组织分割的多尺度注意网络
> 基于脑组织分割的精确头模型有助于提升经颅磁刺激的治疗效果，但是由于人脑的复杂性，很难实现精确的脑组织分割。为此，本文提出了基于迁移学习的多尺度注意网络，该网络可以学习多模态数据之间的互补信息，采用迁移学习的方法解决了小样本数据引起的过拟合问题，利用膨胀卷积提取并融合多尺度特征，加入注意力机制聚焦重要特征信息， 提高了脑组织分割的准确性。 多尺度注意网络可以为个性化头模型的建立提供一个较好的分割结果，进而优化经颅磁刺激的治疗效果

* 在引言提到了多模态聚合网络来提高分割效果，这个可以以后看一看
* 本文主要是对于样本数据过少而提出的基于迁移学习的方法。选用空洞卷积获取不同尺度的特征信息，融合特征图的高低感受野，利用注意力机制聚焦多尺度特征融合后的感兴趣区域， 进而提高分割精度。
* 提到了多尺度特征融合模块和CBAM注意力机制模块，前者我涉猎不多，尚难以理解；后者提到了空间注意力，也有待我学习。