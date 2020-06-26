numpy中np.finfo用法

~华仔呀 2020-03-10 13:52:24  857  收藏 3
分类专栏： python
版权
例子：
"""
np.finfo使用方法
    eps是一个很小的非负数
    除法的分母不能为0的,不然会直接跳出显示错误。
    使用eps将可能出现的零用eps来替换，这样不会报错。
"""
import numpy as np
 
x = np.array([1, 2, 3], dtype=float)
eps = np.finfo(x.dtype).eps  # eps = 2.220446049250313e-16 type = <class 'numpy.float64'>
print(eps, type(eps))
height = np.array([0, 2, 3], dtype=float)
height = np.maximum(height, eps) #一旦height中出现0，就用eps进行替换
print(height)   #[2.22044605e-16 2.00000000e+00 3.00000000e+00]
dy = x / height

————————————————
版权声明：本文为CSDN博主「~华仔呀」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/minhuaQAQ/java/article/details/104773022
