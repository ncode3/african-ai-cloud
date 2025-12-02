# African AI Cloud — Learning Project

*From proof-of-concept to production infrastructure for AI sovereignty.*

## Vision

Demonstrate that AI infrastructure doesn't require AWS/Azure/GCP.

Africa has:
- 300+ days of sunshine (solar power)
- Land (data centers)
- Talent (engineers)
- Lower costs (40-50% vs Western cloud)

What's missing: Infrastructure expertise and initial capital.

**This project:** Prove the model at micro-scale, document for replication.

---

## Current Implementation

### Atlanta AI & Robotics Initiative (Pilot)

A distributed data center teaching HBCU students production AI infrastructure:

**Primary Site (Dave's GDC):**
- 3x Dell PowerEdge servers
- KVM hypervisor
- 3-node OpenShift cluster
- Production AI workloads (SAMMO Fight IQ)
- Location: Atlanta, GA

**Secondary Site (Building Now):**
- 2x Dell PowerEdge servers
- OpenStack virtualization layer
- OpenShift deployment
- Site-to-site VPN (WireGuard)
- Location: Atlanta, GA

**Stack:**
- **Compute:** Red Hat OpenShift (Kubernetes)
- **Virtualization:** KVM / Red Hat OpenStack
- **Security:** Palo Alto architecture
- **Networking:** Enterprise switches (Arista/Cisco)
- **Cost:** ~$2,000 CapEx (vs $500+/month cloud)

---

## The Economics

### Cloud Cost (AWS/Azure):
```
3-node Kubernetes cluster: $300-500/month
GPU instances for AI: $1,000+/month
Storage (1TB): $100/month
Bandwidth: $100+/month

Total: $1,500-1,800/month = $18-22k/year
```

### Bare Metal Cost:
```
3x refurb servers: $600 (one-time)
Network equipment: $300 (one-time)
Power: $50/month (solar reducible)
Internet: $100/month

Year 1: $2,700
Year 2+: $1,800/year

5-year savings: $80,000+
```

**Scale this to Africa:** 40-50% cost advantage over Western cloud providers.

---

## The Infrastructure Dream Team

Building this with 80+ years combined experience:

- **Dave (Red Hat):** 20+ years infrastructure, OpenShift architect
- **Nick (Red Hat):** 25+ years virtualization, OpenStack expert
- **Doran (Palo Alto):** 20+ years security, enterprise defense
- **Nolan (Ex-Microsoft):** 8 years solutions, $100M+ revenue

Not "homelab enthusiasts." Production infrastructure veterans.

---

## Lessons & Documentation

### Phase 1: Hardware Selection
- [Server specs and sourcing](docs/hardware-selection.md)
- [Network equipment guide](docs/networking.md)
- [Power and cooling considerations](docs/power-cooling.md)

### Phase 2: Base Infrastructure
- [KVM installation and configuration](lessons/kvm-setup.md)
- [OpenStack deployment](lessons/openstack-deployment.md)
- [Network configuration](lessons/network-config.md)

### Phase 3: Container Platform
- [OpenShift on bare metal](lessons/openshift-baremetal.md)
- [Storage configuration](lessons/storage-setup.md)
- [Multi-site architecture](lessons/distributed-setup.md)

### Phase 4: AI Workloads
- [Local AI inference](lessons/local-inference.md)
- [GPU integration](lessons/gpu-setup.md)
- [SAMMO Fight IQ case study](lessons/sammo-deployment.md)

### Phase 5: Operations
- [Monitoring and logging](lessons/monitoring.md)
- [Backup and disaster recovery](lessons/backup-dr.md)
- [Security hardening](lessons/security.md)

---

## Real-World Impact

**Atlanta AI & Robotics Initiative (501c3):**
- Teaching HBCU students production infrastructure
- First cohort: Morehouse College (40 students)
- Job outcomes: $115k infrastructure role (first graduate)
- Next workshop: February 2026 ("Deploy a Website on Bare Metal")

**Corporate Partnerships (In Progress):**
- Red Hat (potential curriculum sponsor)
- Microsoft (partnership discussions)
- Palo Alto Networks (security architecture)
- NVIDIA (exploring GPU grants)

---

## The African Vision (Long-term)

### Phase 1: Prove the Model (Current)
- Atlanta pilot: 2 sites, 10-20 students
- Demonstrate cost savings, educational outcomes
- Document everything for replication

### Phase 2: Scale to HBCUs (2026-2027)
- 10 HBCUs, 500 students/year
- Train-the-trainers model
- Corporate partnerships for funding

### Phase 3: African Deployment (2028+)
- Partner with African universities
- Replicate infrastructure model
- Solar-powered data centers
- Train local engineers
- Compete with Western cloud at 40-50% lower cost

---

## Why This Matters

**For HBCUs:**
- Students learn production skills (not just theory)
- Job placement in $100k+ infrastructure roles
- Closes the opportunity gap

**For Africa:**
- Demonstrates AI infrastructure sovereignty is possible
- Proves economic viability (cost advantage)
- Creates local jobs and expertise
- Reduces dependence on Western cloud

**For Industry:**
- Solves talent shortage (trained engineers)
- Demonstrates bare metal viability for AI
- Shows alternative to cloud monopolies

---

## Get Involved

**Students:** 
- Atlanta Robotics workshops (free, hands-on)
- Email: nolan@atlanta-robotics.org

**Corporate Partners:**
- Hardware grants, software licenses, job pipelines
- Contact: nolan@atlanta-robotics.org

**Contributors:**
- Documentation, lessons, architecture reviews
- Submit PRs or open issues

---

## Links

- [Atlanta AI & Robotics Initiative](https://atlanta-robotics.org)
- [LinkedIn: Nolan Code](https://linkedin.com/in/nolanscode)
- [RHCSA Learning Journey](https://github.com/ncode3/rhcsa-learning-journey)

---

*"Great things start in small rooms."* — OutKast

We're starting in a garage. Building for a continent.

---

*Last Updated: December 2024*
