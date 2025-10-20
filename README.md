# African AI Cloud — Learning Project

Exploring a tiny "my-own-AWS" using Linux + automation.  
This is a **learning project**, not a commercial product.

## What This Is

I'm learning to build cloud infrastructure by migrating my application (Heart Pattern) from AWS to self-hosted RHEL infrastructure. This is about understanding infrastructure from first principles.

## Current Status

**Week 0-1: Foundation** ✅
- Learning RHCSA fundamentals
- Built 3-node OpenShift cluster with Dave (Red Hat SA mentor)
- Deployed production-grade Kubernetes on VMware
- Learned overcommitment, caching, resource planning

**Week 2-8: Deep Dive** 🎯
- Monitoring & observability
- AI inference workloads
- Agentic AI (infrastructure operations)
- Production troubleshooting

**Week 9-16: Proof of Concept** ⏳
- Migrate Heart Pattern from AWS
- Implement Redis caching
- Measure performance improvements
- Document cost savings

## Proof-of-Concept Ladder

✅ SSH to a server  
✅ Deploy a demo app  
✅ Run an AI agent  
✅ Build a 3-node cluster  
🎯 Migrate HeartPattern (current milestone)  
⏳ Serve external users (future)  
⏳ Explore quantum (long term)

## Goals

1. **Learn by doing** - Hands-on with real infrastructure
2. **Migrate Heart Pattern** - From AWS to self-hosted (proof)
3. **Document everything** - So I (and others) can learn
4. **Measure results** - Cost savings, performance, lessons

## Tech Stack

- **OS**: Red Hat Enterprise Linux 9
- **Virtualization**: KVM/QEMU (3-node cluster)
- **Orchestration**: OpenShift (Kubernetes)
- **Automation**: Ansible, Python, Bash
- **Monitoring**: Prometheus, Grafana
- **Storage**: Ceph (distributed storage)
- **Caching**: Redis (performance optimization)

## Why?

After 8 years as Microsoft Solution Architect, I realized:
- I designed cloud solutions without understanding infrastructure
- AI tools (Cursor, v0) taught me to build FAST but not RIGHT
- My own app (Heart Pattern) is slow because I don't know caching
- Infrastructure knowledge = foundation for everything else

## What I'm Learning

### Infrastructure Fundamentals
- Resource planning (CPU, memory, storage)
- Overcommitment strategies (how clouds make money)
- Caching architectures (the secret to performance)
- Network isolation (VLANs, security)
- Monitoring & troubleshooting (Prometheus, OOM killer)

### The Gap
AI coding tools generate beautiful apps quickly.
But they don't teach infrastructure, caching, or optimization.
That's the gap I'm filling.

## Structure

- `/docs` - Architecture, plans, deep dives
- `/weekly-log` - Progress updates
- `/infrastructure` - Ansible playbooks, configs (future)
- `/monitoring` - Prometheus/Grafana setup (future)

## The Bigger Vision

If successful, this becomes a blueprint for:
- African founders seeking data sovereignty
- Cost-effective cloud infrastructure
- Open-source alternatives to AWS
- Infrastructure education

But for now: **Learning by doing.**

## Not Goals (Yet)

This is NOT (yet) a commercial venture. It's a learning project that might evolve.

I'm not building:
- ❌ A commercial cloud platform (yet)
- ❌ Quantum computing (Phase 4, years away)
- ❌ Multi-region infrastructure (one location for now)

## Follow Along

- GitHub (this repo): Documentation and learning
- GitHub (sibling): [rhcsa-learning-journey](https://github.com/ncode3/rhcsa-learning-journey)
- LinkedIn: [(https://www.linkedin.com/in/nolan-s-code-mba/)]

## License

MIT - Use, learn, share freely.

---

**Current Focus**: Adding Redis caching to Heart Pattern (Week 2-8)  
**Next Milestone**: AWS migration (Week 9-16)
