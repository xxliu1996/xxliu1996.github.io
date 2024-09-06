---
permalink: /
title: "About Me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---
I am a 5th year Ph.D. student majoring in Electrical and Computer Engineering at University of Iowa. I am actively looking for Machine Learning/Deep Learning/Computer Vision/Medical Image Analysis/Software Development Engineer internship positions for 2024 Summer.  
 
My research lies in surgical navigation, deep learning, computer vision, medical image processing. My goal is incorporating cutting-edge technologies into surgical navigation systems. In my projects, I applied deep learning to medical image processing, including spine segmentation, fluorescence-to-color image registration. My current project focuses on incorporating 3D surgical tool tracking techinque into our fluorescence imaging surgical navigation system. These projects help me to develop solidate skills on C/C++/Python programming, deep network implementation with Pytorch/Tensorflow, CT/MRI processing, etc.  
 
Also, I have devloped additional skills on C#/Matlab/HTML/JavaScript programming, Unity game development, using 3D Slicer/ImageJ to process medical images, 3D CAD design, 3D printing, etc. 

<style>
* {
  box-sizing: border-box;
}

body {
  background-color: white; /* Changed to white */
  font-family: Helvetica, sans-serif;
}

/* The actual timeline (the vertical ruler) */
.timeline {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
}

/* The vertical ruler */
.timeline::after {
  content: '';
  position: absolute;
  width: 6px;
  background-color: light gray; /* Changed to light gray */
  top: 0;
  bottom: 0;
  left: 50%;
  margin-left: -3px; /* Keep the ruler centered */
}

/* Container around content */
.container {
  padding: 10px 40px;
  position: relative;
  background-color: inherit;
  width: 50%;
}

/* The circles on the timeline */
.container::after {
  content: '';
  position: absolute;
  width: 25px;
  height: 25px;
  right: -13px; /* Adjusted to center the circle */
  background-color: black; /* Changed to black */
  border: 4px solid gray; /* Changed border to gray */
  top: 15px;
  border-radius: 50%;
  z-index: 1;
}

/* Place the container to the left */
.left {
  left: 0;
}

/* Place the container to the right */
.right {
  left: 50%;
}

/* Add arrows to the left container (pointing right) */
.left::before {
  content: " ";
  height: 0;
  position: absolute;
  top: 22px;
  width: 0;
  z-index: 1;
  right: 30px;
  border: medium solid white;
  border-width: 10px 0 10px 10px;
  border-color: transparent transparent transparent white;
}

/* Add arrows to the right container (pointing left) */
.right::before {
  content: " ";
  height: 0;
  position: absolute;
  top: 22px;
  width: 0;
  z-index: 1;
  left: 30px;
  border: medium solid white;
  border-width: 10px 10px 10px 0;
  border-color: transparent white transparent transparent;
}

/* Fix the circle for containers on the right side */
.right::after {
  left: -13px; /* Adjusted to center the circle */
}

/* The actual content */
.content {
  padding: 20px 30px;
  background-color: white;
  border: 2px solid gray; /* Changed border to gray */
  position: relative;
  border-radius: 6px;
}

/* Media queries - Responsive timeline on screens less than 600px wide */
@media screen and (max-width: 600px) {
  /* Place the timeline to the left */
  .timeline::after {
  left: 31px;
  }
  
  /* Full-width containers */
  .container {
  width: 100%;
  padding-left: 70px;
  padding-right: 25px;
  }
  
  /* Make sure that all arrows are pointing leftwards */
  .container::before {
  left: 60px;
  border: medium solid white;
  border-width: 10px 10px 10px 0;
  border-color: transparent white transparent transparent;
  }

  /* Make sure all circles are at the same spot */
  .left::after, .right::after {
  left: 15px;
  }
  
  /* Make all right containers behave like the left ones */
  .right {
  left: 0%;
  }
}
</style>

News
======
<div class="timeline">
  <div class="container left">
    <div class="content">
      <h2>2024-08-23</h2>
      <p>Xingxing Liu just finished his second internship at Alcon Laboratories locating at Lake Forest, CA.</p>
    </div>
  </div>
  <div class="container right">
    <div class="content">
      <h2>2019-08-12</h2>
      <p>Xingxing Liu just joined University of Iowa as a Ph.D. student at department of Electrical and Computer Engineering.</p>
    </div>
  </div>
  <div class="container left">
    <div class="content">
      <h2>2019-06-30</h2>
      <p>Xingxing Liu just graduated from University of Science and Technology of China.</p>
    </div>
  </div>
</div>