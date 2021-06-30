## A data mapping method for roadside LiDAR sensors

## 一种路测激光雷达的数据映射方法

这篇论文主要是将GPS与激光雷达的位置进行转化，进而可以得到激光雷达所测信息的位置。

主要分为：参考点匹配；变换矩阵计算；激光雷达数据坐标转换。

通过最小二乘法进行求解，参考点至少是四个，通过超定系统来进行求解。

#### 参考点匹配：大地坐标到空间直角坐标转换

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190418085024305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYzNzQ5MA==,size_16,color_FFFFFF,t_70)

大地坐标系以纬度B、经度L、大地高H描述一点的空间位置。纬度的定义是某点的地面法线与赤道面的夹角，以赤道面为起算点，向南为负，范围为-90°~0°，向北为正，范围为0°~90°；经度L由起始大地子午面起算，向东为正，向西为负，范围是-180°~180°。某点沿法线到椭球面的距离称为该点的大地高H。

参心空间直角坐标系以椭球中心O为坐标原点，以起始子午面与赤道面的交线为X轴，在赤道面上与X轴正交的方向为Y轴，椭球的旋转轴为Z轴，三个方向呈右手系。

已知某点的大地坐标（B、L、H），可按下式转换为空间直角坐标（X，Y，Z）：

![[公式]](https://www.zhihu.com/equation?tex=X%3D%28N%2BH%29cosBcosL%EF%BC%881%EF%BC%89+%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=Y%3D%28N%2BH%29cosBsinL+%EF%BC%882%EF%BC%89+%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=Z%3D%28N%281-e%5E2%29%2BH%29sinB%EF%BC%883%EF%BC%89+%5C%5C)

其中，![[公式]](https://www.zhihu.com/equation?tex=N)为卯酉圈半径，![[公式]](https://www.zhihu.com/equation?tex=e)是地球的第一偏心率。令参考椭球的赤道半径为![[公式]](https://www.zhihu.com/equation?tex=a)，参考椭球的极半径为![[公式]](https://www.zhihu.com/equation?tex=b)。在参考椭球的定义中，![[公式]](https://www.zhihu.com/equation?tex=a)大于![[公式]](https://www.zhihu.com/equation?tex=b)。则：

![[公式]](https://www.zhihu.com/equation?tex=e%5E2%3D%28a%5E2-b%5E2%29%2Fa%5E2%EF%BC%884%EF%BC%89+%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=N+%3D+a%2F%281-e%5E2sin%5E2B%29%5E%7B%5Cfrac%7B1%7D%7B2%7D%7D%EF%BC%885%EF%BC%89+%5C%5C)

#### 变换矩阵计算

将两个空间直角坐标系进行转化，里面包括：尺度变换，对称变换，旋转变换，平移变换，投影变换。将5个变换进行合并，得到转换矩阵T。![image-20210531151314479](https://user-images.githubusercontent.com/71913439/123905167-622e5680-d9a4-11eb-976d-9c613a1d5ebc.png)

最小二乘

假设参考点个数为m，矩阵A表示LiDAR采集到的(x, y, z)信息，矩阵B表示变换后的(x, y, z)信息，可以用(x, y,  z)表示，超定系统可以表示为![image-20210531151428129](https://user-images.githubusercontent.com/71913439/123905548-23e56700-d9a5-11eb-9032-1a69390e245b.png)

其中

![image-20210531151455353](https://user-images.githubusercontent.com/71913439/123905412-dff26200-d9a4-11eb-963b-39b285b25ca8.png)![image-20210531151621801](https://user-images.githubusercontent.com/71913439/123905442-f00a4180-d9a4-11eb-8c6f-2339d0ed0c33.png)

![image-20210531152039711](https://user-images.githubusercontent.com/71913439/123905492-07e1c580-d9a5-11eb-8b55-05f7a06bf293.png)






#### 激光雷达坐标转换

将激光雷达坐标转换为大地坐标系。

已知空间直角坐标（X，Y，Z),由以上公式可得：

![[公式]](https://www.zhihu.com/equation?tex=tanL%3D%5Cfrac%7BY%7D%7BX%7D%EF%BC%886%EF%BC%89+%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=tanB%3D%5Cfrac%7BZ%2BNe%5E2sinB%7D%7B%28X%5E2%2BY%5E2%29%5E%7B%5Cfrac%7B1%7D%7B2%7D%7D%7D%EF%BC%887%EF%BC%89+%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=H%3D%5Cfrac%7B%28X%5E2%2BY%5E2%29%5E%5Cfrac%7B1%7D%7B2%7D%7D%7BcosB%7D-N%EF%BC%888%EF%BC%89+%5C%5C)











