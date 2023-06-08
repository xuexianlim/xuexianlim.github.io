---
layout: page
title: Planning and Decision Making for Autonomous Robots
description: 
img: assets/img/PDM4AR_2.jpg
importance: 1
# category: work
---
<p style="text-align: justify">
This is hands down my favourite course thus far, which is why I'm featuring every single exercise in this course! The content that was taught was entirely new to me and maybe that was why it was so interesting. The assessment was done via seven graded exercises and honestly, it felt almost like a puzzle-solving challenge which I really enjoyed. I was always looking forward to the release of the next exercise.
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
In Exercise 3, I implemented value and policy iteration to solve a particular Markov Decision Process (MDP). In this MDP, there was a robot that tried to cross grass (green) and swamp (blue) tiles to reach a goal cell. Due to fog, the robot had a certain probability of going towards its desired direction or accidentally heading off in the other three cardinal directions or even getting stuck in its current location. The stage cost to be minimised was time taken (swamps took more time naturally). While the robot could not intentionally choose to exit the map boundaries, it could still inadvertently do so due to the finite transition probabilities of going off in a direction other than its chosen one. When this happened, it was considered as lost and a new one would then be parachuted into the start cell. In large maps, this led to a peculiar but entirely logical phenomenon. For faraway sectors, the robot's optimal policy was to move towards the edge of the map and hug the edge in the hopes that the it would get lost and be replaced with a new one that could immediately resume from the start cell which was closer to the goal cell. This was to be expected since no cost was imposed on replacing a lost robot and effectively, it was as if the robot could teleport to the start cell by exiting the map boundaries. This highlights the importance of modelling choices and assumptions.
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
Exercise 4 was about calculating Dubins paths. Intuitively, we all know that cars are not hovercrafts and are limited in their possible directions of motions. However, they can still achieve all possible states via some local manoeuvering. For example, parallel parking is a Lie bracket manoeuvre that allows a car to have a net sideways movement. I find it rather amusing that for every mundane phenomenon in real life, there's some rigorous mathematical concept out there to describe it even if it's unbeknownst to most people. The average driver doesn't need to know that their car is non-holonomic to perform a three-point turn that follows a Reeds-Shepp path.
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
In Exercise 6, I solved several mixed-integer linear programming (MILP) optimisation problems where a voyage had to be planned. (The exercise even had its own narrative lore which sounded suspiciously close to the One Piece anime.) There were various costs and constraints imposed on the different problems. The unifying constraint throughout all the problems was the requirement to visit one and only one of the \(n\) islands in every archipelago (there were \(N\) archipelagos).
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
Exercise 7 was the final assignment and it was huge. Huge in terms of the weightage in the course and huge in terms of the sheer workload. Loads of people were remarking on the forums that this course should have been worth more than 4 ECTS credits. Some even went so far as to point out that the workload for Exercise 7 alone was comparable to an entire semester project. I won't deny that it was a pretty stressful experience that was further exacerbated by a time crunch from exam preparations though on hindsight, I found this exercise to be rather satisfying and rewarding when the code finally worked (it is what some might term as type 2 fun).
<br><br>
The goal of the exercise was to create a planning and control stack for cars at an intersection with obstacles. All cars behave the same way as they run on the same code. The cars are individual agents and are unable to communicate with each other (much like in the real world although we do have turn signals and maybe rude hand gestures in the real world). They do however receive lidar observations about the obstacles in their surroundings in a limited range around themselves.
<br><br>
I broke down the problem into three parts - pathfinding, steering and decision making.
<br><br>
For pathfinding, I used an <a href="https://arxiv.org/pdf/1105.1186.pdf">RRT*</a> algorithm. The first time I generated a basic RRT that succesfully connected the start and goal polygons, I was so elated that I just sent it to my friend without any context. I then improved upon it by implementing RRT* as aforementioned. I tweaked the cost function slightly as the critera for scoring also included the cars' compliance with the lane directions. I thus added a penalty for the absolute heading deviation from the lane direction. I also limited the angles between each tree segment so that there would not be sharp turns that the cars could not perform. If I wanted to be really strict about it, I guess I could have implemented RRT* with Dubins paths but I decided that my method was a sufficient compromise. Finally, I biased the search towards the goal sector so that the RRT would not waste time exploring dead ends.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_8_RRT.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    What is it? Blood vessels? Mycelial network? Ant nest? Nah, it's just vanilla RRT.
</div>

