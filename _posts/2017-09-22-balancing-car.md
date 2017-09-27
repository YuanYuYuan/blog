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
mathjax: true

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
  - url: /assets/images/balancing-car/FBD-rod.png
    image_path: /assets/images/balancing-car/FBD-rod.png
    title: "Free Body Diagram of rod"
  - url: /assets/images/balancing-car/FBD-wheel.png
    image_path: /assets/images/balancing-car/FBD-wheel.png
    title: "Free Body Diagram of Wheel"

gallery3:
  - url:        /assets/images/7697.jpg
    image_path: /assets/images/7697.jpg
    title: "LinkIt 7697"
  - url:        /assets/images/L293D.jpg
    image_path: /assets/images/L293D.jpg
    title: "L293D Motor Driver IC"
  - url:        /assets/images/MPU6050.jpg
    image_path: /assets/images/MPU6050.jpg
    title: "IMU Sensor MPU6050"
   
gallery4:
  - url:        /assets/images/balancing-car/CAD.png
    image_path: /assets/images/balancing-car/CAD.png
    title: "CAD"
  - url:        /assets/images/balancing-car/CAD-explosion.png
    image_path: /assets/images/balancing-car/CAD-explosion.png
    title: "CAD Explosion"

gallery5:
  - url:        /assets/images/balancing-car/DDPG-model.png
    image_path: /assets/images/balancing-car/DDPG-model.png
    title: "DDPG-model"
  - url:        /assets/images/balancing-car/DDPG.gif
    image_path: /assets/images/balancing-car/DDPG.gif
    title: "CAD Explosion"

gallery6:
  - url:        /assets/images/balancing-car/PID-response-1.png
    image_path: /assets/images/balancing-car/PID-response-1.png
    title: "PID-response-1"
  - url:        /assets/images/balancing-car/PID-response-2.png
    image_path: /assets/images/balancing-car/PID-response-2.png
    title: "PID-response-2"

---

This is a project about the self-balancing car. 


## ROBOTS

There are two version of robot car, right one is is 1st ver. robot car in big size, 
operating in 12V, but since it's so bulky to balance itself, so there is the 2nd ver. in small size, 
which is small, compact, modolarized and easy to train and verified the control theorem.

{% include gallery id="gallery1" caption="Big car and small car." %}


## PHYSICAL MODEL

The robot which is equivalent to a inveted pendulum consists of two parts, the rod and the wheel.
The goal is to drive the wheel properly to prevent tilting, 
so we have to calculate the relative inertial force casued by the acceleration of wheel.

Following pictures are the Free Body Diagram of the two part, rod and wheel.

{% include gallery id="gallery2" caption="Free Body Diagram of **rod** and **wheel**. " %}

There are two method to deal with the model, 
one is the classical way in Newton Physics, 
another one is using Lagrangian method, i.e. energy method.

### NEWTON METHOD

Angular acceleration of wheel

\\[ I\omega \ddot{\phi}=\tau -F\cdot R \\]

Linear acceleration of wheel C.M.

\\[ \hat{i}:m_w \cdot\ddot{x}=-P_x-F \\]
\\[ \hat{j}:0=N-P_y-m_wg \\]

Angular acceleration of rod

\\[ I_r\ddot{\theta}=-\tau + P_yL\sin \theta+P_xL\cos \theta \\]

Linear acceleration of rod C.M.

\\begin{align}
    \hat{i}&:m_r(\ddot{x}-\ddot{\theta}L\cos\theta+\dot{\theta}^2L\sin\theta)=P_x \\\
    \cos\theta \hat{i}+\sin\theta \hat{j}&:m_r(\ddot{x}\cos\theta-\ddot{\theta}L)=-m_rg\sin\theta+P_y\sin\theta+P_x\cos\theta
\\end{align}

Position of C.M. of rod	

\\[ r=x\hat{i}-L\sin\theta\hat{i}+L\cos\theta\hat{j} \\]

Velocity of C.M. of rod

\\[
    \dot{r}=\dot{x}\hat{i}-\dot{\theta}L\cos\theta\hat{i}-\dot{\theta}L\sin\theta\hat{j}
\\]

Acceleration of C.M. of rod

\\begin{align}
    \ddot{r}&=(\ddot{x}-\ddot{\theta}L\cos\theta+
    \dot{\theta}^2L\sin\theta)\hat{i}-(\ddot{\theta}L\sin\theta+\dot{\theta}^2L\cos\theta)\hat{j}\\\
    &=(\ddot{x}\cos\theta-\ddot{\theta}L)(\cos\hat{i}+\sin\hat{j})-(\ddot{x}\sin\theta+\dot{\theta}^2L)(\cos\hat{j}-\sin\hat{i})
