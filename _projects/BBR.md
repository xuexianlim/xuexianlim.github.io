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
This robot does exactly as its name implies, delicately balancing a ping pong ball at the desired coordinates atop itself. It comprises a PCB with an <a href="https://www.adafruit.com/product/3405">Adafruit HUZZAH32 - ESP32 Feather board</a> mounted on it, three <a href="https://kstservos.com/products/ds725mg-hv-digital-coreless-servo-18kg-cm-0-07sec-for-550-700-size-rc-helicopter?_pos=1&_sid=01f191e10&_ss=r">KST DS725MG HV servo motors</a> connected to three arms with two links each (forming a 3-revolute-revolute-spherical (3-RRS) parallel mechanism), a <a href="https://pixycam.com/pixy2/">Pixy2 camera</a>, a frosted acrylic plate and most importantly, a <a href="https://equipment.ittf.com/#/equipment/balls">ping pong ball</a>. The robot had to be connected to a laptop/PC for its operation. The PC would receive the ball position in the camera frame and convert it to the world frame. It would then feed this into a PID controller to obtain a desired angle for the plate. Finally, it would perform inverse kinematics to obtain the required angles for the servo motors and send a PWM signal to the microcontroller which would then control the servo motors.
<br><br>
The great thing about the Pixy2 camera is its speed, making it highly suitable for visual servoing. With a standard camera, the image would have to be compressed for sending, decompressed on the PC and then analysed with computer vision algorithms, leading to an unacceptably large delay for PID control. In contrast, the Pixy2 camera comes with integrated object detection and performs all these steps at 60 Hz, sending only the useful information (i.e. the coordinates of the ping pong ball) to the PC.
<br><br>
However, these coordinates still needed to be converted from the image frame to the world frame. We first took a bunch of pictures of a checkerboard pattern and used OpenCV to determine the Brown radial distortion model coefficients.
</p>

$$r_{d}=(1+k_{1}r^{2}+k_{2}r^{4}+\cdots)r$$

<p style="text-align: justify">
We could then use the Newton-Raphson method to calculate the undistorted coordinates in the image frame. These coordinates could now be converted to the world frame using the perspective camera model.
</p>

$$\lambda\begin{pmatrix}u\\v\\1\end{pmatrix}=\textbf{K}\begin{pmatrix}\textbf{R}|\textbf{T}
\end{pmatrix}\begin{pmatrix}X_{w}\\Y_{w}\\Z_{w}\\1\end{pmatrix}$$

<p style="text-align: justify">
After that, we calculated the velocity of the ball in the x-direction and the y-direction by using a simple first-order discrete derivative. We applied a moving average filter to both the position and the velocity of the ball as the raw data was very noisy. This could definitely have been improved by using a Butterworth filter for example. The figure below shows that a moving average filter with a larger window size gives smoother results but also a larger phase lag. In contrast, a 2nd-order Butterworth filter gives very smooth results with less phase lag. Ultimately, the main reason why we chose a 10-point moving average filter was its extreme simplicity in implementation. It should be noted that if we were working in the frequency domain for example, a moving average filter would actually be a very poor low-pass filter due to its slow roll-off and poor stopband attenuation.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/BBR_Filter.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Raw and filtered x-component of velocity in the time domain.
</div>

<p style="text-align: justify">
After obtaining the position and velocity of the ball, we could feed this to the PID controller which outputs the desired plate angle along the x-axis and the y-axis.
</p>

$$\varphi\left(t\right)=K_{p}e\left(t\right)+K_{i}\int_{0}^{t}e\left(\tau\right)d\tau+K_{d}\frac{d}{dt}e\left(t\right)$$

<p style="text-align: justify">
In discrete time, the following approximations can be made.
</p>

$$e^{t}\approx e\left[k\right]=x_{ref}-x_{actual}:=e_{p}\left[k\right]$$

$$\begin{array}{rcl}
\int_{0}^{t}e\left(\tau\right)d\tau&\approx & T_{s}\sum_{n=0}^{k}e\left[k\right]:=e_{i}\left[k\right]\\
&=&e_{i}\left[k-1\right]+T_{s}e\left[k\right]\end{array}$$

$$\begin{array}{rcl}
\frac{d}{dt}e^{t}&=&\frac{d}{dt}\left(x_{ref}-x_{actual}\right)\\
&=& v_{ref}\left(t\right)-v_{actual}\left(t\right)\\
&\approx&v_{ref}\left[k\right]-v_{actual}\left[k\right]:=e_{d}[k]\end{array}$$

$$\therefore \varphi\left[k\right]=K_{p}e_{p}\left[k\right]+K_{i}e_{i}\left[k\right]+K_{d}e_{d}\left[k\right]$$

<p style="text-align: justify">
The reference position and velocity for a circular trajectory could be obtained by simply using the parametric form of the equation of a circle.
</p>

