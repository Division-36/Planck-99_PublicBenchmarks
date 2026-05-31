# Planck-99 — Behavioral Malware Classifier for Embedded Linux

**37KB. 34ns. 96.28% accuracy on 10 years of unseen IoT malware.**

Planck-99 is a deterministic, syscall-based malware classifier built 
for embedded Linux and MCU-class hardware — the layer where no 
commercial security product currently operates.

---

## The Gap

Traditional behavioral detection requires 50–500MB RAM.  
Embedded Linux devices have 256KB–4MB.  
Every existing vendor fails this constraint by 2–3 orders of magnitude.

The result: 21 billion deployed IoT devices with zero behavioral 
security at the firmware layer. Neros runs on embedded Linux. 
Castelion does too. Neither is secured at this layer.

---

## Benchmark Results

| Metric | Value |
|--------|-------|
| Binary size | 37 KB |
| Median inference latency | 34 ns (σ ≤ 14 ns) |
| Throughput | 29.4M inferences/sec (single CPU core) |
| Accuracy (unseen data) | 96.28% |
| Precision | 97.71% |
| Recall | 97.87% |
| Dataset | ADFA-LD, 2016–2026 IoT malware |
| Generalization ceiling | 51× beyond training trace length |

All benchmarks are reproducible. Scripts and datasets are in this 
repository.

---

## Why the Numbers Hold

**Length-invariant by construction.**  
Input is a 32-dimensional normalized syscall frequency vector — 
ratios, not counts. Trained on traces averaging 863 syscalls. 
Performs correctly on traces of 117,088 syscalls. This is a 
mathematical property of the representation, not empirical luck.

**Deterministic inference.**  
Int8-quantized closed-form dot product. Same input → same output, 
every time. Every classification produces a JSON proof file: 
a complete, reproducible audit trail. EU CRA Article 13 compliant 
by construction.

**Explicit failure modeling.**  
Traces under 500 syscalls produce unstable signals. A gating 
mechanism blocks classification below this threshold. 
FPR on IoT dataset: 12.18% — documented data distribution artifact 
(1:5.3 benign-to-malware ratio). On balanced dataset: 1.45%. 
Production mitigation: 500-syscall gate.

---

## Architecture

- **Language:** C (pure integer, no floating point at inference)
- **Classifier:** Int8-quantized dot product against precomputed 
  weight matrix
- **Input:** 32-dimensional normalized syscall frequency vector
- **Output:** Binary classification + JSON proof file
- **Dependencies:** None. No GPU, no network, no OS requirement 
  beyond a C controller.

---

## What's in This Repository

```
/IoTsyscalls              — syscall frequency datasets
/OriginalTrained_dataset  — training data (ADFA-LD)
/linuxStaticSyscalls_MALWARES — malware syscall traces
Planck-99_benchmark_paper.pdf    — full 8-page technical paper
Planck-99_TechnicalBrief.pdf     — architecture deep-dive
planck99_business_pitch.pdf      — market context and business model
```

---

## Regulatory Context

**EU Cyber Resilience Act — August 2027.**  
Every connected device sold in Europe must demonstrate on-device, 
traceable security. The JSON proof file addresses Article 13 
traceability requirements by construction.

**US Critical Infrastructure.**  
Volt Typhoon and Flax Typhoon (260,000+ compromised embedded devices, 
FBI/CISA September 2024) confirm the attack surface is the firmware 
layer — exactly where Planck-99 operates.

---

## Status

Active benchmarking across multiple unseen distributions.  
No source code is published — IP protection.  
All benchmark results are reproducible from the datasets and 
methodology in this repository.

---

**Commercial licensing and partnerships:**  
zs.01117875692@gmail.com

*Planck-99 is proprietary technology developed under Division-36.  
All rights reserved.*