\\end{align}

\\begin{align}
    &\Rightarrow P_y\sin\theta+P_x\cos\theta=\frac{I_r\ddot{\theta}+\tau}{L}\\\
    &\Rightarrow m_r(\ddot{x}\cos\theta-\ddot{\theta}L)=-m_rg\sin\theta\frac{I_r\ddot{\theta}+\tau}{L}\\\
    &\Rightarrow -(m_rL\cos\theta)\ddot{x}+(I_r+m_rL^2)\ddot{\theta}=m_rgL\sin\theta-\tau
\\end{align}

and $$P_x=-m_w\ddot{x}-F$$,$$F=\frac{-(I_w\ddot{\phi}-\tau)}{R}$$

\\begin{align}
    &\Rightarrow m_r(\ddot{x}-\ddot{\theta}L\cos\theta-\dot{\theta}^2L\sin\theta)=-m_w\ddot{x}+\frac{(I_w\ddot{\phi}-\tau)}{R}\\\
    &\Rightarrow I_w\ddot{\phi}-(m_rR+m_wR)\ddot{x}+(m_rRL\cos\theta)\ddot{\theta}=m_rR\dot{\theta}L\sin\theta+\tau
\\end{align}

No slip condition:$$\ddot{x}=-R\ddot{\phi}$$

\\begin{align}
    \Rightarrow
    \begin{cases}
        (m_rRL\cos\theta)\ddot{\phi}+(I_r+m_rL^2)\ddot{\theta}=m_rgL\sin\theta-\tau\\\
        (I_w+(m_r+m_w)R^2)\ddot{\phi}+(m_rRL\cos\theta)\ddot{\theta}=m_rRL\dot{\theta}^2\sin\theta+\tau
    \end{cases}
\\end{align}

### LAGRANGIAN METHOD

\\begin{cases}
    \text{K.E. of wheel:}T_w=\frac{1}{2}m_w\dot{x}^2+\frac{1}{2}I_w\dot{\phi}^2\\\
    \text{K.E. of rod:}T_r=\frac{1}{2}m_r(\dot{x}-L\dot{\theta}\cos\theta)^2+
        \frac{1}{2}m_r(L\dot{\theta}\sin\theta)^2+\frac{1}{2}I_r\dot{\theta}^2\\\
    \text{P.E. :}V=m_rg\cos\theta
\\end{cases}

using Euler-Lagrange equation

\\[
    \frac{d}{dt}\big(\frac{\partial \mathcal{L}}{\partial \dot{q}}\big)-\frac{\partial\mathcal{L}}{\partial q} \\\
\\]

\\[
    \mathcal{L}=T_w+T_r-V, 
    q=
    \begin{pmatrix}
    x \\\
    \phi \\\ 
    \theta 
    \end{pmatrix}
\\]

\\begin{align}
    \frac{d}{dt}\big(\frac{\partial \mathcal{L}}{\partial \dot{x}}\big)-\frac{\partial\mathcal{L}}{\partial x}
    &=\frac{d}{dt}\big(m_w\dot{x}+m_r(\dot{x}-L\dot{\theta}\cos\theta)\big) \\\
    &=m_w\ddot{x}+m_r\ddot{x}-m_rL\ddot{\theta}\cos\theta+m_rL\dot{\theta}^2\sin\theta=F
\\end{align}


\\begin{align}
    \frac{d}{dt}\big(\frac{\partial \mathcal{L}}{\partial \dot{\phi}}\big)-
    \frac{\partial\mathcal{L}}{\partial \phi}&=\frac{d}{dt}\big(I_w\dot{\phi}\big) \\\
    &=I_w\ddot{\phi}=\tau-F\cdot R \\\
    \frac{d}{dt}\big(\frac{\partial \mathcal{L}}{\partial \dot{\theta}}\big)-
    \frac{\partial\mathcal{L}}{\partial \theta}
    &=(-m_rL\cos\theta)\ddot{x}+(I_r+m_rL^2)\ddot{\theta}-m_rgL\sin\theta=-\tau
\\end{align}

\\begin{align}
    \Rightarrow
    \begin{pmatrix}
        (m_w+m_r)R^2+I_w &m_rRL\cos\theta \\\ 
        m_rRL\cos\theta & I_r+m_rL^2
    \end{pmatrix}
    \begin{pmatrix}
        \ddot{\phi} \\\ 
        \ddot{\theta}
    \end{pmatrix} + 
    \begin{pmatrix}
        -m_rRL\dot{\theta}^2\sin\theta \\\
        -m_rgL\sin\theta
    \end{pmatrix} =
    \begin{pmatrix}
        \tau \\\
        -\tau
    \end{pmatrix}
