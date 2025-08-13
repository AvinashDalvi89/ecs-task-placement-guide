# Missing Required Attributes

**Root Cause**  
The ECS task definition includes requirements that none of the cluster’s container instances meet—such as ENI support, a specific OS, GPU capability, or log driver support.

**Placement Strategy / Constraints**  
Implicit—derived from task definition requirements (e.g., `awsvpc`, Windows OS, GPU resources, logging drivers).

**Workload Type**  
ECS on EC2 (service or standalone tasks).

**Symptoms**  
- Tasks stuck in `PENDING`.  
- Event message:  
  > “The closest matching container-instance is missing an attribute required by your task.”

**Resolution**  
- Ensure instances use the ECS-optimized AMI or run a supported ECS agent.  
- Match task OS/architecture (e.g., Windows task → Windows container instances).  
- Enable required features via ECS agent config (e.g., logging drivers, GPU support).  
- Restart agent or replace instances as needed.

**References:**  
- **Stack Overflow real-world case:**  
  “The closest matching container-instance is missing an attribute required by your task” error; solution includes checking `runtimePlatform` mismatch (ARM vs x86) and cleaning up constraints:  
  https://stackoverflow.com/questions/56290746/ecs-error-the-closest-matching-container-instance-is-missing-an-attribute-requ  

- **Community blog post:**  
  ECS service fails due to missing attribute, even when `ecs-cli check-attributes` shows “None”; fixing mismatched subnets resolved the error:  
  https://cultivatingsoftware.wordpress.com/2023/12/20/aws-missing-required-attribute/  

- **AWS Official Docs:**  
  ECS API failure explanation for `ATTRIBUTE` error and attribute dependencies:  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/api_failures_messages.html#TaskFailedToStart_FAILURES  
  (See `TaskFailedToStart: ATTRIBUTE` section.)
