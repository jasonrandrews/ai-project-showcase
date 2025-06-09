---
layout: ../../layouts/ProjectLayout.astro
title: "AI-ified the Arm Design System"
summary: "Re-shaped ADS documentation for AI Agents, enabling rapid web prototypes with Arm look/feel."
author: "Zach Lasiuk"
---

## Challenge

AI tools can create websites based on text specifications in an instant. However, making these websites look and feel Arm shaped is more complicated. Currently the Arm standard is our Arm Design System (ADS). AI Agents cannot access the ADS documentation (which isn't formatted for best use by agents anyways) and there is no central place or file with examples to draw from. 

## Solution

The ADS docs and component specs, for React and VinellaJS applications, were converted into an AI Agent-digestible format -- structured html docs with clear explinations and examples. This enables Agents to auto-wire ADS components and leverage the standardized Arm grid and color pallete. 

## Results

These docs were used alongside GitHub Copilot Agent to create a single-page TCO prototype for the ACM project. Using these docs **cut down on prototyping time by weeks**, avoiding consistent back and forth by checking docs. It replicated successful patterns (logged in one example location) while avoiding common bugs.




