# Host Port Conflicts

**Root Cause**  
Using a fixed host port in the task definition can prevent new tasks from being placed if that port is already in use on all instances. ECS returns a `RESOURCE:PORTS` failure.

**Placement Strategy / Constraints**  
Any – failure stems from static host port usage.

**Workload Type**  
ECS on EC2 using bridge/host networking or awsvpc with fixed hostPort.

**Symptoms**  
- Tasks remain in `PENDING`.  
- Event: “closest matching container-instance is already using a port required by your task”.

**Resolution**  
Use dynamic port mapping and load balancers to avoid port conflicts, or use a load balancer-backed service.

**References:**  
- AWS port mapping documentation:  
  https://docs.aws.amazon.com/AmazonECS/latest/APIReference/API_PortMapping.html  
- Community case on Stack Overflow:  
  https://stackoverflow.com/questions/60915026/aws-ecs-task-failed-with-reason-resourceports  
- Deployment stack issue and resolution:  
  https://serverfault.com/questions/898952/aws-ecs-unable-to-place-task  
