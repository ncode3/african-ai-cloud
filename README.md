# African AI Cloud Reference Architecture

A design and learning repository for small-footprint, locally operated AI infrastructure.

## Project Status

**Design-stage reference implementation.** This repository documents architecture decisions, infrastructure experiments, and planned labs. Files labeled as drafts or “coming soon” are roadmap items, not completed production modules.

This project does not represent a commercial cloud service, production service-level agreement, or validated cost benchmark.

## Purpose

The goal is to make private-cloud and edge-AI infrastructure understandable, reproducible, and teachable. The reference model is intended for universities, workforce programs, community labs, and operators evaluating local compute.

The work focuses on five questions:

1. How should compute, storage, networking, and security be assembled at small scale?
2. Which workloads benefit from local or edge deployment?
3. What operational skills are required to run the stack safely?
4. How can infrastructure be documented as a repeatable learning environment?
5. Which assumptions must be tested before the model is expanded to another site?

## Reference Stack

| Layer | Technologies under evaluation | Learning outcome |
|---|---|---|
| Workloads | Local inference, computer vision, APIs | Deploy and observe real applications |
| Containers | Kubernetes and OpenShift | Operate scheduled, resilient workloads |
| Private cloud | OpenStack | Provision compute, network, and storage services |
| Virtualization | KVM and QEMU | Manage hosts, virtual machines, and resource isolation |
| Data | Object, block, and shared storage | Match storage design to workload requirements |
| Network | VLANs, routing, VPN, firewalls | Segment traffic and control trust boundaries |
| Hardware | Commodity servers and edge systems | Understand power, cooling, capacity, and lifecycle |

## Architecture Principles

- **Local-first where justified:** Use local compute when latency, control, data residency, or training value warrants it.
- **Hybrid by design:** Public cloud remains an option when it is the right operational or economic choice.
- **Security at every layer:** Separate management, workload, user, and observability traffic.
- **Measure before scaling:** Record utilization, latency, power, thermal, reliability, and support data.
- **Reproducible operations:** Infrastructure changes should be versioned, reviewed, and recoverable.
- **Operator development:** Every component should support a documented lab or runbook.

## Repository Map

```text
architecture/          Reference diagrams and design specifications
docs/                  Hardware, networking, power, cooling, and economics notes
lessons/               Planned and completed operator labs
scripts/terraform/     Infrastructure-as-code proof of concept
```

## Current Work

| Workstream | Status |
|---|---|
| Reference architecture | In progress |
| Terraform proof of concept | Available for review |
| Hardware and network specifications | Draft |
| KVM, OpenStack, and OpenShift labs | Planned |
| Local inference labs | Planned |
| Monitoring and incident runbooks | Planned |
| Cost and power model | Requires measured data |

## Security

Never commit credentials, private keys, state files, or site-specific network details. Use environment variables or a secrets manager, and review every infrastructure plan before applying it.

Security concerns should be reported privately. See [SECURITY.md](SECURITY.md) when available; do not place sensitive findings in a public issue.

## Contributing

Contributions should improve a reproducible design, lab, test, or operating procedure. A useful pull request should state:

- the problem being addressed;
- the tested environment;
- exact validation steps;
- security and rollback considerations;
- any assumptions that still require field data.

## Related Work

- [Atlanta AI & Robotics Initiative](https://atlanta-robotics.org)
- [AARI Edge Infrastructure](https://github.com/ncode3/AARI-Edge-Infrastructure)
- [AARI Azure Robot Ops](https://github.com/ncode3/aari-azure-robot-ops)

---

Maintained by Nolan S. Code for the Atlanta AI & Robotics Initiative.
