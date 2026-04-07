# Why This Matters — Planck-99


* Planck-99 is a kernel-level malware detection system that enables real-time threat detection on devices that previously could not run security software.
* It reduces detection latency from milliseconds to nanoseconds and operates within ~37KB, making it viable for IoT, embedded systems, and low-resource environments.
* This allows organizations to deploy behavioral security directly on-device — eliminating reliance on cloud analysis and reducing response time from seconds to instant.


## The Problem

Modern malware detection does not operate where it matters most.

Existing solutions are:
- Too heavy for embedded / IoT systems
- Too slow for real-time detection
- Dependent on long traces or post-execution analysis

As a result, vast numbers of devices operate without effective protection at the behavioral level.

---

## The Solution

Planck-99 is a syscall-based malware classifier designed for **real-time, embedded environments**.

It operates with:
- ~30–70 nanoseconds inference latency
- ~37 KB total system footprint
- No dependency on trace length at inference time

The model runs directly at the system level and enables **continuous behavioral monitoring**.

---

## What Makes It Different

### 1. Length-Invariant Detection
Traditional approaches degrade or slow down with longer traces.

Planck-99 uses **normalized syscall frequency ratios**, making detection:
- Independent of trace length
- Stable across vastly different execution scales

This enables generalization up to **51× beyond training conditions**.

---

### 2. Real-Time Kernel-Level Execution
The system is implemented as a lightweight C kernel component:
- Deterministic latency (nanoseconds)
- No runtime overhead accumulation
- Suitable for continuous monitoring loops

This is not post-analysis — it is **inline detection**.

---

### 3. Embedded-First Design
Planck-99 is designed for environments where ML typically fails:
- IoT devices
- Low-memory systems
- Edge deployments without accelerators

Total footprint fits within tens of kilobytes.

---

### 4. Explicit Failure Modeling
The system identifies and accounts for its limitations:

- Short traces (<500 syscalls) produce unstable signals
- A gating mechanism prevents unreliable classification
- Sliding window ensures continuous accuracy over time

This makes the system **predictable and controllable in production**

---

## Why It Matters

Planck-99 shifts malware detection from:
- Heavy → lightweight  
- Delayed → real-time  
- Server-dependent → device-native  

This enables a new deployment model:

> Behavioral security at the lowest levels of computation.

Devices that previously could not run security models can now:
- Detect threats locally
- Respond instantly
- Operate without external dependencies

---

## The Outcome

- Orders-of-magnitude faster inference (ns vs ms)
- Minimal resource usage (KB vs MB/GB)
- Strong generalization across datasets and time

Planck-99 redefines where malware detection can exist — moving it from the cloud to the device itself.
It is a change in where and how malware detection can exist.

---

## Status

Planck-99 is currently under active testing and benchmarking across multiple datasets, including unseen distributions.

All results, benchmarks, and system details are publicly available in this repository.

---
```
Intellectual Property Notice:
Planck-99 is a proprietary technology developed by Ziad Salah under the Division-36 umbrella.
All rights reserved. Commercial licensing and partnership inquiries: dariangosztafio@gmail.com
```
## Bottom Line

If malware detection is to scale across billions of devices,  
it must become:

- Lightweight  
- Deterministic  
- Always-on  

Planck-99 is a step in that direction.
