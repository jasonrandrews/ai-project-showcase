---
layout: ../../layouts/ProjectLayout.astro
title: "Accelerate Bitmap Scanning in Database Systems with SVE2"
summary: "An SVE2 implementation that dramatically improves bitmap scanning performance for database operations on Arm servers"
author: "Pareena Verma"
---

## Challenge

When cloud native developers migrate their Database systems, particularly those handling analytical workloads to Arm based servers, they can spend significant time on scanning bitmaps for operations like bitmap indexes, bloom filters, and column filtering. These operations are fundamental to query execution and can become performance bottlenecks, especially for large datasets.

Traditional scalar implementations process bits individually or use basic optimizations like byte-level skipping, but they fail to leverage the vector processing capabilities of modern Arm processors. Even advanced compilers struggle to auto-vectorize these operations due to their complex branching patterns.

Hand-writing SVE2 optimized code is extremely tedious and requires deep instruction-level knowledge of the architecture. Developers need to understand vector lengths, predication, specialized instructions, and complex memory access patterns. This creates a high barrier to entry for database engineers who want to leverage these performance benefits but lack specialized SIMD expertise.

Database developers need efficient bitmap scanning implementations that can take advantage of Arm's advanced vector processing capabilities without requiring deep expertise in SIMD programming.

## Solution

Leverage AI agents like Amazon Q and shell-gpt to generate SVE2-optimized code for bitmap scanning operations, dramatically lowering the barrier to entry for developers:

1. **AI-assisted code generation**
   *Use AI agents to generate optimized SVE2 implementations with strategic guidance, eliminating the need for deep instruction-level expertise.*

2. **Implement and compare multiple approaches**
   *Create four implementations: generic scalar, optimized scalar, NEON vector, and SVE2 vector to demonstrate the evolution of optimization techniques.*

3. **Utilize specialized SVE2 instructions and prefetching optimizations**
   *Guide the AI to employ `svcmpne_u8`, `svpnext_b8`, and `svlastb_u8` instructions to efficiently identify and process non-zero bytes in bitmaps.*

4. **Benchmark across different bit densities**
   *Use AI agent to generate the test harness and test performance across multiple bit densities (0% to 10%) to understand the optimal implementation for different scenarios.*

## AI developer tools used

- Amazon Q
- Shell GPT

## Results

The implementation demonstrates significant performance improvements for bitmap scanning operations across different bit densities, w
ith the SVE2 implementation showing particularly impressive results for sparse bitmaps.

By using AI agents like Amazon Q to generate the optimized code, the development process was dramatically simplified. What would norm
ally require weeks of specialized SVE2 programming knowledge was accomplished with strategic guidance to the AI, making advanced vect
or optimizations accessible to database developers without deep SIMD expertise.

Performance was recorded on a Graviton4 instance with Ubuntu 24.04 and a bitmap size of 10 million bits:

### Execution Time (ms)

| Density | Set Bits | Scalar Generic | Scalar Optimized | NEON  | SVE       |
|---------|----------|----------------|------------------|-------|-----------|
| 0.0000  | 0        | 7.169          | 0.456            | 0.056 | 0.093     |
| 0.0001  | 1,000    | 7.176          | 0.477            | 0.090 | 0.109     |
| 0.0010  | 9,996    | 7.236          | 0.591            | 0.377 | 0.249     |
| 0.0100  | 99,511   | 7.821          | 1.570            | 2.252 | 1.353     |
| 0.1000  | 951,491  | 12.817         | 8.336            | 9.106 | 6.770     |

### Speedup vs Generic Scalar

| Density | Scalar Optimized | NEON    | SVE     |
|---------|------------------|---------|---------|
| 0.0000  | 15.72x           | 127.41x | 77.70x  |
| 0.0001  | 15.05x           | 80.12x  | 65.86x  |
| 0.0010  | 12.26x           | 19.35x  | 29.07x  |
| 0.0100  | 5.02x            | 3.49x   | 5.78x   |
| 0.1000  | 1.54x            | 1.40x   | 1.90x   |

The implementation demonstrates that SVE2 instructions provide consistent performance advantages across various bitmap densities, with particularly strong results for the sparse bitmaps commonly encountered in database filtering operations.

This project showcases how AI agents like Amazon Q can bridge the gap between high-performance computing and application development, making advanced SVE2 optimizations accessible to developers without requiring them to become vector instruction experts. With some structural guidance, the AI was able to generate complex SVE2 code that achieves impressive performance gains, democratizing access to the full power of Arm's vector processing capabilities.

Full learning path is available at https://learn.arm.com/learning-paths/servers-and-cloud-computing/bitmap_scan_sve2/
