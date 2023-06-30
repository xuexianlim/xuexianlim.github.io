---
layout: page
title: Miniature Motorised Car
description: Design and Manufacture
img: assets/img/DMT.jpg
importance: 7
category: "Imperial College London"
---
<p style="text-align: justify">
The goal of this project was to design and build a miniature motorised car to race along a straight track. The design was subject to several non-negotiable constraints.
</p>

<ul>
    <li>Several standardised components had been provided and had to be included in the final design.</li>
    <ul>
        <li>Axles</li>
        <li>Bearing housings</li>
        <li>Brushed DC motor</li>
        <li>Switch</li>
        <li>AA batteries</li>
        <li>Wheels (assortment of ⌀ 50 mm, ⌀ 65 mm or ⌀ 80 mm)</li>
    </ul>
  <li>The car could not be wider than 200 mm. There were no length or height restrictions.</li>
  <li>Transmission elements could not be exposed and had to be covered with an additively manufactured cover.</li>
  <li>The switch had to be accessible from the outside of the vehicle without removing components such as the cover.</li>
  <li>The car had to be able to withstand an average person applying their full body weight on itself.</li>
  <li>All components had to be manufactured from a list of stock materials (sheets, plates, round bars and tubes of various materials and dimensions).</li>
  <li>The total budget was £600 and the allocated workshop time was 12 hours.</li>
</ul>
<p style="text-align: justify">
The project was overall a rather enjoyable one. Our car did not win the race but I wasn't too bothered by that. I was more impressed that we were able to accurately predict the race time of the car within half of a second. We used our dynamics and mechatronics knowledge to formulate a differential equation that modelled the position, velocity and acceleration of the car using the torque-speed characteristics of the motor, estimates of trasmission efficiency and estimates of the car's mass. It was really cool seeing how we could apply the things we learnt in other modules to an actual mechanical design project like this. Incidentally, this differential equation was a first-order linear differential equation which we had literally just learnt to solve in our Mathematics and Computing module (using separation of variables or using an integrating factor). On hindsight, I realised that the differential equation that we formulated neglected the rotational inertia of the wheels. However, this rotational inertia was likely not as significant as the car's mass and hence, the equation remained decently accurate in modelling the kinematics of the car.
<br><br>
A PDF of the final report can be found <a href="{{ 'DMT.pdf' | prepend: 'assets/pdf/' | relative_url}}" target="_blank" rel="noopener noreferrer">here <i class="fas fa-file-pdf"></i></a>.
</p>