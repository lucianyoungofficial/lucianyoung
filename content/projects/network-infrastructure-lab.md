---
title: "Network Infrastructure Lab"
date: 2026-07-20
weight: 1
summary: "A self-hosted networking platform focused on Linux, networking, deployment and troubleshooting."
draft: true
---

## Overview

A personal networking infrastructure project built to explore Linux server administration, secure remote access, cloud deployment, and network troubleshooting.

Through continuous testing, troubleshooting, and optimization, the project evolved into a stable networking solution.

## Background

I started this project because my previous VPN services often suffered from poor stability and inconsistent performance. Building my own server provided greater control over reliability and security while allowing me to understand how the underlying infrastructure works.

At the same time, I wanted to strengthen my networking knowledge in preparation for the National Computer Rank Examination (Level 3). Instead of learning only from textbooks, I chose to build and troubleshoot a real system from scratch.

## Goals

- Build a reliable, low-latency, and high-performance remote access solution.
- Develop a deeper understanding of Linux server administration and computer networking.

## Implementation

The server is hosted on **Tencent Cloud**, using a **TCP-based proxy** to tunnel traffic. In my recorded tests, TCP throughput ranged from **15 Mbps to 180 Mbps**.

I also experimented with UDP-based protocols — **WireGuard** and **Hysteria2** — and observed **1–15 Mbps**. UDP throttling on the network path is one possible explanation, but the cause has not been isolated. These results led me to use TCP for this deployment.

## Current Status

At the time of writing, the node was running, with a lowest recorded latency of **59 ms**. The test endpoints, tools, sample sizes, and network conditions were not documented here, so these figures are observations rather than a reproducible benchmark.

Bandwidth still fluctuates with network conditions, sometimes high, sometimes not. It's not perfect yet, but it's mine. I'll keep tuning and gradually make full use of the server.

## Next Steps

- Record test conditions and repeated measurements before drawing stronger performance conclusions.
- Explore additional self-hosted services, such as NAS, as future work.