<p style="text-align: justify">
For steering, I implemented a <a href="http://ai.stanford.edu/~gabeh/papers/hoffmann_stanley_control07.pdf">Stanley</a> controller. It worked very well after some tuning of the PID parameters. For speed, I implemented a flat reference speed and used another PID controller to maintain the speed. This reference speed would be altered by the car's decision making algorithm in response to obstacles in the vicinity of the car.
<br><br>
For decision making, I implemented a state machine decision making algorithm with states for the car to go, perform an emergency stop, replan its path, proceed slowly, wait for other cars to pass or back up to make space for other cars. The main problem that I was concerned about was what the cars would do in the event of a path conflict or even a gridlock.
<br><br>
This problem got me thinking about the necessity of the rules of the road/sea/air in real life. Each individual driver/sailor/pilot is a presumably rational agent with somewhat limited communication to other agents. The only reason why traffic doesn't devolve into chaos is because every agent adheres to these rules and just as importantly, assumes that other agents adhere to these same rules. This allows agents to make safe and predictable decisions that are consistent with what other agents would expect. For example, a very common rule across the land, sea and air domains states that vehicles coming from the right have the right of way. (This is why port lights are red and starboard lights are green. It's a mini traffic light of sorts that reinforces this rule to another approaching vehicle!) When these expectations are violated, accidents have a much higher probability of occuring.
<br><br>
With this in mind, I proceeded to design some rules for the cars to follow so that they would know when they had the priority to proceed and when they had to yield. These rules had to be applicable by each car using only its own lidar observations and without communication with any other cars. These rules also had to be consistent. That is, all cars in the area of conflict had to arrive at the same conclusion after applying the rules.
<br><br>
For a two-car conflict, the car which was closer to the point of intersection between the paths of the two cars would have priority. This made sense since this meant that the car with priority was the one that would cross the other car's path first. This was also reasonably easy to calculate as the cars could observe each other's positions and headings and extrapolate a path from there. This rule could definitely be improved by having the cars store a history of the other car's positions to more accurately predict its future trajectory rather than assuming it to be a straight path. This would have added a lot more complexity to the code however and given the limited timeframe to complete the exercise, I was not convinced that it was actually necessary.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include figure.html path="assets/img/PDM4AR_8_PriorityA.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-6">
        {% include figure.html path="assets/img/PDM4AR_8_PriorityB.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Priority in a two-car conflict.
</div>

<p style="text-align: justify">
For a multi-car gridlock, I calculated the centroid of the cars' positions. Intuitively, this meant that this was the area where the cars were more clustered towards. To determine the priority, I looked at a combination of the car's distance from the centroid and its angle off a line connecting the centroid to itself. I hypothesised that a car that was far from the centroid as well as having a large angle off was in the best position to manoeuvre around the gridlock and hence, gave it priority. Do I think that this is a rule that results in the fastest resolution of the gridlock? Absolutely not. One could look at the image below and argue that if the yellow car moved first, the blue and green cars could then quickly continue on their merry way. But remember the criteria that I set out for my rules. This rule is applicable by each car using only its own lidar observations. This rule also results in consistent conclusions amongst all cars. As far as I was concerned, this was a simple yet valid rule to implement. Crucially, it was a scalable rule that could be generalised to any number of cars.
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-">
        {% include figure.html path="assets/img/PDM4AR_8_PriorityC.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Priority in a multi-car gridlock.
</div>

<p style="text-align: justify">
Sigh, life in this intersection would have been so much easier if only there were traffic lights. Putting all the components together, we get the following simulation runs. (Do note that the cars were only given 50 s to reach their respective goals so they could not dilly-dally.)
<br><br>
</p>

<div class="row justify-content-center">
    <div class="col-6">
        {% include video.html path="assets/video/PDM4AR_8A.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
    <div class="col-6">
        {% include video.html path="assets/video/PDM4AR_8B.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    Simulation runs from my own stress tests.
    <br>
    I deliberately created scenarios that were likely to result in conflicts. Apologies for the frame rate. It had to be reduced, otherwise the video results for each simulation run would have taken way too long to generate on my laptop.
</div>

<div class="row justify-content-center">
    <div class="col-">
        {% include video.html path="assets/video/PDM4AR_8.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    Simulation run from the official test server.
</div>

<p style="text-align: justify">
It ain't perfect and there definitely are some bugs to iron out but I still am incredibly happy with my work.
</p>