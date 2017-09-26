---
title: "Balancing Car"
header:
  teaser: /assets/images/unsplash-1.jpg
  overlay_image: /assets/images/unsplash-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Robot
tags:
  - Control
  - LinkIt 7697
  - Machine Learning

gallery1:
  - url:        /assets/images/balancing-car/small-car.jpg
    image_path: /assets/images/balancing-car/small-car.jpg
    title: "Small Car"
  - url:        /assets/images/balancing-car/big-car.png
    image_path: /assets/images/balancing-car/big-car.png
    title: "Big Car"

gallery2:
  - url: /assets/images/balancing-car/small-car-side-view.jpg
    image_path: /assets/images/balancing-car/small-car-side-view.jpg
    title: "Side view of small car"
  - url: /assets/images/balancing-car/FBD-body.png
    image_path: /assets/images/balancing-car/FBD-body.png
    title: "Free Body Diagram of Body"
  - url: /assets/images/balancing-car/FBD-wheel.png
    image_path: /assets/images/balancing-car/FBD-wheel.png
    title: "Free Body Diagram of Wheel"
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

This is a project about the self-balancing car. 

## ROBOTS


{% include gallery id="gallery1" caption="Big car and small car." %}


## PHYSICAL MODEL

We can part

<iframe src="https://drive.google.com/file/d/0B0HNqd_8V0OlRURhZnBwTmRhbDA/preview" width="640" height="480"></iframe>

{% include gallery id="gallery2" caption="Free Body Diagram of **body** and **wheel**. " %}

### NEWTON METHOD

\\[ x = {-b \pm \sqrt{b^2-4ac} \over 2a} \\]


### LAGRANGIAN METHOD

## MEASUREMENT

## SIMULATION

### STATE SPACE

### TRANSFER FUNCTION

## IMPLEMENTATION

### HARDWARE

### SCHEMATICS

## VIDEOS

![small-car]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/small-car.gif)

![big-car]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/big-car.gif)

## ANALYSIS

## MACHINE LEARNING

## REFERENCE

[MATLAB: State-Space Methods for Controller Design](http://ctms.engin.umich.edu/CTMS/index.php?example=InvertedPendulum&section=ControlStateSpace)

[MIT OCW Linear Quadratic Regulator](https://ocw.mit.edu/courses/mechanical-engineering/2-154-maneuvering-and-control-of-surface-and-underwater-vehicles-13-49-fall-2004/lecture-notes/lec19.pdf)

[MIT OCW Feedback Control](https://ocw.mit.edu/courses/aeronautics-and-astronautics/16-30-feedback-control-systems-fall-2010/lecture-notes/MIT16_30F10_lec18.pdf)

Measurement of moment of inertia: Katsuhiko Ogata(2004). System Dynamics (4th ed). pp.82-83 New Jersey:Pearson


{% include toc title="Outline" icon="file-text" %}


