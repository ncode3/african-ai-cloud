# Resource Exhaustion: Diagnosis and Prevention

## What Dave Taught Me

When systems exhaust resources, they don't just "fail" - they degrade in predictable ways. Understanding this is critical for production operations.

## CPU Exhaustion

### How It Happens
```
Normal State:
├── Physical CPU: 48 cores
├── Allocated: 192 vCPUs (4:1 overcommit)
├── Actual usage: 30% average
├── Response time: <10ms
└── Everything smooth ✅

CPU Exhaustion:
├── Multiple VMs spike to 100% simultaneously
├── Physical CPU: 95-100% utilized
├── Hypervisor can't keep up
├── VMs compete for CPU time
└── Symptoms appear 🚨
```

### The Progression
```
Stage 1: Slight slowdown (50-100ms)
└── "App feels sluggish"

Stage 2: Noticeable lag (500ms-2s)
└── "Why is everything slow?"

Stage 3: Severe degradation (5-10s)
└── "Is the server down?"

Stage 4: Stops responding (timeouts)
└── "It's dead"

Stage 5: System hangs
└── Can't even SSH in
```

### Diagnosis
```bash
# Check load average
$ uptime
load average: 48.32, 52.17, 45.88  # On 8-core system = BAD

# Check CPU usage
$ top
%Cpu(s): 98.5 us, 1.2 sy, 0.0 ni, 0.0 id

# Per-process
$ ps aux --sort=-%cpu | head
```

### Fix

- Identify CPU-heavy processes
- Scale horizontally (add nodes)
- Optimize code
- Set CPU limits (cgroups)

## Memory Exhaustion (Much Worse!)

### The Death Spiral: Swap Thrashing
```
The Progression:

1. Memory fills up (95%+)
2. System starts using swap (disk)
3. Disk is 1000× slower than RAM
4. CPU maxes out copying RAM ↔ disk
5. Disk I/O maxes out
6. Everything grinds to halt
7. OOM Killer starts killing processes
```

### Why It's Worse Than CPU
```
CPU Exhaustion:
✅ System slows gradually
✅ Can usually recover
✅ No data loss

Memory Exhaustion:
❌ Death spiral (thrashing)
❌ Hard to recover
❌ OOM Killer murders processes
❌ Possible data loss
```

### Symptoms
```
During Swap Thrashing:
├── RAM: 100% full
├── Swap: Growing rapidly
├── CPU: 90-100% (doing NO useful work!)
├── Disk I/O: 95-100%
├── Load average: 10-50× CPU count
└── System essentially frozen
```

### Diagnosis
```bash
# Check memory
$ free -h
              total        used        free
Mem:          128G        128G        0G    # Full!
Swap:          16G         15G        1G    # Nearly full!

# Check swap activity
$ vmstat 1
si    so     # Swap in/out per second
8500  7200   # 8.5 GB/s swap activity = thrashing!

# Check OOM killer
$ dmesg | grep -i "out of memory"
[12345.678] Out of memory: Kill process 15234 (postgres)
[12345.679] Killed process 15234
```

### Fix

**Immediate:**
- Restart memory-hogging process
- Kill non-critical processes
- Reboot if necessary

**Short-term:**
- Add more swap (bandaid)
- Add RAM if possible

**Long-term:**
- Fix memory leaks in code
- Right-size applications
- Set memory limits (cgroups)
- Monitor proactively

## The OOM Killer

### What It Is

Linux's last resort when out of memory. Kills processes to free RAM.

### How It Chooses Victims
```
Scoring Algorithm:
├── High score = More likely to die
├── Factors that increase score:
│   ├── Using lots of memory (biggest factor)
│   ├── Running a long time
│   ├── Low priority
│   └── Not a system process
└── Your app: Usually prime target 🎯

Protected:
├── PID 1 (init/systemd): Never killed
├── Kernel threads: Never killed
├── Critical daemons: Rarely killed
```

### Finding OOM Events
```bash
# Check if OOM ran
$ dmesg | grep -i "out of memory"
$ journalctl -k | grep -i "oom"

# Output if OOM ran:
[12345.678] Out of memory: Kill process 15234 (postgres)
[12345.679] Killed process 15234 total-vm:8GB, anon-rss:6GB

# See what was killed
$ dmesg | grep "Killed process"
```

