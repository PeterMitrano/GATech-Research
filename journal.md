## Initial Unsupervised Brainstorming (5/31/16)

_The following was written the day I first learned about the goal for the project, and is in now way informed or actionable._

Ok, so in terms of demo I think we should start with something very simple. The idea isn't to work on grasping or manipulation, or really even mapping. Like Dr Chernova said, over-fitting isn't really a huge issue. So really all we need is the navigation portion. Since the two domains that came up in our talk are hospital robots and hotel robots, I feel like fetch-and-delivery is the general principle. So there really isn't any need for manipulation in this case. Although that could allow our work to expand into different areas. So maybe just start out with the turtle bot, and have it run around the office delivering people cookies, and you just put them in and take them from a basket on the robot. That sounds like fun. So basically I need to give the robot a map, or it could do the mapping itself. I feel like to start we can give it a static map since we know the layout. That also makes it pretty easy to come up with "obstacles" that need manual intervention. Maybe later on we can give it some basic avoidance abilities, that way it's more realistic to what modern robots are capable of. Ok so I could setup the turtle bot, make a map, and use rviz to tell it go to and from places. Then maybe setup robot web tools and make it so we can tell it where to go from the browser. Then once we have that, we need a way to detect failure. The ros nav stack definitely has something like that setup already, so I'm sure we can easily hook into that. So once the planner fails or some other failure condition is met, we want the intervention to occur. At that point, we need to allow teleoperation so the expert can recover from the error manually. During this intervention, we want to capture some data so we can learn from it. That last bit should be the hard part. I think I need to read more about policy forming.

#### Initial thoughts on policy making and the actual leaning:
Given the kinds of domains that we're working in, it doesn't sounds like deep learning is a great idea. Especially since the robots are already 95% autonomous. You just don't get enough demonstrations to learn that way. So we might need to approach it differently. Although, even if we could use deep learning I think we still need to determine what factors we're considering. Which also means I need to learn more about the kinds of failures that occur in various domains. Let's pretend we're only handling navigation errors, where the robot is unable to plan a path. A few reasons that might happen:
 - Something has blocked it's path, and we're not sure if it's temporary or permanent.
   - Cases where there is _no_ other possible path
   - or when the other path is really long.

So deep learning might be able to help us determine what kinds of obstacles are temporary, and which ones are permanent. But that sounds really hard. I'm not sure which inputs we'd use. For instance, it would be cool if seeing orange traffic cones or signs could indicate construction. But in that case, wouldn't it be way easier to just have a special sign that the robot can read that indicates "construction", so then we'd know not to wait. So we could turn this into a computer vision project about determining if obstacles are temporary, but that sounds really hard. I feel like I need to know more about the failure cases we're trying to handle.

## More brainstorming (6/1/16)

So I finished reading the Survey of LfD, and a bunch of things seem like they will be applicable.

 - We are using "teleoperation" as our demonstration approach, so our embodiment and record mapping at the Identify mapping
 - We can eliminate issues of the demonstrator working with more data than the robot because the robot is teleoperated using the robots camera and sensors
 - It's possible to demonstrate only with states, and no actions. Specifically, the demonstration could be the path out which is to be executed by a planner, rather than the actions the planners take. This won't work in every case though, because most of the "intervention" cases are caused by the planner failing.
 - If we learn on a per-domain basis (ie. One hospital, or one hotel) we don't have many training examples to work with
 - For reward functions, one option is to use teleoperation to show the robot the reward states and thus eliminate long periods of initial exploration that acquire no reward feedback
 - Since a human operator is fully engaged during the demonstration, and may be a domain expert, we could ask them to annotate or provide feedback. This could mean annotating what he is doing, what the issue is. It could also mean criticizing previous attempts at recovery.
 - We only acquire new demonstration when a failure occurs, at which point the intervention occurs
 - Demonstrations may be suboptimal because human teleoperation is difficult, and messy. We may want to employ smoothing or removal of unnecessary actions to the demonstrations.
 - Since we have few demonstrations, we should consider developing a policy from LfD, but letting that policy evolve with RL.

#### Picking a domain we can demo
