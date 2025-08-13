# Constraint & Strategy Mismatch

**Root Cause:**  
A placement strategy conflicts with a placement constraint, making it impossible to place more than the first task.  
Example: Constraint requires `ecs.instance-type == t2.micro` and a strategy tries to spread tasks across instance types. The first task lands correctly, but the next cannot satisfy both rules.

**Placement Strategy / Constraints:**  
Spread across instance types + constraint on instance type or custom attribute.

**Workload Type:**  
ECS on EC2 (cluster with mixed instance types).

**Symptoms:**  
- First task runs, others remain in `PENDING`
- Event: "no container instance met all of its requirements"

**Resolution:**  
- Align placement strategy with constraints (e.g., switch to `binpack`)
- Ensure enough matching instances exist to satisfy spread constraints

**References:**  
- [AWS ECS – Placement Constraints](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-constraints.html)  
- [Stack Overflow – ECS Task Stuck Due to Constraint/Strategy Conflict](https://stackoverflow.com/questions/73513296/ecs-not-respecting-task-placement-constraint)
