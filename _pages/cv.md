---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* Ph.D in Electrical and Computer Engineering, Univesity of Iowa, 2025 (expected)
* B.S. in Applied Physics, University of Science and Technology of China, 2019

Work experience
======
* Spring 2024: Academic Pages Collaborator
  * Github University
  * Duties includes: Updates and improvements to template
  * Supervisor: The Users

* Fall 2015: Research Assistant
  * Github University
  * Duties included: Merging pull requests
  * Supervisor: Professor Hub

* Summer 2015: Research Assistant
  * Github University
  * Duties included: Tagging issues
  * Supervisor: Professor Git
  
Skills
======
<div style="display: flex;">
  <dive stype="width: 20%;">
    Python
  </div>
  <dive stype="width: 20%;">
    C++
  </div>
  <dive stype="width: 20%;">
    C#
  </div>
</div>

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>