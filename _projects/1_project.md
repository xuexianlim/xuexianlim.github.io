---
layout: page
title: Planning and Decision Making for Autonomous Robots
description: 
img: assets/img/PDM4AR_2.jpg
importance: 1
# category: work
---
<p style="text-align: justify">
This is hands down my favourite course thus far, which is why I'm featuring every single exercise in this course! The content that was taught was entirely new to me and maybe that was why it was so interesting. The assessment was done via 7 graded exercises and honestly, it felt almost like a puzzle-solving challenge which I really enjoyed. I was always looking forward to the release of the next exercise.
<br><br>
Exercise 1 was about graph searches (breadth/depth-first search, iterative deepening search). 
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_2.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A graph with a valid path (red) between the start (orange) and goal (green) nodes.
</div>

<p style="text-align: justify">
Exercise 2 extended this with informed graph searches (uniform cost search, A* search).
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include figure.html path="assets/img/PDM4AR_3.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6">
        {% include figure.html path="assets/img/ETH_Map.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Does this graph look familiar? That's because it's a map of the area around ETH Zürich!
</div>

<p style="text-align: justify">
In Exercise 3, I implemented value and policy iteration to solve a particular Markov Decision Process (MDP). In this MDP, there was a robot that tried to cross grass (green) and swamp (blue) tiles to reach a goal cell. Due to fog, the robot had a certain probability of going towards its desired direction or accidentally heading off in the other 3 cardinal directions or even getting stuck in its current location. The stage cost to be minimised was time taken (swamps took more time naturally). While the robot could not intentionally choose to exit the map boundaries, it could still inadvertently do so due to the finite transition probabilities of going off in a direction other than its chosen one. When this happened, it was considered as lost and a new one would then be parachuted into the start cell. In large maps, this led to a peculiar but entirely logical phenomenon. For faraway sectors, the robot's optimal policy was to move towards the edge of the map and hug the edge in the hopes that the it would get lost and be replaced with a new one that could immediately resume from the start cell which was closer to the goal cell. This was to be expected since no cost was imposed on replacing a lost robot and effectively, it was as if the robot could teleport to the start cell by exiting the map boundaries. This highlights the importance of modelling choices and assumptions.
</p>

> "All models are wrong, but some are useful." - George Box, 1976

<p style="text-align: justify">
At the end of the day, models are simply approximations and their utility depends on how well the assumptions reflect the actual processes. If indeed I just so happened to have infinite robots (and parachutes) and hence, could afford to aidrop endless waves of innocent robots at no cost, then this model would be entirely valid and would accurately reflect the directional choices that any robot should make.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include figure.html path="assets/img/PDM4AR_4A.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6">
        {% include figure.html path="assets/img/PDM4AR_4B.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The optimal value function. Right: The optimal policy.
    <br>
    Notice how in the bottom left sector of the map for example, the optimal policy is to head away from the goal and towards the edge of the map. "Get lost!" I tell my poor robots. "It's much faster this way."
</div>

<p style="text-align: justify">
Exercise 4 was about calculating Dubins paths. Intuitively, we all know that cars are not hovercrafts and are limited in their possible directions of motions. However, they can still achieve all possible states via some local manoeuvering. For example, parallel parking is a Lie bracket manoeuvre that allows a car to have a net sideways movement. I find it rather amusing that for every mundane phenomenon in real life, there's some rigorous mathematical concept out there to describe it even if it's unbeknownst to most people. The average driver doesn't need to know that their car is non-holonomic to perform a 3-point turn that follows a Reeds-Shepp path.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_5.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A simple Dubins path.
</div>

<p style="text-align: justify">
Exercise 5 was about collision checking. This was when I came to the realisation that computers are so smart yet so dumb. I can glance at a 2D path with obstacles along the way and immediately tell you whether there is a collision along the path. In contrast, using a naive collision checking algorithm, a computer needs to check boolean mathematical conditions for each and every path segment and each and every obstacle (and each and every line constituting the boundaries of the obstacle). Nevertheless, it can be sped up to eliminate redundant checks by using R-trees for example. Maybe my brain is actually subconsciously working in the exact same way as a computer when it comes to collision checking but can you really prove that, hmm?
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_6.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pfft, this path clearly has collisions. Anyone can see that without calculations!
</div>

<p style="text-align: justify">
In Exercise 6, I solved mixed-integer linear programming (MILP) optimisation problems where a voyage had to be planned. (The exercise even had its own narrative lore which sounded suspiciously close to the One Piece anime.) There were various costs and constraints imposed on the different problems. The unifying constraint throughout all the problems was the requirement to visit one and only one of the \(n\) islands in every archipelago (there were \(N\) archipelagos).
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_7.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Bon voyage!
</div>

<p style="text-align: justify">
This was one of the harder exercises that required some thinking out of the box as some costs were not linear. For example, one of the costs to be minimised was the total L1 distance travelled.
</p>

$$\sum_{a=1}^{N-1}\left|x_{a+1,\text{ }i_{a+1}}-x_{a,\text{ }i_{a}}\right|+\left|y_{a+1,\text{ }i_{a+1}}-y_{a,\text{ }i_{a}}\right|$$

$$i_{a}\in \mathbb{Z}:i\in \left[1,n\right]$$

<p style="text-align: justify">
One method of resolving this was to use the following simple identity.
</p>

$$\left|x_{2}-x_{1}\right|+\left|y_{2}-y_{1}\right|=\max\left(\begin{array}{l}
x_{2}-x_{1} + y_{2}-y_{1}\\
x_{2}-x_{1} + y_{1}-y_{2}\\
x_{1}-x_{2} + y_{2}-y_{1}\\
x_{1}-x_{2} + y_{1}-y_{2}
\end{array}\right)$$

<p style="text-align: justify">
With deliberate constraint choices, it then becomes easy to reformulate the minimum L1 distance cost as a minimax optimisation problem. An alternative solution by some other students utilised the common trick of introducing two additional non-negative variables to create new constraints in order to minimise the absolute value of the difference of two variables.
</p>

$$x_{a+1}-x_{a}=p_{a}-q_{a}$$

$$p_{a},q_{a}\ge 0$$

<p style="text-align: justify">
It's really nice to see how there are multiple ways to solve the same problem. While researching different tricks, I even found something called the Big M method whereby large M parameters are introduced into the constraints to turn on or off variables. (Confusingly, the Big M method is also the name of a modified version of the simplex algorithm to solve linear programming problems with greater-than constraints.) These are all very ingenious tricks to exploit linear programming solvers.
<br><br>
Exercise 7 was the final assignment and it was big.
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include video.html path="assets/video/PDM4AR_8.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    A simulation run with 5 cars.
</div>
