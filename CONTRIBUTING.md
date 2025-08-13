# Contributing

We welcome PRs that:
- Add new placement failure scenarios
- Improve clarity or diagrams
- Update references to latest AWS docs

## How to Contribute
1. Fork this repo
2. Create a branch: `git checkout -b feature/new-scenario`
3. Add your `.md` file under `scenarios/`
4. (Optional) Add diagrams under `diagrams/` and reference them in your scenario
5. Commit and push
6. Open a PR

## Scenario Template
```md
# Scenario Name
**Root Cause:**  
**Placement Strategy / Constraints:**  
**Workload Type:**  
**Symptoms:**  
**Resolution:**  
**References:**


---

## **Example Scenario File** (`scenarios/insufficient-resources.md`)
```md
# Insufficient Cluster Resources

**Root Cause:**  
No container instance has enough free CPU/memory to run the task. Often occurs during rolling updates when ECS temporarily needs extra headroom.

**Placement Strategy / Constraints:**  
Default spread; no special constraints.

**Workload Type:**  
ECS on EC2 (services or standalone tasks).

**Symptoms:**  
- Tasks stuck in `PENDING`
- Event: `insufficient CPU units available` or `insufficient memory available`

**Resolution:**  
- Add capacity (scale out EC2 cluster or switch to larger instances)
- Reduce task resource reservations
- Adjust deployment config to require fewer overlapping tasks
- Use capacity providers with auto scaling

**References:**  
- [AWS ECS Docs – Placement Strategies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html)
