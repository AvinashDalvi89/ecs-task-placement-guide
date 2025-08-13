# Constraint & Strategy Mismatch

**Root Cause**  
A placement strategy conflicts with a placement constraint. For example, the constraint requires `ecs.instance-type == t2.micro`, but the strategy is set to spread across instance types. ECS places one task correctly, then fails to place the second task because of the conflict.

**Placement Strategy / Constraints**  
Spread across instance types alongside a constraint on instance type or custom attributes.

**Workload Type**  
ECS on EC2 (clusters with mixed instance types).

**Symptoms**  
- One task starts successfully, others stay in `PENDING`.  
- Event: “no container instance met all of its requirements”.

**Resolution**  
Align strategy and constraints. For example, switch to `binpack` to pack multiple tasks onto the matching instance.

**References:**  
- Official AWS ECS guide on placement constraints:  
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-constraints.html  
- Real-world example on Stack Overflow:  
  https://stackoverflow.com/questions/73513296/ecs-not-respecting-task-placement-constraint  
