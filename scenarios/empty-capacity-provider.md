# Empty Capacity Provider (EC2 Launch Type)

**Root Cause**  
The ECS service was configured to use an EC2 capacity provider, but no instances were registered (e.g., ASG not scaled up or misconfigured), leading to "EMPTY CAPACITY PROVIDER" placement failures.

**Placement Strategy / Constraints**  
Not strategy-specific; failure happens because the selected capacity provider has no active instances.

**Workload Type**  
ECS on EC2 (service or standalone tasks).

**Symptoms**  
- Tasks stuck in `PENDING` or `PROVISIONING` then fail.  
- Event/Error: `TaskFailedToStart: EMPTY CAPACITY PROVIDER`.

**Resolution**  
- Ensure the Auto Scaling Group has `desired` or `min` size > 0.  
- Configure managed scaling correctly for your capacity provider.  
- Verify that container instances are properly registered to the cluster.

**References:**  
- [Stack Overflow – ECS Task fails to provision due to EMPTY CAPACITY PROVIDER](https://stackoverflow.com/questions/77792296/aws-ecs-task-fails-to-provision-due-to-empty-capacity-provider)  
- [AWS API Docs – EMPTY CAPACITY PROVIDER failure explanation](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/api_failures_messages.html#TaskFailedToStart_FAILURES)  
