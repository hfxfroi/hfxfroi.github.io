---
layout: post
title: Bray-Curtis 距离矩阵
category: R
tags: [Bray-Curtis]
---

```
library(vegan)

# 参数设置
Args <- commandArgs()
# 读入数据
data <- read.table(Args[6], sep='\t', head=T)

# apply函数有3个参数：
# apply(data,margin,function)
# a. 第一个为输入的数据，要求为矩阵或者数据框的形式
# b. 第二个参数指的是按行还是按列来进行计算，为1时是按行进行计算，为2时是按列进行计算
# c. 第三个参数指的是使用什么函数

# 数据标准化
# data[,-1]：去掉data的第一个列
# 2：对列进行操作
data_normalize <- apply(data[,-1], 2, function(x) x/sum(x)*1)

# 计算距离矩阵
dist_bray <- vegdist(t(data_normalize), method='bray')
dist_bray

# 写入文件
write.table(as.matrix(dist_bray), Args[7], raw.names=TRUE, sep='\t', quote=FALSE)
```


运行程序 `Rscript bray_distance.r input output`
