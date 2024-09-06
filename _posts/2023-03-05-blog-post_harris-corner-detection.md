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

为了更方便地找到角点，定义函数$$R(A_W)$$如下，其中$$\kappa$$的取值范围是 0.04 和 0.10 之间。 
$$R(A_W) = det (A_W) - \kappa {(trace(A_W))}^{2} = (\lambda_1 \times \lambda_2) - \kappa {(\lambda_1 + \lambda_2)}^{2}$$

设定适当的阈值，若$$R(A_W)$$高于该阈值，则该区域包含角点。

处理流程及代码实现
======
第一步，读取图片，将图片转化为单通道的灰度图，然后对其进行高斯模糊。下面是图片处理结果以及代码。除了定义了高斯模糊的函数，还定义了一个对图片的边缘进行像素补充的函数。
<img src='/images/blog/2023-harris-corner-detection/corner-detection-4.png'>

```python
## Read image and convert to grayscale image
import cv2
import matplotlib.pyplot as plt
import numpy as np

img_path = '/path/to/image/file'
img_rgb = cv2.imread(img_path)
img_gray = cv2.cvtColor(img_rgb, cv2.COLOR_BGR2GRAY)
img_gray = img_gray.astype(np.float32)

## generate padding image with padding size, padding mode "mirror"
def padding_img(img, padding_size):
  padding_topleft = img[0: padding_size, 0: padding_size]; padding_topleft = np.flip(padding_topleft, 0); padding_topleft = np.flip(padding_topleft, 1)
  padding_topright = img[0: padding_size, img.shape[1] - padding_size: img.shape[1]]; padding_topright = np.flip(padding_topright, 0); padding_topright = np.flip(padding_topright, 1)
  padding_bottomleft = img[img.shape[0] - padding_size: img.shape[0], 0: padding_size]; padding_bottomleft = np.flip(padding_bottomleft, 0); padding_bottomleft = np.flip(padding_bottomleft, 1)
  padding_bottomright = img[img.shape[0] - padding_size: img.shape[0], img.shape[1] - padding_size: img.shape[1]]; padding_bottomright = np.flip(padding_bottomright, 0); padding_bottomright = np.flip(padding_bottomright, 1)
  
  padding_top = img[0: padding_size, :]; padding_top = np.flip(padding_top, 0)
  padding_bottom = img[img.shape[0] - padding_size: img.shape[0], :]; padding_bottom = np.flip(padding_bottom, 0)
  padding_left = img[:, 0: padding_size]; padding_left = np.flip(padding_left, 1)
  padding_right = img[:, img.shape[1] - padding_size:img.shape[1]]; padding_right = np.flip(padding_right, 1)
  
  img_padding = np.block([[padding_topleft, padding_top, padding_topright],
                          [padding_left, img, padding_right],
                          [padding_bottomleft, padding_bottom, padding_bottomright]])
  
  return img_padding

## apply gaussian filter to the input image
def gaussian_filtering(img, sigma = 1, muu = 0, kernel_size = 3):
  # generate gaussian filter kernel
  x, y = np.meshgrid(np.linspace(-2, 2, kernel_size),
                     np.linspace(-2, 2, kernel_size))
  dst = np.sqrt(x**2 + y**2)
  normal = 1/(2 * np.pi * sigma**2)
  gauss = np.exp(-((dst - muu)**2 / (2.0 * sigma**2))) * normal

  padding_size = int(kernel_size/2)
  img_padding = padding_img(img, padding_size)
  
  img_filtered = np.zeros_like(img)
  
  for i in range(img.shape[0]):
    for j in range(img.shape[1]):
      img_filtered[i][j] = np.sum(np.multiply(img_padding[i: i + kernel_size, j: j + kernel_size], gauss))

  
  return img_filtered

img_filtered = gaussian_filtering(img_gray, kernel_size = 3)
```

第二步，用 Sobel 算子计算图像的水平和垂直方向的梯度。下面是图像处理结果以及代码。
<img src='/images/blog/2023-harris-corner-detection/corner-detection-5.png'>