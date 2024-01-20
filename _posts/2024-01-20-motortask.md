Tags: #blog #robotics

Alternative title:
LLMs are AGI as long as language is the only way to measure intelligence.


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
* This blog post about [Cerebellum](https://sarahconstantin.substack.com/p/what-does-the-cerebellum-do-anyway) was extremely interesting and should probably be mentioned with detail!(Probably worth reading the HN thread and it's comment too)


# Main text

## Background
With the reignited discussion surrounding AI due to the recent advancement in large language models (LLM) such as GPT-4 and ChatGPT, I've had more occasions having to repeat the argument that *sensio-motor task is hard*, and the advancement in LLM does not directly transfer to some robot sensio-motor tasks(yet). In layman terms, I always have to start with saying "everyone equate the Skynet with T900 terminator, but those are two very different problems with different solutions." and while this is my personal opinion, the latter one (T900) is **a harder problem**.
![](/assets/images/terminator.gif)

So I decided to write down my thought and supports for it, so that from further on I can just refer to this piece of text, and hopefully this will improve with feedback & counter arguments. Most people that want to discuss this topic with me are from the field of Software engineering, Machine Learning, and occasionally Neuroscience researchers (since I work with them) so it will be catered towards people with more tech/science leaning. The point I'm making is not something new, it has been made several times, so I will also dig a little bit in *why* some people seem to intuitively have a distaste for it. 

Keep in mind that a lot of things mentioned here is still something  actively debated, with fair disagreements. So I might soon be proven wrong(maybe by you!). I would be very happy to be proven wrong, because my interest and work (right now) is to apply the advancement in Deep Learning to robotics, including LLM, meaning that if I'm wrong, I can be safe that my current effort is not wasted.

## Known since the 80s
Let's start by mentioning  [Moravec's Paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradox):
>Moravec's paradox is the observation by artificial intelligence and robotics researchers that, contrary to traditional assumptions, reasoning requires very little computation, but sensorimotor and perception skills require enormous computational resources. The principle was articulated by Hans Moravec, Rodney Brooks, Marvin Minsky and others in the 1980s.

Moravec hypothesize that this could be due to sensory & motor portion of the human brain have had billions of years of experience and natural selection to fine-tune it, while abstract thought have had maybe 100 thousands year or less.  
~~The formulation of the paradox that I personally like is this,  *What we consider to be an intellectually hard task is often what we consciously can reason to be hard. But the easy tasks, the tasks that can be unconsciously performed, but not consciously be explained.*~~

`how to connect the above insight in to the below attitude...?`

A similar observation have been
Most ML & Software backgrounds peoples reaction to the above can be summarized as [this](Illustration by Bill Sanderson, New Scientist, 13 May 1976):
![this](/assets/images/twitter_llm_robot.png)

### "The hardware is just not there yet"
This is another argument I've heard multiple times, albeit a bit less recently, from Machine Learning folks: The hardware capacity is not there yet to actually utilize the ML capacities. Here's a [video](https://www.youtube.com/watch?v=UxWH5XAcFnM) of a human controlling a robot. This is a teleoperated robot I used to work with, it is controlled with a VR headset. The only feedback the user is getting is 3D image from two eyes, and the controller location mapped to that image like AR, for visual feedback of whre your VR controllers currently are at. 
It's a very simple(and cheap) setup at its core, but on this platform, *automating the task below is a very complex thing*. Yet humans can do this effortlessly; with only vision feedback, complete VR novice could do this task in a couple of minutes without damaging the robot. There are even more complex teleoperation setup and robot such as [1X technologies (formerly Halodi Robotics)](https://www.youtube.com/watch?v=091SsPrwuYc) or [Teleoperation with haptics feedback by Shadowhand](https://www.youtube.com/watch?v=J-3CcyF4Emw). So the hardware has already shown it capacity to do thing, *when operated by an human brain*. It's hard to claim that the hardware isn't there yet, when you have this setup, and more expensive robot arms have precision far better than humans. (We are omitting the *it's economically not feasible yet* argument here )
![](/assets/telexistence.gif)

So here's what they actually mean when they say the hardware is not there yet: "There's no gigantic dataset with all the possible thinkable human tasks that is perfectly executed by a human, that have been labeled and collected noise free." Which is true, and is a problem addressed in this [blog post](https://evjang.com/2022/07/23/robotics-generative.html) by [Eric Jang](https://twitter.com/ericjang11?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor) (If this topic interest you, you should probably follow him!) and is something actively worked on in the research field of Robot learning.

To me this sounds a bit like "well"

```
REACTION_TIME = 0.25
NUM_MUSCLES = 600

def your_brain(text_command, image_from_eye, proprioception, sound, tactile_sensation):
    assert is_newton(output)
    assert dimensions(output) >= NUM_MUSCLES
    assert type(output) == continuous_type
    assert computation_time < REACTION_TIME //seconds
    return output

def your_solution(text_command, image_from_camera, priprioception, force_sensors, tactile_sensors, sound):
    assert is_newton(output)
    assert computation_time < REACTION_TIME //seconds
    return output
```

### Why do you intuitively repel this idea?
When I mention this, majority of the proponent I speak with, if they're not Neuroscientists, or someone that have at least dabbled in some complex control theory related domain, is to treat it with suspicion. I've inquired why, often with the benefit of time because usually I've rephrased my arguments multiple times so I'm well prepared, so I ask them that they can come back to me later. This part is very much speculative, but I would suspect that it's very much tied to the idea of  [human exceptionalism](https://en.wikipedia.org/wiki/Anthropocentrism).
![[human_exceptionalism.jpg]]
Illustration by Bill Sanderson, New Scientist, 13 May 1976

This also serves as a reference for me when I meet a person with a more Machine-Learning background that without putting much thought to the problem, would claim that since *hard* problems such as language and vision have been solved all we need to do is slam that model in a moving agent and the embodiment problem is solved. With a convenient backup plan that is "Well the hardware isn't there yet!" if this fails.

# TODO
Read those so that I'm not referencing shit I haven't read
* https://evjang.com/2022/07/23/robotics-generative.html
* https://www.economist.com/special-report/2016/06/23/automation-and-anxiety
# References
This [Twitter link](https://twitter.com/DhruvBatraDB/status/1641823326741102600)
I think this is the [Economist article I read long time ago](https://www.economist.com/special-report/2016/06/23/automation-and-anxiety)

https://www.economist.com/sites/default/files/ai_mailout.pdf
