# Subnet IP Exhaustion (Fargate)

**Root Cause:**  
Each Fargate task requires an IP from the selected subnet. If no free IPs are available, ECS cannot place the task.

**Placement Strategy / Constraints:**  
No explicit strategy; tasks are constrained by the subnets provided.

**Workload Type:**  
ECS on Fargate with awsvpc networking.

**Symptoms:**  
- Tasks fail to start in `PENDING`
- Error: "insufficient free addresses in subnet"

**Resolution:**  
- Use larger subnets
- Add subnets in more AZs to the service/task networking config
- Expand VPC CIDR if needed

**References:**  
- [AWS re:Post – ECS Fargate Subnet Capacity Issues](https://repost.aws/knowledge-center/ecs-fargate-task-subnet-ip)  
- [AWS ECS – Service Networking](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-networking.html)