$$\begin{array}{rcl}
x_{ref}&=&r\cos\frac{2\pi t}{T}\\
y_{ref}&=&r\sin\frac{2\pi t}{T}\\
v_{x\text{ }ref}&=&\frac{d}{dt}x_{ref}\\
&=&\dot{r}\cos\frac{2\pi t}{T}-r\frac{2\pi}{T}\sin\frac{2\pi t}{T}\\
&=&-r\omega\sin\frac{2\pi t}{T}\\
v_{y\text{ }ref}&=&r\omega\cos\frac{2\pi t}{T}\end{array}$$

<p style="text-align: justify">
After obtaining the desired plate angles, we could use inverse kinematics to calculate the required servo motor angles. The plate centre is assumed to be at \(\textbf{p}=\begin{pmatrix}0&0& P_{z}\end{pmatrix}^{T}\) while \(\varphi_{z}=0\).
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-4">
        {% include figure.html path="assets/img/BBR_SchematicA.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-4">
        {% include figure.html path="assets/img/BBR_SchematicB.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-4">
        {% include figure.html path="assets/img/BBR_SchematicC.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Ball balancing robot schematic diagrams.
</div>

$$\begin{array}{rcl}
\delta z_{A}&=&R\sin\varphi_{x}\\
\delta z_{B}&=&-\frac{1}{2}R\sin\varphi_{x}+\frac{\sqrt{3}}{2}R\sin\theta_{y}\\
\delta z_{C}&=&-\frac{1}{2}R\sin\varphi_{x}-\frac{\sqrt{3}}{2}R\sin\theta_{y}\\

\beta_{A}&=&\arccos\left(\frac{\left(P_{Z}+\delta z_{A}\right)^{2}+L_{1}^{2}-L_{2}^{2}}{2L_{1}\left(P_{Z}+\delta z_{A}\right)}\right)\\
\beta_{B}&=&\arccos\left(\frac{\left(P_{Z}+\delta z_{B}\right)^{2}+L_{1}^{2}-L_{2}^{2}}{2L_{1}\left(P_{Z}+\delta z_{B}\right)}\right)\\
\beta_{C}&=&\arccos\left(\frac{\left(P_{Z}+\delta z_{C}\right)^{2}+L_{1}^{2}-L_{2}^{2}}{2L_{1}\left(P_{Z}+\delta z_{C}\right)}\right)\\

\alpha_{A}&=&\frac{\pi}{2}-\beta_{A}\\
\alpha_{B}&=&\frac{\pi}{2}-\beta_{B}\\
\alpha_{C}&=&\frac{\pi}{2}-\beta_{C}\end{array}$$

<p style="text-align: justify">
Finally, the appropriate PWM signal was generated and sent to the servo motors to tilt the plate at the desired angle. This led to the following ball dynamics.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/BBR_Ball.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Ball dynamics.
</div>

$$\begin{array}{rcl}
J_{P}&=&J+mR^{2}\\
&=&\frac{2}{3}mR^{2}+mR^{2}\\
&=&\frac{5}{3}mR^{2}\\
J_{P}\ddot{\eta}&=&mgR\sin\theta_{y}\end{array}$$

<p style="text-align: justify">
Using the no-slip condition \(x=R\eta\), the acceleration of the ball can be obtained.
</p>

$$\begin{array}{rcl}
\ddot{x}&=&\frac{d^{2}}{dt^{2}}\left(R\eta\right)\\
&=&R\ddot{\eta}\\
&=&R\frac{mgR\sin\theta_{y}}{J_{p}}\\
&=&R\frac{mgR\sin\theta_{y}}{\frac{5}{3}mR^{2}}\\
&=&\frac{3}{5}g\sin\theta_{y}\\
\ddot{y}&=&-\frac{3}{5}g\sin\varphi_{x}\end{array}$$

<p style="text-align: justify">
If we assume \(\varphi_{x}\) and \(\theta_{y}\) to be small angles about the equilibrium, the above equations can be linearised. Hence, PID control is indeed a valid method for controlling the system.
</p>

$$\begin{array}{rcl}
\ddot{x}&\approx&\frac{3}{5}g\theta_{y}\\
\ddot{y}&\approx&-\frac{3}{5}g\varphi_{x}\end{array}$$

<p style="text-align: justify">
We tuned the PID parameters to achieve a critically damped step response. We also added individual offset angles to each of the servo motors to correct for their subtle systematic errors, ensuring that when 0 plate angle was demanded, both \(\varphi_{x}\) and \(\theta_{y}\) would indeed be 0.
<br><br>
The ball balancing robot was finally ready to work its magic! Overall, this was a really fun project that combined a little bit of everything to create a fascinating final product.
</p>

> "Engineers like to solve problems. If there are no problems handily available, they will create their own problems." - Scott Adams

<p style="text-align: justify">
And as we stare at the ping pong ball going round and round, we can ponder about why we went through all that trouble just to... make a ping pong ball go round and round.
</p>