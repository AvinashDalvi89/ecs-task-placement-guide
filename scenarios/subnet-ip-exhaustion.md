# Subnet IP Exhaustion (Fargate)

**Root Cause**  
Fargate tasks using `awsvpc` networking mode need one IP address from the assigned subnet. If your subnet runs out of IPs, ECS cannot launch new tasks.

**Placement Strategy / Constraints**  
No explicit placement strategy — constrained by network configuration.

**Workload Type**  
ECS on Fargate.

**Symptoms**  
- Tasks stuck in `PENDING` or fail to start.  
- Error messages such as:  
  > `Unexpected EC2 error while attempting to Create Network Interface ... insufficient free addresses in subnet`  
  or  
  > `InsufficientFreeAddressesInSubnet`.

**Resolution**  
- Increase the subnet size or CIDR block.  
- Deploy tasks across multiple subnets or AZs.  
- Ensure enough free IP capacity, especially for high concurrency Fargate workloads.

**References:**  
- **Stack Overflow real-world case:**  
  User's state machine task fails due to “InsufficientFreeAddressesInSubnet” in Fargate app:  
  https://stackoverflow.com/questions/67128013/ecs-task-fails-with-insufficientfreeaddressesinsubnet-error-when-running-my-stat

- **Reddit user report:**  
  User hitting this error when running multiple Fargate Spot tasks due to IP limits:  
  https://www.reddit.com/r/aws/comments/136dy0s/getting_insufficientfreeaddressesinsubnet_error/

- **AWS official troubleshooting documentation:**  
  Describes how Fargate tasks fail due to subnet IP exhaustion and advises creating new subnets:  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/failed-to-start-error.html
