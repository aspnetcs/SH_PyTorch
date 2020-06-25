拉普拉斯特征映射（Laplacian Eigenmaps）

qrlhl 2017-09-22 21:11:18  23147  收藏 31
分类专栏： 机器学习
版权
1、介绍
拉普拉斯特征映射（Laplacian Eigenmaps）是一种不太常见的降维算法，它看问题的角度和常见的降维算法不太相同，是从局部的角度去构建数据之间的关系。也许这样讲有些抽象，具体来讲，拉普拉斯特征映射是一种基于图的降维算法，它希望相互间有关系的点（在图中相连的点）在降维后的空间中尽可能的靠近，从而在降维后仍能保持原有的数据结构。
本文参考http://blog.csdn.net/xbinworld/article/details/8855796。

2、推导
拉普拉斯特征映射通过构建邻接矩阵为WW（邻接矩阵定义见这里）的图来重构数据流形的局部结构特征。其主要思想是，如果两个数据实例ii和jj很相似，那么ii和jj在降维后目标子空间中应该尽量接近。设数据实例的数目为nn，目标子空间即最终的降维目标的维度为mm。定义n×mn×m大小的矩阵YY，其中每一个行向量yTiyiT是数据实例ii在目标mm维子空间中的向量表示（即降维后的数据实例ii）。我们的目的是让相似的数据样例ii和jj在降维后的目标子空间里仍旧尽量接近，故拉普拉斯特征映射优化的目标函数如下：


min∑i,j||yi−yj||2Wijmin∑i,j||yi−yj||2Wij
下面开始推导：

∑i=1n∑j=1n||yi−yj||2Wij=∑i=1n∑j=1n(yTiyi−2yTiyj+yTjyj)Wij=∑i=1n(∑j=1nWij)yTiyi+∑j=1n(∑i=1nWij)yTjyj−2∑i=1n∑j=1nyTiyjWij=2∑i=1nDiiyTiyi−2∑i=1n∑j=1nyTiyjWij=2∑i=1n(Dii−−−√yi)T(Dii−−−√yi)−2∑i=1nyTi(∑j=1nyjWij)=2trace(YTDY)−2∑i=1nyTi(YW)i=2trace(YTDY)−2trace(YTWY)=2trace[YT(D−W)Y]=2trace(YTLY)
∑i=1n∑j=1n||yi−yj||2Wij=∑i=1n∑j=1n(yiTyi−2yiTyj+yjTyj)Wij=∑i=1n(∑j=1nWij)yiTyi+∑j=1n(∑i=1nWij)yjTyj−2∑i=1n∑j=1nyiTyjWij=2∑i=1nDiiyiTyi−2∑i=1n∑j=1nyiTyjWij=2∑i=1n(Diiyi)T(Diiyi)−2∑i=1nyiT(∑j=1nyjWij)=2trace(YTDY)−2∑i=1nyiT(YW)i=2trace(YTDY)−2trace(YTWY)=2trace[YT(D−W)Y]=2trace(YTLY)

其中WW是图的邻接矩阵，对角矩阵DD是图的度矩阵（Dii=∑nj=1WijDii=∑j=1nWij），L=D−WL=D−W成为图的拉普拉斯矩阵。
变换后的拉普拉斯特征映射优化的目标函数如下：


mintrace(YTLY),s.t.YTDY=Imintrace(YTLY),s.t.YTDY=I
其中限制条件s.t.YTDY=Is.t.YTDY=I保证优化问题有解，下面用拉格朗日乘子法对目标函数求解：

f(Y)=tr(YTLY)+tr[Λ(YTDY−I)]∂f(Y)∂Y=LY+LTY+DTYΛT+DYΛ=2LY+2DYΛ=0∴LY=−DYΛ
f(Y)=tr(YTLY)+tr[Λ(YTDY−I)]∂f(Y)∂Y=LY+LTY+DTYΛT+DYΛ=2LY+2DYΛ=0∴LY=−DYΛ

其中用到了矩阵的迹的求导，具体方法见迹求导。ΛΛ为一个对角矩阵，另外LL、DD均为实对称矩阵，其转置与自身相等。对于单独的yy向量，上式可写为：Ly=λDyLy=λDy,这是一个广义特征值问题。。通过求得mm个最小非零特征值所对应的特征向量，即可达到降维的目的。
关于这里为什么要选择mm个最小非零特征值所对应的特征向量，下面评论中的大佬指出，将LY=−DYΛLY=−DYΛ带回到mintrace(YTLY)mintrace(YTLY)中，由于有着约束条件YTDY=IYTDY=I的限制，可以得到mintrace(YTLY)=mintrace(−Λ)mintrace(YTLY)=mintrace(−Λ)。即为特征值之和。我们为了目标函数最小化，要选择最小的mm个特征值所对应的特征向量。

3、步骤
使用时算法具体步骤为：

步骤1：构建图

使用某一种方法来将所有的点构建成一个图，例如使用KNN算法，将每个点最近的K个点连上边。K是一个预先设定的值。

步骤2：确定权重

确定点与点之间的权重大小，例如选用热核函数来确定，如果点ii和点jj相连，那么它们关系的权重设定为：

Wij=e−||xi−xj||2tWij=e−||xi−xj||2t
另外一种可选的简化设定是Wij=1Wij=1如果点ii，jj相连，否则Wij=0Wij=0。

步骤3：特征映射

计算拉普拉斯矩阵L的特征向量与特征值：Ly=λDyLy=λDy
使用最小的m个非零特征值对应的特征向量作为降维后的结果输出。

4、实例


上图所示左边的图表示有两类数据点（数据是图片），中间图表示采用拉普拉斯特征映射降维后每个数据点在二维空间中的位置，右边的图表示采用PCA并取前两个主要方向投影后的结果，可以清楚地看到，在此分类问题上，拉普拉斯特征映射的结果明显优于PCA。



上图说明的是高维数据（图中3D）也有可能是具有低维的内在属性的（图中Swiss roll实际上是2D的），但是这个低维不是原来坐标表示，例如如果要保持局部关系，蓝色和下面黄色是完全不相关的，但是如果只用任何2D或者3D的距离来描述都是不准确的。

下面的三个图是拉普拉斯特征映射在不同参数下的展开结果（降维到2D），可以看到，似乎是要把整个卷拉平了，蓝色和黄色差的比较远，很好地保留了数据原有的结构。
————————————————
版权声明：本文为CSDN博主「qrlhl」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qrlhl/java/article/details/78066994
