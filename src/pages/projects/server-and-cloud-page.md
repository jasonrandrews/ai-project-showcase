---
layout: ../../layouts/ProjectLayout.astro
title: "Create a single page view of Server and Cloud Learning Paths"
summary: "Comparing the front page information for over 100 Learning Paths is difficult. Using AI tools to create a single page view greatly simplifies the comparison and makes improvement much easier."
author: "Jason Andrews"
---

## Challenge

As Learning Paths standards change, the review precess improves, and different authors have different ways to explaining the audience and prerequisites it becomes hard to keep consistent standards. Comparing the front page information for 100+ Learning Paths is difficult, but we want to maintain some consistency and compare and contrast the information. 

## Solution

One way to get a better view is to create a single page which displays the key information for all Learning Paths. This makes it easy to see how they differ, how they are the same, and quickly spot things that can be improved. 

AI developer tools such as [v0.dev](https://v0.dev) are a great way to solve the problem. Using v0.dev the data is scraped from learn.arm.com. v0.dev created a website with a card for each Learning Path so they can all viewed at the same time. The entire project is created using prompts, no coding is required.

## AI developer tools used

- v0.dev
- GitHub Copilot

## Results

The v0.dev project automatically generates and hosts (using [Vercel](https://vercel.com)) a single page which is always up to date with the latest Server and Cloud Learning Paths. The page is challenging because the scraping takes time and users don't want to wait. v0.dev is able to implement complex caching and on-demand loading to delivery good performance. 

View the created project at: 
[Migrate applications to Arm servers and cloud instances](https://server-and-cloud.vercel.app/)