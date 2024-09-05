---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

<div class="wordwrap">You can also view my CV as a pdf on <a href="https://xxliu1996.github.io/files/xingxingliu_cv_mle_2024.pdf">CV</a>.
</div>

{% include base_path %}

Education
======
* Ph.D in Electrical and Computer Engineering, Univesity of Iowa, 2025 (expected)
* B.S. in Applied Physics, University of Science and Technology of China, 2019

Work experience
======
* ## University of Iowa
Graduate Research Assistant | Aug. 2019 - May 2025 (Expected)
  * Develop a surgical navigation system that enables 3D visualization of spine anatomy and precise tracking of surgical tools, with the potential to enhance the accuracy and safety of spine procedures.
  * Develop a deep network model for cross-domain spine segmentation, trained on T2 MRI images and capable of accurately segmenting both T1 and T2 MRI images.
  * Develop an algorithm for fluorescence-to-color image registration using features detected by a convolutional neural network.

* ## Alcon Laboratories
Research & Development Intern | June 2024 - Aug. 2024
  * Work on optimizing eye limbus and pupil detection programs with GPU acceleration. Employ CUDA to accelerate key stages of the eye image processing pipeline including rotation, filtering, edge detection, etc.

* ## Philips North America
Research Scientist Intern | June 2023 - Aug. 2023
  * Develop deep network models for 3D cerebral angiography segmentation to enhance catheter navigation in endovascular procedures.
  
Skills
======
<style>
td, th {
   border: none!important;
}
</style>


| Time         | Length        | Speed              | Mass         |
| ------------ | ------------- | ------------------ | ------------ |
| -Millisecond | Millimetre    | Kilometre per hour | Milligram    |
| Second       | Centimetre    | Foot per second    | Gram         |
| Minute       | Inch          | Miles per hour     | Ounce        |

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>