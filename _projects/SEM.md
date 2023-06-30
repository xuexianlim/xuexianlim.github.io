---
layout: page
title: Steering System Team
description: Imperial Racing Green
img: assets/img/SEM_Car.jpg
importance: 5
category: "Imperial College London"
---
<p style="text-align: justify">
The Shell Eco-Marathon is an annual competition where teams design, build, and race energy-efficient vehicles. Imperial Racing Green participates in the battery electric prototype class featuring tri-wheel, ultra-lightweight vehicles. I was a member of the five-man team that designed and manufactured the steering system for Imperial Racing Green's car.
<br><br>
We first sat down and had a nice chat with the team principal, who highlighted the problems with the previous pitman arm steering system. Firstly, it was broken.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-8">
        {% include figure.html path="assets/img/SEM_Tie_Rod.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A broken tie rod in a lightweight but insufficiently strong steering system.
</div>

<p style="text-align: justify">
Secondly, the driver reported that it was difficult to centre the steering wheel after applying a turning input.
<br><br>
Thirdly, the steering column was uncomfortably short.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/SEM_Column.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    In the case of a steering column, size does matter.
</div>

<p style="text-align: justify">
The team principal therefore emphasised that he wanted the steering system to be reliable, ergonomic and adjustable. We considered his requirements and the rules of the Shell Eco-Marathon and formulated a product design specification (PDS). A snippet of the PDS is shown below.
<br><br>
</p>

<table>
    <tr>
        <th>Feature</th>
        <th>Criteria</th>
    </tr>
    <tr>
        <td>Functionality</td>
        <td>
            <ul>
                <li>Turning radius must be 8 m or less. External wheel must be able to follow a 90-degree arc of radius 8 m in both directions.</li>
                <li>Must be able to effectively steer while the vehicle is moving at 40 km/h.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Ergonomics</td>
        <td>
            <ul>
                <li>Must be comfortable to use in a near-lying position.</li>
                <li>Steering column must have an adjustable range of 52-62 cm for different drivers.</li>
            </ul>
        </td>
    </tr>
        <tr>
        <td>Safety</td>
        <td>
            <ul>
                <li>Must have a high safety factor (&gt;2).</li>
                <li>Must not impede the driver's ability to egress quickly (&lt;10 s) in the event of an emergency.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Size and Weight</td>
        <td>
            <ul>
                <li>Must maintain the existing wheelbase of 512 mm for compatibility with the aeroshell.</li>
                <li>Central section is limited to 120×160×200 mm in order to fit within the chassis and maintain leg room for the driver.</li>
                <li>Should weigh &lt;2 kg.</li>
            </ul>
        </td>
    </tr>
</table>
<div class="caption">
    PDS snippet.
</div>

<p style="text-align: justify">
Following this, we researched steering systems used by other teams and then individually brainstormed potential design concepts. I drafted three concepts - a pitman arm steering system, a rack and pinion steering system and a direct trike steering system. The first two were pretty standard steering systems that can be found in go-karts and cars today. The direct trike steering system was the most unorthodox. It featured handles that connected directly to the kingpin. Its biggest drawbacks were the possibly unintuitive nature of steering (turn handles to the left to go right and vice versa) and the lateral space required for the movement of the handles (space was definitely not a luxury within the tight confines of the aeroshell).
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/SEM_Trike.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Direct trike steering system.
</div>

<p style="text-align: justify">
We used a selection matrix to objectively assess all the steering system concepts that we thought up. Unsurprisingly, the good ol' rack and pinion steering system emerged as the clear winner. It was sturdy, compact and intuitive for the driver to use. 
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/SEM_Rack.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Rack and pinion steering system. Sometimes, the wheel just doesn't need to be reinvented.   
</div>

<p style="text-align: justify">
We were now ready to go into the detailed design. We did some calculations for the gear ratio to achieve a balance between steering sensitivity and steering effort required. We also calculated the minimum face width for different materials using the Lewis equation. This led to us choosing a 42-teeth, MOD 1.5 steel pinion. We designed the housing for the rack and pinion as well as the mountings to attach the housing to the tubular chassis. A universal joint connected the pinion shaft to the steering column. The steering column consisted of two concentric hollow shafts that were locked together via a single split clamp collar. This clamp could be loosened to slide the inner shaft in or out to adjust the length of the steering column. We re-dimensioned the tie rods and chose a new material (6082-T6 aluminium alloy) for it. The existing steering knuckles from the previous steering system were kept.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include figure.html path="assets/img/SEM_CAD.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6">
        {% include figure.html path="assets/img/SEM_Assembly.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: CAD visualisation of the steering system mounted onto the chassis. Right: Assembly drawing for the steering system.
</div>

<p style="text-align: justify">
We then proceeded to the manufacturing and assembly stage. We manufactured the custom components in the university's workshop. It was really nice to be using the machining tools again after a hiatus from COVID-19. We milled, turned, sawed, drilled, reamed, tapped and bent things. We ordered the rest of the standard components like the rack and pinion, bearings and other bits and bobs from suppliers.
<br><br>
After assembling the parts and mounting the steering system onto the chassis, we were ready for testing. The first test was the steering radius test. We tuned the steering camber and toe angles and found that the car could turn with a steering radius of 4.3 m. Unfortunately, we could not do this test at speed as the powertrain of the car was not ready yet.
<br><br>
The second test was to test the strength of the system. Our FEA simulations identified the tie rod as the most probable component for failure. (This was exactly the part that failed in the previous steering system). We therefore attached strain gauges to the tie rods and used a torque wrench to apply torques of up to 20 Nm on the steering column. The highest stresses in the tie rods were found to be about 18 MPa, which is an order of magnitude lower than their yield stress or buckling stress values.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/SEM_Strain.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Strain gauges on the tie rods.
</div>

<p style="text-align: justify">
The third test was a qualitative ergonomics test with the drivers. They were highly satisfied with the feel of the steering system. However, once again, as the powertrain was not ready, test drives could not be done to ascertain the handling characteristics of the car.
<br><br>
Regardless, our team was confident that the safety factors for the steering system were high enough that it would not fail like before. It might have even been over-engineered but we erred on the side of caution as a heavier but fully working steering system was more than preferred over a lighter but non-functional one.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/SEM_Test.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Approved by the Stig.
</div>