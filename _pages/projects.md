---
title: Portfolio
layout: default
permalink: /portfolio/
published: true
---
<h2 style="text-align: center;">Professional projects</h2>

<div class="ProjectContainer">

	<div class="gallery">

  {% for project in site.projects %}

  {% if project.redirect %}
  <div class="projectTile">
          <a href="{{ project.redirect }}" target="_blank">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% else %}

  <div class="projectTile">
          <a href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% endif %}

  {% endfor %}
	</div>

</div>

<h2 style="text-align: center;">Personal projects</h2>

<div class="ProjectContainer">

	<div class="gallery">

  {% for project in site.personal %}

  {% if project.redirect %}
  <div class="projectTile">
          <a href="{{ project.redirect }}" target="_blank">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% else %}

  <div class="projectTile">
          <a href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
          <span>
              <h2>{{ project.title }}</h2>
              <br/>
              <p>{{ project.description }}</p>
          </span>
          </a>
  </div>

  {% endif %}

  {% endfor %}
	</div>

</div>

<h2 style="text-align: center;">Publications</h2>

1. S. Jegorov et al., "Novel Digital Twin Concept for Industrial Application. Study Case: Propulsion Drive System." Proceedings of the ASME 2022 International Mechanical Engineering Congress and Exposition. Volume 2B: Advanced Manufacturing. Columbus, Ohio, USA. October 30–November 3, 2022. V02BT02A011. ASME. doi: [10.1115/IMECE2022-97243](https://doi.org/10.1115/IMECE2022-97243)

2. M. Ibrahim et al., "Conceptual Modelling of an EV-Permanent Magnet Synchronous Motor Digital Twin." *IEEE-PEMC International Power Electronics and Motion Control Conference.* Brasov, Romania. September 25-29, 2022. IEEE. link: [ETIS](https://www.etis.ee/Portal/Publications/Display/30c67d44-e946-4e58-9949-5bb56b54d92d)

3. V. Rjabtšikov et al., "Digital Twin Service Unit for AC Motor Stator Inter-Turn Short Circuit Fault Detection," *2021 28th International Workshop on Electric Drives: Improving Reliability of Electric Drives (IWED)*, 2021, pp. 1-5, doi: [10.1109/IWED52055.2021.9376328](https://doi.org/10.1109/IWED52055.2021.9376328).

4. V. Kuts et al., ‘ROS middle-layer integration to Unity 3D as an interface option for propulsion drive simulations of autonomous vehicles’, *IOP Conference Series: Materials Science and Engineering*, vol. 1140, no.1, pp. 012008, May 2021, doi: [10.1088/1757-899X/1140/1/012008](https://doi.org/10.1088/1757-899X/1140/1/012008).

5. V. Kuts et al., "Digital Twin: Universal User Interface for Online Management of the Manufacturing System." *Proceedings of the ASME 2021 International Mechanical Engineering Congress and Exposition. Volume 2B: Advanced Manufacturing.* Virtual, Online. November 1–5, 2021. V02BT02A003. ASME. doi: [10.1115/IMECE2021-69092](https://doi.org/10.1115/IMECE2021-69092).