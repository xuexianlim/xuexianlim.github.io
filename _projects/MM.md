---
layout: page
title: Motion Matching for Responsive Animation of Digital Humans
description: 
img: assets/img/MM_BobA.jpg
importance: 2
category: "ETH Zürich"
---
<p style="text-align: justify">
Animating responsive characters in video games is hard. Animating responsive characters with natural, lifelike movements is harder still. Character animation has traditionally been done using state machines. Transitions between different states (e.g. walking, running, jumping) have to be defined manually. This procedure can get very big and tedious very quickly if the character has lots of different states.
<br><br>
A recent alternative to this method is motion matching. It was first developed by <a href="https://www.gdcvault.com/play/1023280/Motion-Matching-and-The-Road">Ubisoft</a>. Motion matching is a technique where a motion capture (mocap) database is continuously searched at runtime for the most suitable frame that matches the current pose and the desired future plan. Because the motions come from mocap data, the resulting animation is realistic and natural while still being responsive to the user's inputs.
<br><br>
This project was my team's capstone project for the Digital Humans course. To be honest, I never expected myself to be working on a character animation project during my Master's in Robotics, Systems and Control. The Digital Humans course is a merger of two previous courses - Computational Models of Motion and Virtual Humans. I took it mainly for the former portion. There were 12 different projects to choose from but my team ultimately chose this as it looked interesting (plus the supervisor was a very nice chap). I really enjoyed this project regardless. It seems that life sometimes has a way of leading you down unexpected paths of serendipity.
<br><br>
Before I get into the project proper, I just want to say that this team was probably the best team that I ever worked with for any project. The other members were friendly, helpful, professional, accommodating and hardworking. We adhered strictly to our Gantt chart schedule and so the project had no hiccups and was basically smooth sailing all the way. We had very good version control practices in Git so even though there were new branches and pull requests all the time, the main branch remained very clean. It was pure bliss.
<br><br>
A PDF of the final report can be found <a href="{{ 'MM.pdf' | prepend: 'assets/pdf/' | relative_url}}" target="_blank" rel="noopener noreferrer">here <i class="fas fa-file-pdf"></i></a>.
<br><br>
</p>

<p style="text-align: justify">
<i>I am quite busy so this page is still a work in progress. Check back next time for updates!</i> 🚧
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include video.html path="assets/video/MM.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true loop=true muted=true %}
    </div>
</div>
<div class="caption">
    
</div>
