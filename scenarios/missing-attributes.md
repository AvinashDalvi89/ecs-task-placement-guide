# Missing Required Attributes

**Root Cause:**  
Cluster instances lack ECS agent capabilities required by the task.  
Examples:
- awsvpc mode requires `ecs.capability.task-eni`
- Windows tasks need `ecs.os-type=windows`
- GPU tasks need `ecs.capability.gpu`

**Placement Strategy / Constraints:**  
Implicit constraints from task definition.

**Workload Type:**  
ECS on EC2 (not Fargate).

**Symptoms:**  
- Tasks in `PENDING`
- Event: "closest matching container-instance is missing an attribute required by your task"

**Resolution:**  
- Update ECS agent or use ECS-optimized AMI
- Launch instances matching OS/arch
- Enable required ECS agent configs

**References:**  
- [AWS ECS – Attributes and Task Requirements](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-constraints.html#attributes)  
- [AWS re:Post – Missing ECS Capability Attributes](https://repost.aws/knowledge-center/ecs-missing-attribute-task-placement)
