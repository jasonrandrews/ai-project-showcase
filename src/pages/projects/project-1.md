---
layout: ../../layouts/ProjectLayout.astro
title: "Accelerate search algorithms used in Databases using SVE2"
summary: "An SVE2 implementation using the MATCH instruction to dramatically make search operations in byte and half word arrays faster on Arm servers."
author: "Pareena Verma"
---

## Challenge

Query-intensive databases (think SAP HANA-style reported scans, JSON parsers, or even a plain old memchr) spend a surprising amount of time doing nothing more than “find the first byte/half-word that equals X.”
When cloud developers run these workloads on Arm based servers they notice hot spots and low performance becuase those tight inner loops are still written as scalar C implementations and even the best compilers can’t safely vectorise them because the loop breaks as soon as a match is found. 

Updating every affected open-source library/database upstream would take months, and hand-rolling a NEON or SVE2 version is niche, error-prone work that most application developers don’t have time for. 

## Solution

Leverage an AI-assisted Agent like Amazon Q to automate the heavy lifting that makes hand-written SIMD code so painful:

1. **Generate an SVE2-optimised implementation**
   *Use the agent to draft and iteratively refine a `MATCH`-based search routine, side-by-side with the scalar C reference.*

2. **Produce a self-contained benchmark harness**
   *The agent scaffolds a test program that builds both variants, adds benchmakring harness and prints speedups.*

3. **Create exhaustive test cases**
   *Random, worst-case, and real-world data patterns ensure functional correctness across byte and half-word modes for different hit rates, iterations and haystack lengths*

4. **Autogenerate a results digest**
   *The agent parses benchmark logs and emits a Markdown summary table ready for the showcase README.*

> Tried a mix of AI coding tools. Current AI coding tools still stumble on intricate SVE2 idioms; getting a *correct and faster* MATCH loop took many trial–error cycles and manual guidance. Improving AI’s grasp of advanced SIMD patterns remains an open area for tool builders.


## Results

The agent automated code generation, test-case creation, compiler-flag exploration, and results aggregation, so human time was spent only on strategic nudges rather than line-by-line instruction wrangling.

This optimisation went from “probably not worth attempting without deep SVE2 instrinsic expertise” to “quick win”—unlocking a verified 90× search-loop speed-up on Arm Neoverse servers the same day I researched the SAP problem.

Performance was recorded on a Graviton4 instance with Ubuntu 24.04 and a dataset of 65,536 elements (2^16), with different hit probabilities:

### Latency (ns per iteration) for Different Hit Rates (8-bit)

| Implementation        | 0% (No Matches) | 0.001%      | 0.01%      | 0.1%      | 1%       |
|-----------------------|-----------------|-------------|------------|-----------|----------|
| Generic Scalar        | 145,042.80      | 79,414.40   | 22,351.20  | 2,244.60  | 332.60   |
| SVE2 MATCH            | 2,180.60        | 1,092.00    | 425.80     | 109.40    | 67.40    |
| SVE2 MATCH Unrolled   | 1,520.20        | 861.60      | 320.20     | 89.60     | 55.60    |

### Latency (ns per iteration) for Different Hit Rates (16-bit)

| Implementation        | 0% (No Matches) | 0.001%     | 0.01%     | 0.1%     | 1%      |
|-----------------------|-----------------|------------|-----------|----------|---------|
| Generic Scalar        | 86,936.80       | 86,882.40  | 33,973.40 | 4,054.80 | 117.60  |
| SVE2 MATCH            | 3,941.40        | 4,012.20   | 1,618.00  | 235.00   | 59.60   |
| SVE2 MATCH Unrolled   | 3,102.00        | 3,192.40   | 1,254.60  | 193.40   | 59.40   |

### Speedup vs Generic Scalar (8-bit)

| Hit Rate | SVE2 MATCH | SVE2 MATCH Unrolled |
|----------|------------|---------------------|
| 0%       | 66.52x     | 95.41x              |
| 0.001%   | 72.72x     | 92.17x              |
| 0.01%    | 52.49x     | 69.80x              |
| 0.1%     | 20.52x     | 25.05x              |
| 1%       | 4.93x      | 5.98x               |

### Speedup vs Generic Scalar (16-bit)

| Hit Rate | SVE2 MATCH | SVE2 MATCH Unrolled |
|----------|------------|---------------------|
| 0%       | 22.06x     | 28.03x              |
| 0.001%   | 21.65x     | 27.22x              |
| 0.01%    | 21.00x     | 27.08x              |
| 0.1%     | 17.25x     | 20.97x              |

Full learning path is available at https://learn.arm.com/learning-paths/servers-and-cloud-computing/sve2-match/

