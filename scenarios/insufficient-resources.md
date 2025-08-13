# Insufficient Cluster Resources

**Root Cause**  
No container instance has enough free CPU/memory to run the task. This often shows up during rolling updates, because ECS may try to run new tasks *before* stopping old ones—so you need extra headroom.  
- Community example (insufficient memory on t2.micro; deploy needs more capacity): https://www.reddit.com/r/aws/comments/bjefnz/ecs_how_do_you_resolve_the_unable_to_place_a_task/  
- ECS rolling deployments can go up to 200% of desired tasks (needs spare capacity): https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-service-parameters.html

**Placement Strategy / Constraints**  
Usually default (spread). This fails simply because resource requirements (CPU/memory) aren’t met on any single host.

**Workload Type**  
ECS on EC2 (services or standalone tasks). Also seen during service deployments.

**Symptoms**  
- Tasks stuck in `PENDING`  
- Service events like: “unable to place a task… insufficient memory/CPU available”  
- During deployments, service tries to start extra tasks and can’t find capacity

**Resolution**  
- Add capacity (scale out the ASG / use larger instances)  
- Reduce task reservations (CPU/memory)  
- Adjust deployment config (lower `maximumPercent` / `minimumHealthyPercent`) so you don’t need as much overlap  
- Use capacity providers with autoscaling to add instances when tasks are pending  
- Consider Fargate for this service if you want AWS-managed capacity

**References**  
- Reddit thread (real case: insufficient memory during redeploy):  
  https://www.reddit.com/r/aws/comments/bjefnz/ecs_how_do_you_resolve_the_unable_to_place_a_task/  
- ECS: Update service parameters (`maximumPercent` up to 200%, needs capacity):  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-service-parameters.html  
- ECS service event messages (insufficient CPU/MEM examples):  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-event-messages-list.html
