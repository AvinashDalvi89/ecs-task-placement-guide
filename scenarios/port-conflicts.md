# Host Port Conflicts

**Root Cause:**  
Tasks use a fixed host port. ECS can only run one task per instance using that port. If more tasks need to run but the port is already taken, placement fails with `RESOURCE:PORTS`.

**Placement Strategy / Constraints:**  
Any; failure occurs when static host ports are in use.

**Workload Type:**  
ECS on EC2 with bridge or host networking (or awsvpc with fixed hostPort).

**Symptoms:**  
- Tasks remain in `PENDING`
- Event: "closest matching container-instance is already using a port required by your task"

**Resolution:**  
- Use dynamic port mapping
- Attach to a load balancer for traffic routing
- Add more instances if static ports are unavoidable

**References:**  
- [AWS ECS – Service Load Balancing](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-load-balancing.html)  
- [AWS re:Post – Port Already in Use Placement Failures](https://repost.aws/knowledge-center/ecs-service-task-fails-resource-ports)
