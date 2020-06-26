Matlab：分位数函数prctile
已有 16039 次阅读 2017-6-1 23:44 |个人分类:Matlab|系统分类:科研笔记| MATLAB, 分位数, prctile函数

比如a = [1 2 3 4 5 6 7 8 9 10]；

先对a排序，b=sort(abs(a))；

95%分位数 y = prctile(b,95)；

68%分位数 y = prctile(b,68)；
