---
title: 'Harris角点检测Python实现'
date: 2023-03-05
permalink: /posts/2023/03/blog-post-harris-corner-detection/
tags:
  - 求职
  - 美国留学
  - 实习
---
<img src='/images/blog/2023-harris-corner-detection/corner-detection-1.jpeg'>

图像处理作业，分享出来。不足之处，多多见谅。欢迎提出改进意见。

原理
======
所谓角点，即为边的交点。在图像中，创建一个包含角点的局部窗口，那么将该窗口按照任意方向滑动，窗口内的像素平均值都会发生比较大的变化。如果窗口在像素变化平缓的区域内滑动，窗口内的像素平均值不会显著变化；如果窗口在包含边的区域内滑动，沿着边的方向滑动，窗口内的像素平均值不会显著变化，而沿着垂直于边的方向滑动，窗口内的像素平均值会发生较大的变化。
<img src='/images/blog/2023-harris-corner-detection/corner-detection-2.png'>

所以，对于图像中的某个点，我们需要一个函数，来衡量包含该点的窗口内的像素平均值对滑动的敏感度。对于窗口$$W$$和位移$$\Delta$$，定义窗口函数$$S_{W}$$。该函数计算窗口沿着某个方向移动后，窗口内的每个点的像素变化值的平方和。

$$\Delta = [\Delta x, \Delta y]$$

$$S_{W}(\Delta) = \sum_{(x_i, y_i) \in W}^{}{(f(x_i, y_i) - f(x_i + \Delta x, y_i + \Delta y))}^{2}$$

用泰勒展开公式，可以得到

$$
f(x_i + \Delta x, y_i + \Delta y) \approx f(x_i, y_i) + 
\begin{bmatrix}
\frac{\partial f(x_i, y_i)}{\partial x} & \frac{\partial f(x_i, y_i)}{\partial y}
\end{bmatrix}
\begin{bmatrix}
\Delta x \\
\Delta y
\end{bmatrix}
$$

$$
S_W(\Delta) = \sum_{(x_i,y_i)\in W} [\Delta x, \Delta y]
\left[ 
\begin{array}{cc}
\left(\frac{\partial f(x_i,y_i)}{\partial x}\right)^2 & \frac{\partial f(x_i,y_i)}{\partial x} \frac{\partial f(x_i,y_i)}{\partial y} \\
\frac{\partial f(x_i,y_i)}{\partial x} \frac{\partial f(x_i,y_i)}{\partial y} & \left(\frac{\partial f(x_i,y_i)}{\partial y}\right)^2
\end{array}
\right]
[\Delta x, \Delta y]^T
$$

$$
S_W(\Delta) = [\Delta x, \Delta y] \left[
\begin{array}{cc}
\sum_{(x_i,y_i)\in W} \left(\frac{\partial f(x_i,y_i)}{\partial x}\right)^2 & \sum_{(x_i,y_i)\in W} \frac{\partial f(x_i,y_i)}{\partial x} \frac{\partial f(x_i,y_i)}{\partial y} \\
\sum_{(x_i,y_i)\in W} \frac{\partial f(x_i,y_i)}{\partial x} \frac{\partial f(x_i,y_i)}{\partial y} & \sum_{(x_i,y_i)\in W} \left(\frac{\partial f(x_i,y_i)}{\partial y}\right)^2
\end{array}
\right]
[\Delta x, \Delta y]^T
$$

$$
S_W(\Delta) = [\Delta x, \Delta y] A_W (x, y) [\Delta x, \Delta y]^T
$$

矩阵$$A_W(x, y)$$被称为 Harris 矩阵，它是一个对称矩阵，也是一个半正定矩阵。所以，可以求解该矩阵的特征值和特征向量。这两个特征值$$(\lambda_1 , \lambda_2)$$可以体现窗口$$W$$内图像梯度沿着特征向量的变化幅度。基于$$(\lambda_1 , \lambda_2)$$的取值，可以将窗口$$W$$包含区域分为三种情形。

* $$\lambda_1$$和$$\lambda_2$$都很小：没有边或者角点，窗口$$W$$所包围的是一个像素均匀分布和缓慢变化的区域。
* $$\lambda_1$$和$$\lambda_2$$都很小：窗口$$W$$所包围的区域存在边，没有角点。
* $$\lambda_1$$和$$\lambda_2$$都很小：窗口$$W$$所包围的区域存在角点。

<img src='/images/blog/2023-harris-corner-detection/corner-detection-3.png'>