# Yay Robots!

This document is meant to outline and track the work I do this summer (2017) at Georgia Tech, working in Dr Chernova's RAIL Lab.

## Initial problem statement

The overall challenge is to apply LfD techniques to autonomous mobile robots that currently receive human-intervention in the event of failure to complete a task. One example is with delivery robots in hospitals, where failure is not tolerable. If the robot gets stuff or confused, a human operator takes over. We see this human intervention as a "demonstration" from which the robot should be able to learn. If a robot encounters the same issue, it should be able to overcome it with little or no intervention. At the end of this summer, we hope to demonstrate an autonomous mobile robot learning from human intervention.

## First things to do

 - [X] Setup desktop and development environment
 - [ ] Pick a domain, or example for demonstrating and testing
 - [ ] Do more background research on LfD
 - [ ] Get tele-op and navigation working with Turtlebot or Prentice
 - [ ] Identify a set of failure states that we want to learn from, and what kinds of information we have to learn from
 - [ ] Figure out when we need an intervention, and what kinds of intervention we want
 - [ ] Be the very best, like no one ever was!

## Papers I plan to read

 - [X] Survey of Learning from Demonstration (Chernova et al)
 - [ ] probably lots more...

## Stuff I've done
 - [X] Setup turtle bot in Gazebo and ran the gmapping and amcl planning demo.
 - [ ] Made a modified version of turtlebot_teleop_key that only works when planning fails
