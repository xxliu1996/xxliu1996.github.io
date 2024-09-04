---
title: "Deep Learning Based Fluorescence-to-Color Image Registration "
excerpt: "In this project, we built a fluorescence imaging system to captuer both color image and fluorescence image. We achieved fluorescence-to-color image registration with image features extracted by VGG-16.<br/><img src='/images/Project-Fluorescence-to-Color-Image-Registration.png'>"
collection: projects
---

In this project, we built a fluorescence imaging system which can capture both color image and fluorescence image. We used VGG-16 to extract features from color image and fluorescence image to build feature descriptors. Then keypoint matching was performed based on Nearest Neighbor Search (NNS) on the feature descriptor space. After that, the transformation from fluorescence image to color image was calculated. Finally, we applied the transformation to the fluorescence image and overlaid the fluorescence signal onto the color image. 