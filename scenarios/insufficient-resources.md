# Insufficient Cluster Resources

**Root Cause:**  
No container instance has enough free CPU/memory to run the task. This often occurs during rolling updates when ECS temporarily needs extra headroom.

**Placement Strategy / Constraints:**  
Default spread; no special constraints.

**Workload Type:**  
ECS on EC2 (services or standalone tasks).

**Symptoms:**  
- Tasks stuck in `PENDING`
- Event: `insufficient CPU units available` or `insufficient memory available`

**Resolution:**  
- Add capacity (scale out EC2 cluster or switch to larger instances)
- Reduce task resource reservations
- Adjust deployment config to require fewer overlapping tasks
- Use capacity providers with auto scaling

**References:**  
- [AWS ECS – Task Placement Strategies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html)  
- [AWS re:Post – Insufficient CPU or Memory for ECS Tasks](https://repost.aws/knowledge-center/ecs-task-fail-placement-cpu-memory)