\\end{align}

## MEASUREMENT

To obtain the physical parameter of the car, 
we have to measure the some important element derived in above equaitons.

The weight of the robot can be obtained easily by weighing on a platform scale, 
and the length and width are given in designed CAD.

But there is no direct method to measure the momentum inertia, 
so we have to set up an experiment like the following picture, 
hanging the robot by two wires and measure the spin period, 
and derive the theoretical momentum inertia.

![measurement]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/measurement.png)

And the following is simple python code used to compute the inertia.

```python

import numpy as np

# unit: MKS

# W is width, L is length, M is mass
W = #width
L = #length
M = #mass

# I is theoretical inertia, J is pratical inertia

I = M/12*(W**2+L**2)
print("theoretical inertia is {}".format(I))


# calculate inertia from period T
# T is period, A is rotation radius, G is gravity, H is height
T = #period
A = #radius
G = #gravity
H = #height

J = (T/2/np.pi)**2*A**2*M*G/H

print("pratical inertia is {}".format(J))


error = (J-I)/I*100
print("Error is {}%".format(error))
```

Finally, we got the table of desired parameter.

| car   | Rod Inertia | Wheel Inertia | Rod Mass | Wheel Mass | Rod Length |
|-------|-------------|---------------|----------|------------|------------|
| Big   | 0.0012      | 7.8537e-05    | 0.709    | 0.087      | 0.0412     |
| Small | 5.3493e-04  | 3.4951e-05    | 0.367    | 0.042      | 0.0175     |

(units: MKS)




## SIMULATION

At the simulation part, we discuss about the control model applied on the robot, 
there are two aspects on the model, one is state space in modern control, 
anthor one is transfer fucntion in classical control.

### STATE SPACE

After linearization with $$\cos\theta \approx 1, \sin\theta \approx \theta, \dot{\theta}^2 \approx 0$$

\\begin{align}
    &\big((I_r+m_rL^2)[(m_w+m_r)R^2+I_w]-(m_rRL)^2\big)\ddot{\phi} \\\
    &=[(I_r+m_rL^2)+m_rRL]\tau-(m_rRL)m_rgL\theta \\\ \\\
    &\ddot{\phi}=\frac{m_r^2L^2Rg}{(m_rRL)^2-(I_r+m_rL^2)[I_w+(m_w+m_r)R^2]}\theta \\\
    &+\frac{-(I_r+m_rL^2+m_rRL)}{(m_rRL)^2-(I_r+m_rL^2)[I_w+(m_w+m_r)R^2]}\tau \\\ \\\
    &\big[(m_rRL)^2-\big((m_w+m_r)R^2+I_w\big)(I_r+m_r   L^2)\big]\ddot{\theta} \\\
    &=\big(m_rRL+(m_w+m_r)R^2+I_w\big)\tau-\big((m_w+m_r)R^2+I_w\big)m_rgL\theta \\\ \\\
    &\ddot{\theta}=\frac{\big(I_w+(m_w+m_r)R^2\big)m_rgL}{\big(I_w+(m_w+m_r)R^2\big)(I_r+m_r L^2)-(m_rRL)^2}\theta \\\
    &+\frac{-\big(m_rRL+(I_w+(m_w+m_r)R^2)\big)}{\big(I_w+(m_w+m_r)R^2\big)(I_r+m_r    L^2)-(m_rRL)^2}\tau
\\end{align}

Let $$\tau$$ as input $$u$$, with states $$\phi, \dot{\phi}, \theta, \dot{\theta}$$, and the system is

\\begin{align}
    \dot{x}&=Ax+Bu \\\
    y&=Cx+Du
\\end{align}

where 

\\begin{align}
    A&=
    \begin{bmatrix}
        0 & 1 & 0                                                                                         & 0 \\\
        0 & 0 & \frac{m_r^2L^2Rg}{(m_rRL)^2-(I_r+m_rL^2)[I_w+(m_w+m_r)R^2]}                               & 0 \\\
        0 & 0 & 0                                                                                         & 1 \\\
        0 & 0 & \frac{\big(I_w+(m_w+m_r)R^2\big)m_rgL}{\big(I_w+(m_w+m_r)R^2\big)(I_r+m_r L^2)-(m_rRL)^2} & 0
    \end{bmatrix} \\\
    B&=
    \begin{bmatrix}
        0 \\\
        \frac{-(I_r+m_rL^2+m_rRL)}{(m_rRL)^2-(I_r+m_rL^2)[I_w+(m_w+m_r)R^2]} \\\
        0 \\\
        \frac{-\big(m_rRL+(I_w+(m_w+m_r)R^2)\big)}{\big(I_w+(m_w+m_r)R^2\big)(I_r+m_r	L^2)-(m_rRL)^2}
    \end{bmatrix} \\\
    C&=
    \begin{bmatrix}
        1 & 0 & 0 & 0 \\\
        0 & 0 & 1 & 0
    \end{bmatrix}\\\
    D&=
    \begin{bmatrix}
        0 \\\
        0
    \end{bmatrix}
