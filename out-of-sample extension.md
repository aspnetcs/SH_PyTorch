https://blog.csdn.net/qq_43110298/article/details/104571421?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase
在进行降维（dimensionality reduction (DR) ）的学习的时候，发现了一个名词：out-of-sample extension 不太明白这是什么意思，然后发现百度几乎搜不到这些东西，也没有什么国内的博客。但是如果搜索英文“out-of-sample extension”，却可以找到不少的文献。

1 .1 什么是 out-of-sample extension

可见，所谓的out-of-sample extension就是把新的数据直接“嵌入”到训练得到的空间中去（见图中的option 2），而不是把新数据和老数据加起来，在训练或者计算得到一个新的空间、坐标。换句话说：用一部分数据先进行PCA降维，然后得到了降维的投影矩阵W，然后又来了一些新的数据，我们对于新数据的dimensionality reduction (DR)直接用W。

1.2 pca举例
首先，ppt给出了pca算法的过程

然后进行PCA降维处理。蓝色的点为训练用点（已经中心化），绿色的线为新坐标（一维），红色的点为新的点（new data），如下左图。先中心化，然后直接投影，可以得到以下图案。



上图为new data投影后的点。至此out-of-sample extension完成。

所以对于out-of-sample extension来说，步骤如下：


对于ppt的全文，可以关注我的下载中找到。
————————————————
版权声明：本文为CSDN博主「Luna_Lovegood_001」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_43110298/java/article/details/104571421
