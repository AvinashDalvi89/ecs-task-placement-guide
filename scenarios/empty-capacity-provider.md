# Empty Capacity Provider / Launch Type Mismatch

**Root Cause:**  
The chosen capacity provider or launch type has no matching resources.  
Example: Service uses EC2 capacity provider, but the ASG has zero running instances.

**Placement Strategy / Constraints:**  
Not strategy-specific; failure due to unavailable capacity.

**Workload Type:**  
ECS on EC2 or Fargate (services or standalone tasks).

**Symptoms:**  
- Tasks in `PENDING` with "EMPTY CAPACITY PROVIDER" error
- No container instances match launch type

**Resolution:**  
- Start instances for EC2 capacity providers
- Adjust provider auto scaling
- Match launch type to available capacity

**References:**  
- [AWS ECS – Capacity Providers](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cluster-capacity-providers.html)  
- [AWS re:Post – Empty Capacity Provider Error](https://repost.aws/knowledge-center/ecs-empty-capacity-provider)
