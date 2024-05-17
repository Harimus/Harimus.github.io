Tags: #blog #robotics

Alternative title:
# {{page.title}}
# Sensory-motor task are harder than what you (like to) think
# LLMs are AGI as long as language is the only way to measure intelligence.


Key points:
* [Moravec's Paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradoxl)
* We intrinsically *prefer* to think certain task to be harder, those are usually from the academic background. Intelligence Quotient (IQ) is a great example of something mired by this school of thoughts. It over emphasize in the academic skills.
* Comparison of the complexity of Chess/GO vs throwing a basket ball.
    * "Well the visual information and proprioception is highly correlated time-data! They don't just randomly switch!" - is a counter argument. But even in chess & Go there are moves that are so bad we could practically omit them from consideration because no player with the intention to win  would make those moves; so even in those games, there's bias/correlated data. 
    * Our society deem a grandmaster in chess to be intelligent/smart, we might even label him a genius. Yet, a person that can with high accuracy and repeatability throw a basket ball from the 3 point arc to the net, won't be praised for his genius.. *we inherently bias and rank certain abilities to be more intelligent (read: harder) than other ones*. If anything the generative models like GPT-3, ChatGPT and Stable Diffusion have put an unignoreable dent in this reality (for now). 
    * But at the same time, we do appreciate a skill that could be put in-between chess & basketball: A Sword smith or a [sushi chef](https://en.wikipedia.org/wiki/Jiro_Ono_(chef)). Coding is a little bit like being a smith or a chef, minus the fine motions required. We compensate that by associating ourselves more with the chess masters. 
* ... *Because that's what we think make us human unique to all the other animals* it is an  [human exceptionalism](https://en.wikipedia.org/wiki/Anthropocentrism) take on intelligence. Language, logic, math, physics, in its purest form is way more complex than the synergy of perception & sensio-motor commands a dog shows when chasing a a flying frisbee in the field. What truly is unique, is how we in a *world without a correct answer, filled with noise and false signals, we somehow discovered how the world operate and a means to communicate & record it*.
* Vision-Language model (VLM) seems to grasp some meaningful connection in the reality, it will be interesting to see if this is enough, and how *action* or continuous vision (video) will change this understanding.
* Underactuated robotics + Robot Manipulation preface text?
* Also add a little bit about how early socialism said [distribution by intelligence is ok](https://youtu.be/lrBRV3WK2x4?t=518) ?
* veritasium expert perception of chess 
* We've been here before: [Debate: Do Language Models Need Sensory Grounding for Meaning and Understanding?](https://youtu.be/x10964w00zk?t=3381)
* Make a reference to Suttons bitter lesson, esp the point that "encoding human knowledge is bad idea, and wont scale. we need *learning and search*" as mentioned in [this levine talk](https://youtu.be/aDzQwewwvO0?t=868) but right now, with moravecs paradox, *we don't even know what to learn, or what to search for* because it is unconscious behaviors
* This blog post about [Cerebellum]() was extremely interesting and should probably be mentioned with detail!(Probably worth reading the HN thread and it's comment too)
* This post https://loonylabs.org/2020/02/02/spinal-reflex-pathways/ about lego example
* This research introduction https://www.imperial.ac.uk/morph-lab/research/ example of the ear is an interesting second example to the above reflex-pathways. 

# Main text

This post is about my thoughts around the difference of the problems we are faced in robotics vs artificial intelligence research/engineering, and to shed a light to that difference and some misconception. It's mostly catered to tech-people, but I kept it light-hearted and general so I can send it to my friends. I will mention a little bit about the current (2024) advancements later in the text, and that part might be a bit more technical.

If you want a more technical, serious(better) post with a *solution* oriented point to make, I'll refer you to Eric Jang's post [1] (https://evjang.com/2022/07/23/robotics-generative.html)

Tl;dr Do you know Moravec's paradox? Do you understand it? Then you can probably skip (most of) this.


## Background
As I work in robotics research, I've often had to explain the difference between Robotics and Artifical Intelligence (AI). The two fields have obvious overlaps, but as things have developed, especially recently, there's more difference even in the methods of automation. In the public perception, those two fields are often seen as equivalent. 

![](/assets/images/terminator.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*When people talk about AI threat, this is the face they often imagine. A robot* 


With the reignited discussion surrounding AI due to the recent advancement in large language models (LLM) such as ChatGPT, I've had explain the difference more often. One recurring comment have been "When AI(LLM) have made such rapid progress, why haven't robotics? *How hard can it be* to create a robot now that we have ChatGPT?" 
 ![](/assets/images/llama.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*My face after getting that question for the 26th time*

The main point I have to repeat the argument that *sensio-motor task is harder than what you think*, and that the advancement in LLM does not directly transfer to some robot sensio-motor task performance(yet). In layman terms, I always have to start with saying "everyone equate the Skynet with T900 terminator, but those are two very different problems with different solutions." and while this is my personal opinion, the latter one (T900) is **a harder problem**.

So I decided to write down my thought and some arguments for it, so that from further on I can just refer to this piece of text. This post will be aimed mostly towards people with more tech/science leaning. (don't worry, *no math* or coding in this post) The specific perception I want to address can be summarized in [this  (now deleted)](https://twitter.com/DhruvBatraDB/status/1641871357020614656) reply on Twitter to a professor in robotics posting his work
![this](/assets/images/twitter_llm_robot.png){: style="display:block; margin-left: auto; margin-right: auto;" }*LLM-bro. New protagonist to the movie Raise of the LLM-bros, the sequel to Dawn of the crypto-bro. It follow the protagonist flex-tape slapping LLM on to any problem they see and call it a day.*

This post will be divided in to 3 sections. First I'll in few words describe the (relevant part of) how current AI solutions works, Then explaining the difference in the problem setting for robotics and why the methods(solutions) in AI/LLM might not be enough to solve this, and finally I touch a little bit about why I think many people have had hard time *wanting to even accept a central point being made* with some insights that come from this.

Keep in mind that a lot of things mentioned here is still something  actively debated, with fair disagreements. So I might soon be proven wrong.

## How does the AI solutions right now work?
Since the breakthrough of the group of algorithms/methods called [Deep Learning](https://en.wikipedia.org/wiki/Deep_learning), around 2009-2012 in image and pattern recognition, a lot of the subsequent methods that have been developed falls in to the same group methods. This include the Generative AI class of algorithms, such as now famous ChatGPT, all the [AI synthesized voices](https://youtu.be/opU_dKXReDQ?si=r1IoK7K6ylEwMh-8) and Image generation tools such as StableDiffusion, Midjourney, etc.

Without going in to the technical details too much, there's a couple of factor that underpin these group of methods. The first one is the computing power. The breakthrough in 2011 (AlexNet, DanNet) happened when people used Graphic Processing Units (GPU), a specific type of chip to dramatically speed up the training process of those deep learning models. The other is the [requirement for massive amount of data](https://youtu.be/R9OHn5ZF4Uo?si=QPfxNMO6OyPSnke8). It started with tens of thousands of cat pictures to train a model to distinguish cats in early 2010s to *most of the freely available data on the internet* to train the generate images or text. Rich Sutton wrote in his essay The Bitter Lesson \[[5](#references)\] about how rise in computing power being the driving factor of AI advancement.

Those two factors are important in our context. The two requirements that arise from these factors are that these methods are both *power* and *data* hungry. Power (computation) hungry nature of it means that if we ram those methods in to a robot (assuming here that it work that way), as long as you can outrun it for 10-20minutes and run around in a complex enough environment (door, stairs, forest, rocky terrain) that the computation can't catch up, you're pretty good to go.

[![](/assets/images/riseofthemachine.png){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*credit: saturday morning breakfast cereal*
](http://smbc-comics.com/comic/rise-of-the-machines)

These are not the only factors, but the *computation*(power) and *data* requirements, especially the latter, is something to keep in mind for the context of robotics.

## What is *hard*? What is complex?
Let me start by quoting Jacob Browning from this debate (timestamp 56:21) \[[3](#references)\]: 
>In 1966 MIT summer vision project aimed to teach a computer to see in a three-month program. There was a broad assumption that getting a computer to use language and reason was the hard problem of AI. Preceiving by contrast, was thought to be simple, and nothing more than putting input into a cognitive system. This project failed. It turns out vision is really hard ...... the historical background assumption underlying the vision project was the idea that cognition was essentially linguistics, and the corresponding assumption that non-linguistic processes like perception, action and motion and so on are all non-cognitive and easier to solve. 

In more layman term, what he said was that people had the assumption that *reasoning about things(such as cats) in a picture* is harder problem than *finding out what part(pixels) of the picture are things(cats)*. However, it wasn't until 2011 we could somewhat reliably know what part of the picture are cats (and it still produce funny gochas as below)
![](/assets/images/skunk.jpg){: style="display:block; margin-left: auto; margin-right: auto;" width="450" }

The point I want to emphasize with the above quote is that, **what we consider to be a hard/easy problem, are often not a good metric for how hard it actually is to solve that problem**. And we might be only partially wiser than what they were in 1966.


### Known since the 80s
The above observation is not mine. In fact, it have been known since 80s and have a name: It's called the [Moravec's Paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradox):
>Moravec's paradox is the observation by artificial intelligence and robotics researchers that, contrary to traditional assumptions, reasoning requires very little computation, but sensorimotor and perception skills require enormous computational resources. The principle was articulated by Hans Moravec, Rodney Brooks, Marvin Minsky and others in the 1980s.

In a more friendly terms, what Moravec was saying was that when you want to reverse-engineer(replicate) a skill, those skills that are *below the level of conscious awareness* are the harder problems. 

Imagine trying to teach a kid to ride a bicycle, and compare it to teaching the same kid how to do a matrix multiplication. The first skill is something taught to a kid, sometimes before entering elementary school. The latter is taught in Highschool or above. When you try to teach it, you probably start by breaking down each task to set of steps to follow, or concepts to learn. But most likely, the steps or concepts you break it down to is *not that helpful* for the bicycle, but easy to follow for the latter case, even for a computer. The former have way more unconscious process involved that than the latter, and often require more try&error from the kid to finally "grasp" or "get" it, for no better term. Meanwhile, matrix multiplication can entirely be taught with sheets of papers (albeit a lot of papers, if you think how much math you need to learn to understand it). 

As a thought exercise, lets try to break down a simple task: "pick up the coffe mug on the table and take a sip". You can assume that you know where the cup is. However you have to break down each step to *movements*, such as "move right hand forward, with speed X m/s. Move index finger and thumb Y cm". It's a task you most likely can do even without actively watching the process (you can do it while reading this). It's tedious, but to "picking up" it should be quite straight forward in steps. Now, how would your solution change if I added other objects in the way to pick it? How would grab it if it was empty vs filled to the brim (without spilling the content)? What if there was something on top of the cup? What if something sticky, such as honey was glueing it to the table? Your unconscious process can quickly and easily adjust to those settings, but you probably have to rewrite your sheet of "move commands" entirely each time the task is slightly altered. If you have a programming background, you might think you can add *if and while* loops in the mix and preserve that sheet mostly unchanged. And that might work for a while, in controlled environments, but in the real world the amount of variation quickly becomes overwhelming.

Now I asked you to break down that task to "movement component". But in reality, to make a robot(with similar shape to human) do that task, we actually need to break it down to *Force/Torque on each joint in your arm*. It might not seem like a big difference, but unconsciously all your "movement" are also somehow transferred to some form of force output to your arm. And when this force gets wrong, we can sometimes see funny behavior such as this robot falling over due to *thinking it is holding the door knob and applying required force to turn it, expecting a resistance* 

![](/assets/images/robotdoor.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*Robot trying to open a door*

WRITE HOW IN HUMAN BRAINS 80% of the mass is CEREBELLUM THAT DOES THIS KIND OF SHIT! and mention the dude that dont have it, and still can do stuff, but it is slower and have to be done more consciously

I haven't even touched upon the requirement to *also design the mechanical system*, only on the software side of the problem. So a common rebuttal to this (especially from Machine Learning people) is...

### "The hardware is just not there yet"
This is another argument I've heard multiple times, albeit a bit less recently, from Machine Learning folks: The hardware capacity is not there yet to actually utilize the AI advancement. Here's a [video](https://www.youtube.com/watch?v=UxWH5XAcFnM) of a human controlling a robot. 

![](/assets/images/telexistence.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="550" }*Human remotely controlling a upper-torso robot for a convenience store application*

This is a teleoperated robot I used to work with, it is controlled with a VR headset. The only feedback the user is getting is 3D image from two eyes, and the location of your VR controllers mapped to what you see through the headset, for visual feedback of where your VR controllers currently are at. 
It's a very simple(and cheap) setup at its core. The robot targeted mass production so a lot of sensors were stripped and some parts replaced with less reliable but cheaper components. But on this platform, *automating the task below is a very complex thing*. Yet humans can do this effortlessly; with only vision feedback, complete VR novice could do this task in a couple of minutes without damaging the robot. And more impressively, we can adapt to slight deviation without much issues. 

There are even more complex teleoperation setup and robot such as [1X technologies (formerly Halodi Robotics)](https://www.youtube.com/watch?v=091SsPrwuYc) or [Teleoperation with haptics feedback by Shadowhand](https://www.youtube.com/watch?v=J-3CcyF4Emw), and now at time of this writing the Tesla-bot. On the academic side, cheap yet efficient setup such as [Mobile-Aloha](https://mobile-aloha.github.io/) that can (with teleoperation) conduct quite dexterious tasks. So the hardware has already shown it capacity to do things, *when operated by an human brain*. It's hard to claim that the hardware isn't there yet, when you have this setup, with limited set of sensor *yet it can conduct complex task when operated by human*.  (If it is economically feasible or not, is a different question not touched upon, yet)

![](/assets/images/aloha.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="550" }*Two robot hands trying to apply contact lenses on a toy frog (I think it's a frog...?) 7x speedup from original, Teleoperated. Source: [ALOHA](https://tonyzhaozh.github.io/aloha/)*

So here's what they actually mean when they say the hardware is not there yet: 
>"There's no gigantic dataset the size of the internet with all the possible thinkable human tasks that is perfectly executed by a human, that have been labeled and collected noise free, with precision so that *reflexes when stepping on a lego* is also catched. Oh, and also computational hardware that can run ChatGPT sized model in less than 1 millisecond." 

Which is true, and the closest thing we have is probably the [Ego4D dataset by Meta](https://ego4d-data.org/). But if that's the requirement for a functioning solution to be provided by machine learning then most of the work have already been done for you, and it's akin to a incompetent general claiming that if all his soldiers were Supermen, his briliant tactic would've worked!

## The factors that underpin AI advancement can't be expected (yet) in robotics

As you've seen from the above hardware examples, there are real effort to create hardware platforms for teleoperation. The assumption here is that, just like Deep Learning worked thanks to scaling up data (internet-scale) of human demonstration (art, text, music/voice), if we collect enough data of the robot doing a certain task, label it with a textual description, we can train a model that learn abstract actions so that we can skip the "movement component" process we pondered on before, and the model can robustly perform tasks *it haven't originally been trained on*. The effort to create this model, called [Large Behavior Models](https://www.youtube.com/live/fwBbj6UmK-I?si=IDdKVR4q07ja26zZ) (LBM) is happening at different labs but I think [Russ Tedrake and Toyota Research Institutes work](https://www.tri.global/news/toyota-research-institute-unveils-breakthrough-teaching-robots-new-behaviors) is worth a mention, now that [Everyday Robots](https://say-can.github.io/) who also achieved impressive results, are down. Academic effort to create a [dataset to train these models (RT-X)](https://robotics-transformer-x.github.io/) should probably also be mentioned. 

I believe that these methods will get us far, and we will probably see more versatile & dexterous robots coming out from both industry and academic labs.

But this will probably fall short of the expectation that we have in robots. A system failure of a robot are often not tolerated to the same degree as advanced AI models. We can all laugh *and still keep using* ChatGPT or Midjourney when it give wrong answer or a image with a human having 6 fingers. But a *slight* failure of a self-driving car or robot-electrician cutting wrong wire and putting the house on fire, is unacceptable. 

![](/assets/images/robot-door.gif){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*Imagine having a robot like this with the failure rate of ChatGPT*

Since the world is a more dynamic & chatoic place than the internet, and the fact that on the internet, 1% failure-rate on a chat-bot is tolerable for those methods, means that those edge-cases are more prevalent for robotics problem and *not* ignoreable. *Replicating all those edge cases would be a arduous and long task* for data collection. Even at the current stage of things, it seems like *the quality* of the data collected matters more than the quantitym which contrast to the case of LLM models. For robotics, *The data is the bottleneck*.

* For robots point of view, the world is *underactuated*. What this mean is that the action you predict, is not the observation you get from next step. This is a pretty big contrast to say ChatGPT, which genereate texts and check it itself.  ELABORATE ON THIS
* Pretrained (vision) model seems to not work, especially when the weights are frozen. The feature that is extracted for vision task and that required for behavior seems to be different.

The other thing is computation factor. ChatGPT and Midjourney can write you a letter, solve coding problems, paint you a picture *incredibly* fast, compared to humans. Yet the speed those models output their result are magnitudes too slow for what is required to dexteriously traverse and interact with the real environment.


If you're hold a lunch-plate at the cafeteria and someone bump in to you lightly from behind, the entire process from recognizing what happened, to steady your balance while holding that lunch-plate horizontal so the content doesn't fall out, is happening fast. This is a requirement that is currently quite hard to achieve for the LBM or LLM models. It's worth mentioning that this kind of balance problems are something some robot solves very elegantly. You've probably seen [Boston dynamics bullying their robots](https://youtu.be/4PaTWufUqqU?si=V-4gdkNt14XzRnN0) to show this capacity. These robots uses entirely different methods, so it might be unfair to ask a LLM model to do this, and instead we can figure out how to connect those methods. But that again is a tricky technical problem to solve, and a factor outside of what we can expect from Deep Learning.

As example for us human, we know that the brain is divided in to regions with different purposes.  TODO: TALK ABOUT CEREBELLUM


But on top of this cerebellum  we've also developed an entire different process for situation that require even *faster* motor-sensory coordination: reflexes. When you step on a lego (ouch), with your reflexes you withdraw your leg, without even thinking about it. But at the same time as you withdraw your leg, another reflex also tell your opposite leg to help stabilize yourself, so that you don't loose your balance and fall over \[[6](#references)\]. This sensory-motor coordination requires such a quick motion that your unconscious process in the brain is even too slow, and it happens at the spinal cord. 

We might not have to design things according to how a biological brain does things. The solution for robots might look drastically different. Nevertheless, *we need a solution* to those problem addressed by the biological brain in a funny way, and thinking that an AI model that can mimic the capacity of the cognitive process of human brain, with all the afromentioned factors required to make it work, to be able to also solve these hard tasks, is an unanswered question.

## Let's look at our brain
Cerebellum and Reflex (spinal choord)

While my research interest is essentially betting on this working, I can't hide my scepticism for it.


### Sidenote
For people that are familiar the work of Daniel Kahneman, known for his book [Think, fast and slow](https://en.wikipedia.org/wiki/Thinking,_Fast_and_Slow) he suggest a framework of dividing thinking processes to "System 2" for slower, more deliberate & logical thinking, and "System 1" for more fast, instinctive & emotional thinking. *Most problems so far that have been solved with AI methods are from System 2* (Not all).

As a side note, 
.. There is an analogous concept in [*the conscious process of becoming an expert*](https://youtu.be/5eW6Eagr9XA?si=yycoezVb10sba_jk). Magnus Carlsen, world champion in chess said in an [interview](https://youtu.be/PZFS0kewLRQ?si=4TzHjY11vV2QvHKM) that most of the time, he know what to do, and don't need to figure it out. If you've learned how to bicycle, or drive a car, or mastered any other skill, you've done this too. At the beginning you need to focus more, put an conscious effort, using your "System 2", in Kahnemans terms, until after repetition.



# Why is it common intuitively repel this idea?
**Ok so this section is all my personal non-expert speculation and I want you to take this with a bucket of salt. I added it for potential fun discussions.**

When I mention that *complex motor coordination tasks* are harder than playing go or chess or writing code or creative endavor such as digital art, most people instinctively repel this idea. It is sometimes quite frustrating, reminding me of the [comedy sketch The Expert](https://youtu.be/BKorP55Aqvg?si=lN7tPOTAv7sjEdld) because there's often an bias that "because I don't need to think about it when I do it, it must be easy". The weird thing is that, even when I'm surrounded by people with expert knowledge, who understand the complexity of the problem I'm trying to explain, this point seems to not quite sit right! 

My speculation is that the idea that some motor task being harder than what we as a society consider "high intelligence tasks" is an uncomfortable idea, because it questions our belief in [human exceptionalism](https://en.wikipedia.org/wiki/Anthropocentrism).

![](/assets/images/human_exceptionalism.jpg){: style="display:block; margin-left: auto; margin-right: auto;" width="550" }*Illustration by Bill Sanderson, New Scientist, 13 May 1976*

Motor coordination after all, to a certain level, can be done by animals. (Moravec hypothesized around his paradox, that the reason for the paradox could be due to sensory & motor portion of the human brain have had billions of years of experience and natural selection to fine-tune it, while abstract thought have had maybe 100 thousands year or less.)  So saying that these are more complex than abstract reasoning, for quite obvious ideological and religious reasons, are repulsive.

It might not just be about the humana exceptionalism but also how our society justify certain hirarchies. A white collar desk worker typing in an excel sheet is somehow often seen as a more respectable and high-paying job than trades job such as electrician, carpenter, farmer etc. There's an obvious *economic* reason for this, guided by supply & demand and other factors. But anyone that havev worked at some corporate white colloar desk job, with some form [bullshit job](https://en.wikipedia.org/wiki/Bullshit_Jobs) must have thought at some point "gosh, a monkey can do this" while being paid multiples of trade workers while effectively only doing tasks such as "filling in an excel sheet when I get an invoce email." Usually these jobs also require a college degree from the worker (if not more). At some level, we need to create a cognitive dissonance to justify this. The point of sensory-motor tasks being harder than those years spend in college doesn't really sit right.

Even [early socialsts](https://www.youtube.com/watch?v=lrBRV3WK2x4&t=518s) thought domination distributed according to shares of intelligence was ok; from *Socialism 1.0: The First Writings of the Original Socialists, 1803-1813*:  

> I realize my friends, how entirely frustrated you are; but note that the possessors, although inferior in number, possess more enlightenment than you, and that, for the general good, domination must be distributed according to the share of intelligence.

Just for the record I'm not taking any *moral* stand on this. The reason how a society work a certain way is beyond my expertise. I'm just trying to point out examples of biases we inevitably have, when it comes to judging *how hard a task is*, and our belief in meritocratic society & our exceptional place in the nature might come to conflict withi this idea; not so different from the mistaken observation researchers had in 1966 about reasoning vs perception.

I should also add that *complexity* and *utility* of a problem/solution is not the same thing. Quite often in engineering and science, a very simple solution ends up having way more utility value than a complex one.


# Final words

My thoughts around this subject first arose when I started to apply models from LLMs after some promising results I saw at Conference of Robot Learning 2021. The result was promising, but like every roboticist, the more you test a system the more you think about the limitatioon of it and the right conditions required to run it. The real world, unlike the internet who you and me mainly interact with through text, voice and videos, are *so chaotic and complex*. But this is nothing new to someone that have tried to make a robot *do* something useful, so I didn't bother write it down much later, and the first take was way more tech-jargon heavy as it was for my own use and often used as a base material to discuss with my coworkers, whose background was not robotics but machine learning and often neuroscience.

But after the release of Stable Diffusion (Image generation AI) and subsequently ChatGPT I started to get messages from STEM friends like the following:


![](/assets/images/paranoidai.png){: style="display:block; margin-left: auto; margin-right: auto;" width="350" }*A message I got from a friend on instagram back in 2023 after ChatGPT was released*

So I thought maybe this point of view is worth sharing, at least to some of my friend. If you find it useful, or just fun, I'm glad it did but take it with a grain of salt. If you have constructive criticsm I'm all ears. 

To also add in case someone got the impression that I'm downplaying recent AI advancements, I'm not. I think the advances are remarkable, and I do think the impact it will have on our society will be big, both in the possitive and negative. My point is only that due to our skewed understanding of what is an hard problem to solve, people might extrapolate the current impact of AI development to the wrong direction, and therefore get anxious more than needed for different reasons. Personally I think the effect of Deep Fake and LLM-bot based fraud, and *the scale and ease of it* will cause a profound change to the internet, society and our culture. But my stance is similar to this post \[[4](#references)\], that our culture will adapt to this new technology, just as it did before.

Thank you .... X for helping me proof read it, especially the part that I quote from neuroscience and cognitive science.

# References

[1] [Eric Jang - How Can We Make Robotics More like Generative Modeling?](https://evjang.com/2022/07/23/robotics-generative.html)

[2] [Sarah Constantin - What does the cerebellum do anyway?](https://sarahconstantin.substack.com/p/what-does-the-cerebellum-do-anyway) (Note: I've been told by my neuroscientist coworker to take the claims in this post with a grain of salt, so you should probably too!)

[3] [Debate: Do Language Models Need Sensory Grounding for Meaning and Understanding?](https://youtu.be/x10964w00zk)

[4] [AI: Markets for Lemons, and the Great Logging Off](https://www.fortressofdoors.com/ai-markets-for-lemons-and-the-great-logging-off/)

[5] [The bitter lesson - Rich Sutton](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)

[6] [Know your spinal cord – The reflex pathways](https://loonylabs.org/2020/02/02/spinal-reflex-pathways/)

* https://www.economist.com/special-report/2016/06/23/automation-and-anxiety




This [Twitter link](https://twitter.com/DhruvBatraDB/status/1641823326741102600)
I think this is the [Economist article I read long time ago](https://www.economist.com/special-report/2016/06/23/automation-and-anxiety)

https://www.economist.com/sites/default/files/ai_mailout.pdf
