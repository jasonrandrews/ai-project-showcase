---
layout: ../../layouts/ProjectLayout.astro
title: "Port software to Arm using AI developer tools"
summary: "Use AI developer tools to port PerfSpect, an Intel command-line tool designed to optimize Linux server software, to Arm."
author: "Jason Andrews"
---

## Challenge

A cloud developer uses [PerfSpect](https://github.com/intel/PerfSpect) to monitor server performance by extracting PMU information from a running system and reports the data to Grafana for visualization. PerfSpect does not work on Arm Linux systems and needs to be ported. It involves a number of Docker containers used to build the software, some of which download and install pre-built tools. A number of dependencies are very specific to x86 architecture features and are not applicable to Arm.

The source code is written in Go and compiled using Makefiles.

## Solution

The [Amazon Q CLI](https://learn.arm.com/install-guides/aws-q-cli/) is able to monitor the build process, read the error messages, and make fixes to get the project to build on Arm. 

Using an AI developer tool to port software is best done as a multi-step process. 

The general steps are:
- Find out where the friction is by inspecting the code, Makefiles, and Dockerfiles to find things that won't work on Arm
- Plow through the build process and let Amazon Q modify anything needed to get a working build (destroying the original environment in the process)
- Use Amazon Q CLI to give more specific instructions to make targeted changes while maintaining the original project functionality 

This process results in a working initial port of PerfSpect.

## Results

The initial port to get a working `perfspect` binary is completed in a [fork on GitHub](https://github.com/jasonrandrews/PerfSpect). 

You can view the changes in the [initial commit](https://github.com/intel/PerfSpect/compare/main...jasonrandrews:PerfSpect:main). 

Using AI developer tools for software porting to Arm accelerates the porting time by quickly identifying issues and providing new ideas of how to overcome issues. 