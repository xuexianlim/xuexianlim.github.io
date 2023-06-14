---
layout: page
title: Ball Balancing Robot
description: 
img: assets/img/BBR.jpg
importance: 3
category: "ETH Zürich"
---
<p style="text-align: justify">
Hey. Check this out.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include video.html path="assets/video/BBR_Circle.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true loop=true muted=true %}
    </div>
</div>
<div class="caption">
    It's strangely relaxing to watch it go round and round.
</div>

<p style="text-align: justify">
This robot does exactly as its name implies, delicately balancing a ping pong ball at the desired coordinates atop itself. It comprises a PCB with an <a href="https://www.adafruit.com/product/3405">Adafruit HUZZAH32 - ESP32 Feather board</a> mounted on it, three <a href="https://kstservos.com/products/ds725mg-hv-digital-coreless-servo-18kg-cm-0-07sec-for-550-700-size-rc-helicopter?_pos=1&_sid=01f191e10&_ss=r">KST DS725MG HV servo motors</a> connected to three arms with two links each (forming a 3-revolute-revolute-spherical (3-RRS) parallel mechanism), a <a href="https://pixycam.com/pixy2/">Pixy2 camera</a>, a frosted acrylic plate and most importantly, a ping pong ball. The robot had to be connected to a laptop/PC for its operation. The PC would receive the ball position in the camera frame and convert it to the world frame. It would then feed this into a PID controller to obtain a desired angle for the plate. Finally, it would perform inverse kinematics to obtain the required angles for the servo motors and send a PWM signal to the microcontroller which would then control the servo motors.
<br><br>
</p>

<p style="text-align: justify">
<i>This page is still a work in progress. Check back next time for updates! Expected completion: July 2023.</i> 🚧
</p>