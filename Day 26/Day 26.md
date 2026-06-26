# Prior Authorization Workflow Simulator

# Day 26 / 60 – Claude AI Challenge

# Overview:

This project is a single-file, interactive Prior Authorization (PA) Workflow Simulator that visually and experientially demonstrates how a real US healthcare PA request moves through the system — from Patient → Provider → Payer.

Built using HTML, CSS, and Vanilla JavaScript only, the simulator turns a traditionally opaque and frustrating healthcare process into a gamified, drag-and-drop learning experience.

The goal is not just to simulate approvals and denials, but to expose where and why delays actually occur.

# Objective:
To model the real-world Prior Authorization workflow in a way that is easy to understand.
To highlight system-level inefficiencies, especially payer-side delays.
To explore how workflow design and UX can make complex healthcare processes transparent.
To build a fully self-contained, frontend-only simulator with no dependencies.

# Key Learning (Biggest Insight):

While building this simulator, I learned that most Prior Authorization delays are not caused by poor medical necessity, but by what happens after submission — payer queues, turnaround time rules, and manual review bottlenecks.

Even well-documented, medically appropriate cases can stall indefinitely once control shifts from the provider to the payer.

# Key Learnings:

* Documentation quality matters, but it doesn’t guarantee speed.
* Once a PA is submitted, providers largely lose control of the timeline.
* Efficiency scores should reflect system friction, not just user performance.
* Visual workflows (lanes + stages) make hidden operational problems obvious.
* Gamification can be a powerful way to teach healthcare operations and policy concepts.

# What This Simulator Includes:

* Patient → Provider → Payer workflow lanes
* Medical necessity evaluation
* Prior Authorization document collection
* Payer decisions: Approval, Pend, Denial
* Appeal and Peer-to-Peer review paths
* Days elapsed & efficiency scoring
* Educational explanations at every step
* Fully restartable scenarios
* Single HTML file, no frameworks, no APIs

# Why This Matters

Prior Authorization is one of the biggest contributors to care delays and provider burnout in healthcare.
By simulating it end-to-end, this project aims to make those pain points visible, measurable, and discussable.

# SCREENSHOTE:

[Prior Authorization Simulator](prior_authorization_simulator.png)

# HTML File:

[Prior Authorization Simulator](prior_authorization_simulator.html)