### Prevention

- Monitor memory usage (alert at 85%)
- Set memory limits (prevent one process hogging all)
- Fix memory leaks
- Add sufficient RAM for workload

## Production Scenarios

### Scenario 1: Mysterious Nightly Crash
```
Problem:
"App crashes every night at 2 AM.
 Looks healthy by morning.
 No errors in app logs."

Investigation:
$ dmesg | grep -i oom
[Oct 19 02:13:45] Out of memory: Kill process (app-worker)
[Oct 18 02:11:22] Out of memory: Kill process (app-worker)

Pattern: OOM every night ~2 AM

Root Cause:
$ crontab -l
0 2 * * * /usr/local/bin/nightly-report

# Script loads ENTIRE database into memory!

Fix:
# Stream data instead of loading all at once
for batch in DB.query_in_batches(batch_size=1000):
    process_batch(batch)
```

### Scenario 2: The Swap Death Spiral
```
Problem:
"System running but EVERYTHING is slow.
 SSH takes 30 seconds.
 Commands take minutes."

Investigation:
$ top
Load average: 43.28  # On 8-core system!

$ free -h
Mem:  128G  128G   0G   # RAM full
Swap:  16G   15G   1G   # Swap nearly full

$ iostat
sda  %util  98.7%  # Disk maxed

Diagnosis: Classic swap thrashing

Immediate Fix:
$ systemctl restart app-service

Permanent Fix:
- Find memory leak
- Add memory limits
- Monitor with alerts
```

### Scenario 3: Noisy Neighbor
```
Problem:
"Database slow today. Yesterday fast.
 Nothing changed in our app."

Investigation:
Your VM looks fine internally.

Real Issue: Physical host
├── Your VM: Normal behavior
├── Neighbor VM 1: Bitcoin mining (100% CPU)
├── Neighbor VM 2: ML training (100% CPU)
├── Result: Physical CPU exhausted
└── Your VM gets less CPU time

Fix:
- Contact provider (if cloud)
- Request VM migration
- Or: Build own infrastructure (what you're doing!)
```

## Monitoring to Prevent This

### Alert Thresholds
```yaml
# Prometheus alerts

CPU Alerts:
- Warning: >80% for 5 minutes
- Critical: >95% for 2 minutes

Memory Alerts:
- Warning: >85% for 2 minutes
- Critical: >95% for 1 minute

Swap Alerts:
- Warning: Any swap usage >1GB
- Critical: Swap >50% full

Disk I/O Alerts:
- Warning: >80% utilization for 5 minutes
- Critical: >95% for 2 minutes

OOM Alerts:
- Critical: Any OOM killer invocation
```

### Dashboard Panels
```
What to Visualize:

1. CPU Usage
   - Current, trend, threshold lines
   
2. Memory Usage
   - RAM used/available
   - Swap usage (should be 0!)
   
3. Disk I/O
   - Utilization %
   - IOPS, throughput
   
4. Load Average
   - 1min, 5min, 15min
   - Compared to CPU count
   
5. OOM Killer Events
   - Count over time
   - Recent victims
   
6. Top Memory Consumers
   - Identify hogs/leaks
```

## Key Lessons

### 1. CPU Exhaustion = Slow
- System degrades gracefully
- Can usually recover
- Monitor and scale

### 2. Memory Exhaustion = Death
- Swap thrashing kills everything
- OOM Killer murders processes
- Much harder to recover
- Prevention is critical

### 3. Monitor Proactively
- Alert at 80-85%, not 95%
- Track trends, not just current values
- Investigate spikes immediately

### 4. Plan Capacity Correctly
- Don't run at 90% utilization
- Leave headroom for bursts
- Scale early, not in emergency

## For Heart Pattern

Will implement:
- Prometheus for metrics collection
- Grafana for visualization
- Alerts for all resource thresholds
- Automatic scaling triggers (future)
- OOM event tracking
- Weekly capacity reviews

Goal: Prevent issues before users notice.

## Resources

- Dave's production war stories
- Hands-on troubleshooting experience
- OpenShift cluster monitoring
- Real-world scenarios

---

**Bottom Line**: Resource exhaustion is predictable. Monitor proactively, respond quickly, prevent systematically.
