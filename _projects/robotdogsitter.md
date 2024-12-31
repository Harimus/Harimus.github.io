---
layout: default
title: "Weekend project: dog sitter with robot dog!" 
description: this is a project
category: projects
date: 2024-12-17
---

# {{page.title}} 
Last weekend, I was on dog-sitter duty for my brother's dogs. It's always a delight to have those two rascals over!

While discussing the schedule for taking care of them with my partner, I got the idea to program my robot-dog companion as a fun project to tease my dog nephews. (to be that cool uncle).
<div style="text-align:center">
<p float="left">
  <img src="/assets/images/crayfishgimbal.jpg" width="130" />
  <img src="/assets/images/XGO-mini-2.webp" width="300" /> 
</p>
  <p> my brothers dog dressed up for crayfish party & xgo mini2, a hobby quadruped with a robot arm </p>
</div>







The year before, I was part of funding the [Kickstarter project for a mini quadruped robot called Xgo mini](https://www.kickstarter.com/projects/xgorobot/xgo-mini-an-advanced-quadruped-robot-with-ai-modules) after hearing about it in a [Sentdex's video](https://youtu.be/U2nNI9Yp_0g?feature=shared). Although I got the robot, it had been lying around for a year or two. Even after getting the [version 2 with an arm](https://www.robotshop.com/products/xgo-mini-2-quadruped-robot-dog), I never got to actually play with it because I was busy working on stuff at work. 



I've been in the process of studying the MIT course [Underactuated Robotics](https://underactuated.csail.mit.edu/) by Professor Russ Tedrake, after ~~FOMO~~ feeling the need to familiarize myself a bit more with motion planning(Trajectory Optimization), control & simulators now that my work was  becoming more around RL/IL & other Machine Learning applied to robotics. Most of that effort has been confined to the [Drake simulator](https://drake.mit.edu/) and using trajectory optimization (to not break the robot), so not applicable to this.

![](/assets/images/xgodrakewalk.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="450" }*Don't mind the wonky arm. The simulator is treating it as a free joint that bounces back&forth with a pretty major contact force bounce! Not simulators fault, but my setting and urdf file* 

Since version 2 is made in Raspberry Pi, I thought it would probably be an easier platform to just crank up a project from scratch. But Robotics 101 says *the devil is always in the details* and even simple solutions with simple moving parts fail, [something I should be well aware of]({% post_url 2024-05-31-motortask %}). Anyway, I just coded up something simple: using python & ZMQ for remote-control fun, then openCV +  YoloFast with onnxruntime for detecting the dogs & some simple state-machine for chasing them and getting their attention. I didn't want to get boggled down in control algorithms for now, so I went with some built-in gate-control libraries. 

{% assign video_files = site.static_files | where: "video", true  %}
{% for file in video_files %}
   {% if file.name == 'gimbalandxgo.mp4' %}
<video src="{{file.path}}" controls="controls" style="max-width: 630px;">
</video>
   {% endif %}
{% endfor %}
\*No dog was harmed in the process of making this project! Dog uncle cares about his dog-nephews =)

It worked well for a weekend project, with less than a day spent on it. I had fun ~~scaring~~ playing around with the two dogs. Controlling it from the robot's POV was very fun, even if some noticeable delay was introduced with distance since I was just using my phone as a wifi router. The Automation part, predictably, didn't go as well. (one or two successes that I forgot to record...) The simple logic (pseudo code, simplification of simplification):

```python3
if dog is not found:
  cry() # get dogs attention
  found = search_dog()  # simple search heuristic
elif dog is found:
  chase_dog()  # simple motion based on matching the detected bounding box  
elif dog is close_by:
  interact_with_dog() # do some funny stuff
```
broke in a very predictable (and funny) way. 

### The predictable faults:
*The detection quality was low.* One of the remedies would've been to increase the image quality, such as increasing the camera auto-exposure. (the lightning condition at floor level wasn't ideal) Very quick testing did show that the angle matter and the POV from below the dogs often confused the detector.



*The time synchronization issues* that make you appreciate the robotics middleware such as ROS that simplifies all of this ;)

**The heuristic of `search_dog` could've been improved.**  *Motion causes blur in the image*, which drops the detection quality! Standing still while using object detection was the obvious simplification but when the system has small delays caused by: camera capture, socket communication, detection inference, and motion command delays, it accumulates to instability relatively quickly. 

**Dogs are moving (duh!)** `chase_dog()` although continuously updating the position of the detected dogs, didn't really take into account the time delays between detection & also motion commands. An obvious solution was using simple state estimation (Kalman filter etc) for the current robot pose/velocity, and also for tracking the dog position & velocity, and using filtering for outliers.

Enough about the faults, now about the funny faults.

### Funny faults:


**There are two dogs**. Post-processing detection needs to take this into account, but YoloFast uses [nonmax suppression](https://medium.com/analytics-vidhya/non-max-suppression-nms-6623e6572536) for post-processing the bounding boxes, which means that when the dogs are close to each other, it often detects each dog at different frames! It's a problem I solved before at work a long time ago, by estimating object states and using that together with [assignment problem](https://en.wikipedia.org/wiki/Assignment_problem) algorithms (such as The Hungarian algorithm, modified). Relatively simple with very little overhead. (TODO comment somewhere in the code)

![](/assets/images/twodogs.jpg){: style="display:block; margin-left: auto; margin-right: auto;" width="250" }*They're judging my effort....*

**Mirrors**. One part of my apartment has mirrors as a wall. While walking there, the robot detects *itself as a dog!* Which made it just chase itself! The simple solution was to not deploy it close to the mirrors. But yes, my robot dog failed the [mirror test](https://en.wikipedia.org/wiki/Mirror_test).

<div style="text-align:center">
<p float="left">
  <img src="/assets/images/dogtest.jpg" width="300" />
  <img src="/assets/images/catbeanie.jpg" width="300" /> 
</p>
  <p> The machine thinks it's a dog.... but thinks the dog is a cat. </p>
</div>

**Test time affects deployment**. Now this is specific to dogs. While working on it, I realized that version two XGO quadruped came with a microphone. So I went and downloaded some funny short sound clips such as dog toys squeaking, barking, or dog crying. I thought this would dramatically simplify the problem by making the dogs come to the robot, rather than the other way around. And initially, testing it, it worked! **Caveat**: dogs got used to it after about 5 tests, and started to ignore it. So when I finally put everything together it helped very little. 

{% assign video_files = site.static_files | where: "video", true  %}
{% for file in video_files %}
   {% if file.name == 'xgoSoundandmove.mp4' %}
<video src="{{file.path}}" controls="controls" style="max-width: 630px;">
</video>
   {% endif %}
{% endfor %}

This was just a fun weekend project conducted haphazardly.
This project ended up ignoring all the parts about control, (using pre-existing solutions) and skip motion planning. 

Even with that, by remote control, the problem is trivially solved. I skipped any proper automation logic implementation because I just wanted to see how simple logic that almost anyone could write, would perform. The fun of working on real-world robotics is always to reexamine *things we take for granted*. Lightning condition is one. Time delays, multiple objects, tracking, knowing if the legs are stuck or not, slipping and the list can go on.

![](/assets/images/xgoterminator.jpg){: style="display:block; margin-left: auto; margin-right: auto;" width="450" }

(sidenote: I don't particularly like the field of Task and Motion Planning (TAMP) but I gotta admit using those principles rather than simple state-machine would've probably, even for this project, been easier)




