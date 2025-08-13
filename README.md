# ECS Task Placement Guide
> Real-world ECS task placement failure scenarios, their causes, and how to fix them.

## Why This Exists
ECS gives you fine control over where tasks run — but misconfigurations, capacity gaps, and subtle AWS behaviors can keep tasks stuck in `PENDING`.  
This repo collects **real scenarios from the field**, distilled into quick-reference pages.

## Quick Start
| Scenario | Symptom | Quick Fix |
|----------|---------|-----------|
| [Insufficient Resources](scenarios/insufficient-resources.md) | Tasks stuck pending, `insufficient CPU/memory` | Add capacity or reduce reservations |
| [Constraint Mismatch](scenarios/constraint-mismatch.md) | First task runs, others pending | Align strategy with constraints |
| [Port Conflicts](scenarios/port-conflicts.md) | `RESOURCE:PORTS` error | Use dynamic port mapping |
| [Subnet IP Exhaustion](scenarios/subnet-ip-exhaustion.md) | Fargate tasks fail to start | Add subnets / expand CIDR |
| [Empty Capacity Provider](scenarios/empty-capacity-provider.md) | `EMPTY CAPACITY PROVIDER` | Start instances or fix provider |
| [Missing Attributes](scenarios/missing-attributes.md) | Missing capability errors | Update AMI / match OS & features |

## Contributing
We welcome **new scenarios, diagrams, and fixes**. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License
[MIT](LICENSE)
