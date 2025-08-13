# Subnet IP Exhaustion (Fargate)

**Root Cause**  
Fargate tasks need an IP per task from the specified subnet. If the subnet’s IP pool is full, ECS cannot place the task.

**Placement Strategy / Constraints**  
No specific strategy; limited by `awsvpc` networking and subnet configuration.

**Workload Type**  
ECS on Fargate.

**Symptoms**  
- Tasks stuck in `PENDING`.  
- Error: “insufficient free addresses in subnet”.

**Resolution**  
Use larger subnets, multiple AZs, or expand the VPC CIDR block.

**References:**  
- AWS Knowledge Center:  
  https://repost.aws/knowledge-center/ecs-fargate-task-subnet-ip  
- AWS ECS Service Networking guide:  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-networking.html  
