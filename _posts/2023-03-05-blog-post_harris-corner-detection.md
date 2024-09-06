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

所以，对于图像中的某个点，我们需要一个函数，来衡量包含该点的窗口内的像素平均值对滑动的敏感度。对于窗口$$W$$和位移$$\Delta$$，定义窗口函数$$S_{W}$$。该函数计算窗口沿着某个方向移动后，窗口内的每个点的像素变化值的平方和。

$$\Delta = [\Delta x, \Delta y]$$

$$S_{W}(\Delta) = \sum_{(x_i, y_i) \in W}^{}{(f(x_i, y_i) - f(x_i + \Delta x, y_i + \Delta y))}^{2}$$

用泰勒展开公式，可以得到如下
$$f(x_i + \Delta x, y_i + \Delta y) \approx f(x_i, y_i) + [\frac{\partial{f(x_i, y_i)}}{\partial{x}} ,\frac{\partial{f(x_i, y_i)}}{\partial{y}}]{[\Delta x , \Delta y]}^{T}$$

$$S_{W}(\Delta) = \sum_{(x_i, y_i) \in W}^{}[\Delta x, \Delta y]({[\frac{\partial{f(x_i, y_i)}}{\partial{x}} ,\frac{\partial{f(x_i, y_i)}}{\partial{y}}]}^{T}[\frac{\partial{f(x_i, y_i)}}{\partial{x}} ,\frac{\partial{f(x_i, y_i)}}{\partial{y}}]){[\Delta x , \Delta y]}^{T}$$

$$
= [\Delta x , \Delta y]
\begin{bmatrix}  
\sum_{(x_i, y_i) \in W}{{(\frac{\partial{f(x_i, y_i)}}{\partial{x}})}^{2}} & \sum_{(x_i, y_i) \in W}{\frac{\partial{f(x_i, y_i)}}{\partial{x}}} {\frac{\partial{f(x_i, y_i)}}{\partial{y}}}
\end{bmatrix} 
{[\Delta x , \Delta y]}^{T} 
$$