# The Planet Fitness Cloud Model

## The AWS Origin Story

### Phase 1: Retail Problem (2006)
Amazon had a capacity planning problem:
- Black Friday / Prime Day: Need 10× normal capacity
- Rest of year: Servers sit 80% idle
- Capital expense: Massive
- Utilization: Terrible

**Solution:** Rent out excess capacity → AWS born

### Phase 2: Excess Monetization (2006-2015)
AWS as "retail byproduct":
- Amazon needs capacity for peak retail days
- Rents idle capacity to external customers
- Win-win: Monetize what would otherwise be waste

### Phase 3: Cloud-First Infrastructure (2015-present)
AWS realizes cloud > retail:
- Build infrastructure FOR cloud oversubscription
- No longer just "retail excess" - intentional overcommitment
- Planet Fitness model applied to computing

## The Planet Fitness Business Model

**Gym Economics:**
- Membership: $10/month
- Members: 10,000
- Capacity: 200 people
- Actual daily users: 300 (3% utilization)
- **Business model depends on no-shows**

If everyone showed up → Gym collapses

**Cloud Economics (Same Model):**
- Compute: Pay per use
- Hardware: 1,000 VM capacity
- Sold: 3,000 VMs (3:1 oversubscription)
- Actual usage: 1,000 VMs (67% idle)
- **Business model depends on idle resources**

If everyone maxed out → Region collapses

## Why This Matters for AI Workloads

**Problem:** AI workloads don't follow Planet Fitness patterns

Traditional workloads:
- Web servers: 10-20% CPU average (predictable idle)
- Databases: Steady state (known capacity)
- Batch jobs: Scheduled (plan around it)

AI workloads:
- LLM inference: Unpredictable (10 tokens vs 10,000)
- Model training: Sudden (0% to 100% GPU for hours)
- Batch inference: Spiky (unknown input size until runtime)
- **Can't oversubscribe - demand is too volatile**

## The Alternative: Owned Infrastructure

**Red Hat / OpenShift Model:**
- Customer provisions capacity they ACTUALLY need
- No oversubscription (what you pay for = what you get)
- Predictable costs (no surprise throttling)
- True control (you own the fate)

**Economics:**
- Higher upfront cost (buy hardware)
- Lower long-term cost (no cloud markup)
- Predictable performance (no noisy neighbors)
- True sovereignty (your infrastructure, your control)

## Synthesis: Why Yesterday's AWS Outage Matters

Yesterday's outage wasn't oversubscription failure - it was control plane 
failure. But it exposed the fragility of centralized cloud architecture.

**AWS Architecture:**
- Centralized control plane (single point of failure)
- Regional dependencies (us-east-1 is special)
- Oversubscription model (works until it doesn't)

**Result:** When everyone needs infrastructure simultaneously (outage recovery, 
major event), the model shows its limits.

**For AI:** You can't afford "sorry, your inference is throttled because we 
oversold GPUs." Sovereign infrastructure on OpenShift = control your fate.

---

**Credit:** Thanks to David Taylor for the AWS origin story and Planet Fitness 
analogy. Historical context matters.
