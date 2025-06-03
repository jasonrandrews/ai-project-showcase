---
layout: ../../layouts/ProjectLayout.astro
title: "Improve adler32 performance using NEON intrinsics"
summary: "A Go implementation of the Adler-32 checksum algorithm with the core update function implemented in C, optimized with Arm NEON instructions for superior performance."
author: "Jason Andrews"
---

## Challenge

A cloud software developer reported the adler32 checksum function built into the standard Go library was running significantly slower than expected and was a significant bottleneck on an Arm Neoverse N1 server. It was running much slower compared to other architectures. 

Rewriting the built-in Go implementation and contributing upstream is a long process that will not immediately help the project. 

Writing a new version using NEON intrinsics is possible, but tedious work and beyond the coding skills of most cloud developers. Even with the right skills, it's a time consuming task. 

## Solution

AI development tools like GitHub Copilot can work in agent mode to create:
- NEON implementation to compare to the standard library
- Test program 
- Test cases for various input patterns
- Experiment with compilers and compiler flags
- Automatically generate summary of results

AI development tools are not great at complex NEON coding. Reaching a working solution took numerous attempts to achieve correct function and incased performance. More work is needed in AI tools to improve coding at this level.

## Results

Using AI development tools allows this challenge to be solved in hours instead days. It's a probably that would not be attempted without AI tools because the required skills, the time it takes, and uncertainty of results would likely mean to skip the problem.

The optimized implementation achieves consistent performance advantages over the standard library. Benchmarks were performed on different Arm processors:

### Arm Neoverse N1 results

| Data Size | NEON Implementation | Standard Library | Improvement  |
|-----------|---------------------|------------------|--------------|
| 10KB      | 5,479 ns/op         | 6,733 ns/op      | 18.6% faster |
| 1MB       | 503,957 ns/op       | 674,823 ns/op    | 25.3% faster |
| 10MB      | 4,997,849 ns/op     | 6,731,980 ns/op  | 25.8% faster |


You can find out more about solving the challenge using GitHub Copilot by reading [Write NEON intrinsics using GitHub Copilot to improve Adler32 performance](https://learn.arm.com/learning-paths/cross-platform/adler32/).

The complete project is also in the [adler32 GitHub repository](https://github.com/jasonrandrews/stackadler32-neon). The entire repository, including the README file, was generated using Copilot.