\\end{align}

### TRANSFER FUNCTION

Orignal PID control block diagram

![PID-1]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/PID-1.png)

After rearrange

![PID-2]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/PID-2.png)

Thus get the transfer function of the controlled system

![PID-3]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/PID-3.png)

Plug in the ideal motor model to approximate the true model

![ideal-motor-model]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/ideal-motor-model.png)

Then we have the complete transfer function

![PID-4]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/PID-4.png)

{% include gallery id="gallery6" caption="PID response" %}


## IMPLEMENTATION

The robot car is designed in Onshape CAD and made of laser-cutted acrylic board, 
and the main controller is LinkIt 7697 which is much powerful then Arduino board.

To keep balance, it's needed to add an IMU(inertia measurement unit) to monitor the linear accelertaion and angular velocity.

### HARDWARE

{% include gallery id="gallery4" caption="Onshape CAD Model of Small Car" %}

{% include gallery id="gallery3" caption="Electronic Components" %}

### Schematics

![schematics]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/schematics.png)

### Diagram

The following diagram shows the structure of the whole implementation of the robot car, 
some difficult works are the conversion from continuous model to discrete computation on the micro controller, 
and the correction of the derived angle by adding some filter like compimentary filter/Kalman filter.

![diagram]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/diagram.png)


## VIDEOS

![small-car]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/small-car.gif)

![big-car]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/big-car.gif)

## ANALYSIS

The controller 7697 has the ability to transfer the recording data to computer for analysis, 
the following pictures are recorded data while small car balancing with PID control.

### Angle

![angle-analysis]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/angle-analysis.png)

### Angle Rate

![angle-rate-analysis]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/angle-rate-analysis.png)

### Angle Sum

![angle-sum-analysis]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/angle-sum-analysis.png)


## FUTUREWORK: MACHINE LEARNING

Ideal vs Practical

1. Continuous vs Discrete on computation
2. Inaccurate IMU Angle 
3. Ideal Motor Model is not good enough
4. Measurement Error

Since the classical method on controlling problem depends on the accurancy of physical parameter and a stable environment, 
maybe we can have a different way to deal with this kind of problem.

A powerful tool on dealing with continuos control problem is to use RL(Reinforcement Learning), 
the following simulation is used the [DDPG(Deep Determinlistic Policy Gradient)][4]
to balance a inverted pendulum in a custom OpenAI GYM environment.

To have more detail on the simulation, you can refer this [report][5]


{% include gallery id="gallery5" caption="DDPG" %}


The following is the diagram for balancing car under maching learning

![ML-diagram]({{ site.url }}{{ site.baseurl }}/assets/images/balancing-car/ML-diagram.png)

So far, there are still some works to implement the RL algorithm on the robot car, 
including the wireless data transformission(the C++ [library][6] is under developed), and the learnging environment of the robot 
still need some improvement, so there's still a long way to go.

## REFERENCE

[MATLAB: State-Space Methods for Controller Design][1]

[MIT OCW Linear Quadratic Regulator][2]


[MIT OCW Feedback Control][3]

[Continuous control with deep reinforcement learning][4]

[1]:http://ctms.engin.umich.edu/CTMS/index.php?example=InvertedPendulum&section=ControlStateSpace
[2]:https://ocw.mit.edu/courses/mechanical-engineering/2-154-maneuvering-and-control-of-surface-and-underwater-vehicles-13-49-fall-2004/lecture-notes/lec19.pdf
[3]:https://ocw.mit.edu/courses/aeronautics-and-astronautics/16-30-feedback-control-systems-fall-2010/lecture-notes/MIT16_30F10_lec18.pdf
[4]:https://arxiv.org/abs/1509.02971
[5]:https://drive.google.com/open?id=0B0HNqd_8V0OlNFRQUmg0dl9RMzQ
[6]:https://github.com/YuanYuYuan/balancing-robot/tree/master/libs/DataTransimission

Measurement of moment of inertia: Katsuhiko Ogata(2004). System Dynamics (4th ed). pp.82-83 New Jersey:Pearson


{% include toc title="Outline" icon="file-text" %}


