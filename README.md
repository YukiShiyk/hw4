# 数字图像处理第四次作业
## 自动化66史玉康
## 2161800034
## language： MATLAB
### 1、空域低通滤波器：分别用高斯滤波器和中值滤波器去平滑测试图像test1和2，模板大小分别是3x3 ， 5x5 ，7x7； 分析各自优缺点；

**中值滤波**

在实时图像采集中，不可避免的会引入噪声，尤其是干扰噪声和椒盐噪声，噪声的存在严重影响边缘检测的效果，中值滤波是一种基于排序统计理论的非线性平滑计数，能有效平滑噪声，且能有效保护图像的边缘信息，所以被广泛用于数字图像处理的边缘提取，其基本原理是把数字图像或数字序列中的一点的值用该点邻域内所有的点排序后的中值来代替。

中值滤波对椒盐噪声有良好的滤除作用，特别是在滤除噪声的同时，能够保护信号的边缘，使之不被模糊。

中值滤波方法是，对待处理的当前像素，选择一个模板3x3、5x5或其他，这里选择3x3矩阵，该模板为其邻近的若干个像素组成，对模板的像素由小到大进行排序，再用模板的中值来替代原像素的值的方法。

当我们使用3x3窗口后获取领域中的9个像素，就需要对9个像素值进行排序，为了提高排序效率，排序算法思想如图所示。

（1）对窗内的每行像素按降序排序，得到最大值、中间值和最小值。

（2）把三行的最小值即第三列相比较，取其中的最大值。

（3）把三行的最大值即第一列相比较，取其中的最小值。

（4）把三行的中间值即第二列相比较，再取一次中间值。

（5）把前面的到的三个值再做一次排序，获得的中值即该窗口的中值。

**处理结果**

<img src="https://github.com/YukiShiyk/hw4/blob/master/image/中值滤波1.png" width = "300" height = "300" div align=center /><img src="https://github.com/YukiShiyk/hw4/blob/master/image/中值滤波2.png" width = "300" height = "300" div align=center />

**结果分析**

中值滤波的功能是使拥有不同灰度的点更接近它的相邻点。事实上，使用m*m中值滤波器来去除那些相对于其邻域像素更亮或更暗并且其区域小于m^2/2的孤立像素族。在这种情况下，“去除”的意思是强制为邻域的中值灰度。较大的族所受到的影响较小。

观察处理后的图像发现，图像的平滑效果较为明显，且受窗口的影响，窗口越大，平滑效果越明显，图像细节越模糊。优点是可以使图像变得更加平滑，缺点是图像的细节会变得模糊，比如test2中的眼部细节会随着滤波器模块的增大变得越来越模糊。

**高斯滤波**

高斯滤波是一种线性平滑滤波，适用于消除高斯噪声，广泛应用于图像处理的减噪过程。通俗的讲，高斯滤波就是对整幅图像进行加权平均的过程，每一个像素点的值，都由其本身和邻域内的其他像素值经过加权平均后得到。高斯滤波的具体操作是：用一个模板（或称卷积、掩模）扫描图像中的每一个像素，用模板确定的邻域内像素的加权平均灰度值去替代模板中心像素点的值。

**处理结果**

<img src="https://github.com/YukiShiyk/hw4/blob/master/image/高斯滤波1.png" width = "300" height = "300" div align=center/><img src="https://github.com/YukiShiyk/hw4/blob/master/image/高斯滤波2.png" width = "300" height = "300" div align=center/>

<img src="https://github.com/YukiShiyk/hw4/blob/master/image/高斯滤波3.png" width = "300" height = "300" div align=center/><img src="https://github.com/YukiShiyk/hw4/blob/master/image/高斯滤波4.png" width = "300" height = "300" div align=center/>

**结果分析**

从处理后的图像来看，图像的平滑效果较为明显，且受窗口的影响，窗口越大，平滑效果越明显，图像细节越模糊。（此处于中值滤波的效果相似）

### 利用固定方差 sigma=1.5产生高斯滤波器. 附件有产生高斯滤波器的方法； 分析各自优缺点；

此问处理方式及处理结果同问题一第二部分，只不过将高斯分布的sigma值固定为1.5
<img src="https://github.com/YukiShiyk/hw4/blob/master/image/2.1.png" width = "300" height = "300" div align=center/>
<img src="https://github.com/YukiShiyk/hw4/blob/master/image/2.2.png" width = "300" height = "300" div align=center/>

**处理结果**

### 利用高通滤波器滤波测试图像test3,4：包括unsharp masking, Sobel edge detector, and Laplace edge detection；Canny algorithm.分析各自优缺点；

锐化滤波能减弱或消除图像的低频率分量，但不影响高频率分量。因为低频率分量对应图像中灰度值缓慢变化的区域，因为与图像的整体特性，如整体对比度和平均灰度值等有关。锐化滤波将这些分量滤去可使图像反差增加，边缘明显。在实际应用中，锐化滤波的主要目的是突出灰度的过渡部分。补偿轮廓，增强图像的边缘及灰度跳变的部分，使图像变得清晰。

**处理结果**

<img src="https://github.com/YukiShiyk/hw4/blob/master/image/3.1.png" width = "300" height = "300" div align=center/><img src="https://github.com/YukiShiyk/hw4/blob/master/image/3.2.png" width = "300" height = "300" div align=center/>

**结果分析与总结**

①反锐化掩模的处理结果得到了边缘更加清晰的图像，与预期改进结果一致。但同时看到也会引进一些不希望看到的噪声。

②Sobel operator是图像处理中的算子之一，主要用于边缘检测。由于sobel算子是滤波算子的形式，用于提取边缘，可以利用快速卷积函数。缺点是sobel算子并没有将图像的主体与背景严格地区分开来，即其没有基于图像灰度进行处理，观察处理结果可发现其没有很好地将图像边缘完全分离出来。

③拉普拉斯算子是一种微分算子，其应用强调的是图像中灰度的突变，并不强调灰度级缓慢变化的区域。这将产生把浅灰色边线和突变点叠加到暗色背景中的图像。结合处理后的图像观察，拉普拉斯算子对于test3的边缘检测结果较为理想，而对于test4的检测结果则不尽如人意。

④canny函数可以将图像的边缘检测出来。







