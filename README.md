# High-Performance Standard Cell Library using MTCMOS in 45nm Technology

![Tool](https://img.shields.io/badge/Tool-Cadence%20Virtuoso-blue)
![Technology](https://img.shields.io/badge/Technology-45nm%20CMOS-orange)
![Technique](https://img.shields.io/badge/Technique-MTCMOS-purple)
![Application](https://img.shields.io/badge/Application-DSP-green)
<!--![Published](https://img.shields.io/badge/Paper-ICDCCS%202025-brightgreen)-->

---

## Overview

This project develops a **high-performance standard cell library using MTCMOS (Multi-Threshold CMOS)** in 45nm technology for DSP applications. The core idea is to use **high-Vt transistors** to minimize leakage power and **low-Vt transistors** to maximize switching speed — achieving an optimized power-performance trade-off.

The complete VLSI design flow was followed: schematic design → simulation → layout → DRC → LVS → RC extraction → post-layout analysis. Four adder architectures were implemented and benchmarked against published literature.

---

## Problem Statement

| Challenge | Impact |
|-----------|--------|
| Increasing leakage power at 45nm | High static power dissipation in standby |
| Conventional CMOS trade-off limitations | Cannot simultaneously achieve low power + high speed |
| Existing libraries not DSP-optimized | Poor scalability for advanced nodes |

---

## Approach — MTCMOS Technique

```
High-Vt Transistors          Low-Vt Transistors
      │                              │
      ▼                              ▼
Reduced leakage current       Faster switching speed
(lower standby power)         (higher performance)
      │                              │
      └──────────────┬───────────────┘
                     ▼
           Balanced PDP (Power × Delay)
           optimized for DSP workloads
```

---

## Design Flow

```
Schematic Design (Cadence Virtuoso)
           │
           ▼
   Pre-layout Simulation
  (Power, Delay, PDP analysis)
           │
           ▼
   Layout Generation
  (Cadence Layout Editor)
           │
           ▼
   DRC — Design Rule Check ✅
           │
           ▼
   LVS — Layout vs Schematic ✅
           │
           ▼
   RC Extraction
           │
           ▼
   Post-layout Simulation
  (Validated against pre-layout)
```

---

## Standard Cells Designed

| Category | Cells |
|----------|-------|
| Basic logic gates | NOT, AND, OR, NAND, NOR |
| Universal gates | NAND-based, NOR-based |
| Exclusive gates | XOR, XNOR |
| Flip-flops | D flip-flop (various drive strengths) |
| Combinational circuits | Hybrid Adder, Carry Select Adder, Brent-Kung Adder, Ripple Carry Adder |

All cells were designed with **multiple drive strengths** to support standard cell library characterization.

---

## Results — Power, Delay, and PDP

### Hybrid Adder

| Method | Delay (ns) | Power (µW) | PDP (ns·µW) |
|--------|-----------|-----------|-------------|
| Hybrid using CSA and Carry Skip Adders      | 0.070 | 494 | 34.58 |
| **Proposed (MTCMOS)** | **0.195** | **19.1** | **3.7245** |

> **PDP improvement: 9.3× lower** than conventional 

### Carry Select Adder (CSLA)

| Method | Delay (ns) | Power (µW) | PDP (ns·µW) |
|--------|-----------|-----------|-------------|
| **Proposed (MTCMOS)** | **0.096** | **82.35** | **7.9056** |
| CSLA using Method 1      | 4062 | 0.0099 | 40.21 |
| CSLA using Method 2      | 8141 | 0.0064 | 52.102 |

> **PDP improvement: 5.1× lower** than conventional-1 , **6.6× lower** than conventional-2 

### Brent-Kung Adder

| Method | Delay (ns) | Power (µW) | PDP (ns·µW) |
|--------|-----------|-----------|-------------|
| **Proposed (MTCMOS)** | **0.0875** | **7.10** | **0.62125** |
| Parallel Prefix      | 37.88 | 3.98 | 150.8224 |
| Parallel Prefix      | 19.39 | 0.9365 | 18.1561 |

> **PDP improvement: 242× lower** than conventional-1, **29× lower** than conventional-2 

### Ripple Carry Adder (RCA)

| Method | Delay (ns) | Power (µW) | PDP (ns·µW) |
|--------|-----------|-----------|-------------|
| **Proposed (MTCMOS)** | **0.0803** | **5.31** | **0.426393** |
| RCA using Basic CMOS      | 0.155 | 235 | 36.425 |
| RCA using Traditional NAND Full Adders      | 108.1 | 0.0003124 | 0.033757 |
| RCA using NAND-HA-FA      | 0.3133 | 0.08295 | 0.025972 |

> **PDP improvement: 85× lower** than Basic CMOS 

### PDP Summary Across All Adders

| Adder | Proposed PDP (ns·µW) | Best Literature PDP | Improvement |
|-------|---------------------|--------------------|-----------| 
| Hybrid Adder | 3.7245 | 34.58 | **9.3×** |
| Carry Select Adder | 7.9056 | 40.21 | **5.1×** |
| Brent-Kung Adder | 0.62125 | 18.1561 | **29×** |
| Ripple Carry Adder | 0.426393 | 36.425 | **85×** |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Cadence Virtuoso | Schematic design and layout |
| Cadence Spectre | ADE | Circuit simulation |
| Cadence DRC | Design Rule Check |
| Cadence LVS | Layout vs Schematic verification |
| RC Extraction | Parasitic extraction for post-layout simulation |
| 45nm CMOS PDK | Technology library |
| Red Hat Linux | Operating environment |

---
