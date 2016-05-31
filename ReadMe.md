# Yay Robots!

This document is meant to outline and track the work I do this summer (2017) at Georgia Tech, working in Dr Chernova's RAIL Lab.

## Initial problem statement

The overall challenge is to apply LfD techniques to autonomous mobile robots that currently receive human-intervention in the event of failure to complete a task. One example is with delivery robots in hospitals, where failure is not tolerable. If the robot gets stuff or confused, a human operator takes over. We see this human intervention as a "demonstration" from which the robot should be able to learn. If a robot encounters the same issue, it should be able to overcome it with little or no intervention. At the end of this summer, we hope to demonstrate an autonomous mobile robot learning from human intervention.

## First things to do

 - [X] Setup desktop and development environment
 - [ ] Pick a domain, or example for demonstrating and testing
 - [ ] Do more background research on LfD
 - [ ] Get tele-op and navigation working with Turtlebot or Prentice
 - [ ] Figure out when we need an intervention, and what kinds of intervention we want
 - [ ] Be the very best, like no one ever was!

## Papers I plan to read

 - [ ] Survey of Learning from Demonstration (Chernova et al)
 - [ ] probably lots more...

## Initial Unsupervised Brainstorming (5/31/16)

_The following was written the day I first learned about the goal for the project, and is in now way informed or actionable._

Ok, so in terms of demo I think we should start with something very simple. The idea isn't to work on grasping or manipulation, or really even mapping. Like Dr Chernova said, overfitting isn't really a huge issue. So really all we need is the navigation portion. Since the two domains that came up in our talk are hospital robots and hotel robots, I feel like fetch-and-delivery is the general principle. So there really isn't any need for manipulation in this case. Although that could allow our work to expand into different areas. So maybe just start out with the turtle bot, and have it run around the office delivering people cookies, and you just put them in and take them from a basket on the robot. That sounds like fun. So basically I need to give the robot a map, or it could do the mapping itself. I feel like to start we can give it a static map since we know the layout. That also makes it pretty easy to come up with "obstacles" that need manual intervention. Maybe later on we can give it some basic avoidance abilities, that way it's more realistic to what modern robots are capable of. Ok so I could setup the turtle bot, make a map, and use rviz to tell it go to and from places. Then maybe setup robot web tools and make it so we can tell it where to go from the browser. Then once we have that, we need a way to detect failure. The ros nav stack definitely has something like that setup already, so I'm sure we can easily hook into that. So once the planner fails or some other failure condition is met, we want the intervention to occur. At that point, we need to allow teleoperation so the expert can recover from the error manually. During this intervention, we want to capture some data so we can learn from it. That last bit should be the hard part. I think I need to read more about policy forming.

#### Initial thoughts on policy making and the actual leaning:
Given the kinds of domains that we're working in, it doesn't sounds like deep learning is a great idea. Especially since the robots are already 95% autonomous. You just don't get enough demonstrations to learn that way. So we might need to approach it differently. Although, even if we could use deep learning I think we still need to determine what factors we're considering. Which also means I need to learn more about the kinds of failures that occur in various domains. Let's pretend we're only handling navigation errors, where the robot is unable to plan a path. A few reasons that might happen:
 - Something has blocked it's path, and we're not sure if it's temporary or permanent.
   - Cases where there is _no_ other possible path
   - or when the other path is really long.
