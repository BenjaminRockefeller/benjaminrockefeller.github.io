---
layout: page
title: "Project 5｜High-Performance Multi-Model Inference Optimization Platform"
description: "Integrating Tensor Parallelism and INT8 Quantization for Low-Latency Deployment"
importance: 5
category: work
---

# Project 5｜High-Performance Multi-Model Inference Optimization Platform

### Integrating Tensor Parallelism and INT8 Quantization for Low-Latency Deployment

---

## Project Overview

To address enterprise challenges such as high inference latency, excessive GPU memory consumption, and low compatibility with heterogeneous hardware, this project developed a distributed high-performance inference platform. The system combines tensor and pipeline parallelism with mixed-precision quantization, supports multi-modal tasks and dynamic model switching, and is optimized for latency-sensitive use cases in finance, public services, and manufacturing.

---

## Project Contributions

- Designed a distributed inference framework based on Huggingface Transformers and DeepSpeed, enabling combined tensor and pipeline parallel execution.
  - Extended context window up to 128K tokens
  - Integrated vLLM engine for fast multi-turn dialogue support
  - Improved throughput (QPS) by 3.7× under load

- Developed hybrid INT8 + FP16 quantization strategy:
  - Applied Quantization-Aware Training (QAT) to ChatGLM2-6B
  - Deployed using OpenVINO for CPU acceleration
  - Reduced memory usage by ~53%
  - Achieved average response latency < 2.8 seconds

- Created a unified inference interface using FastAPI + JSON-RPC:
  - Supported prompt batching and task-type routing
  - Increased success rate from 92.6% to 99.3%

- Built containerized deployment infrastructure:
  - Used Docker Compose with Nginx for load balancing and SSL security
  - Enabled hybrid CPU/GPU scheduling and intranet access control

- Enabled hot-swappable model loading:
  - Compatible with LoRA and QLoRA adapters
  - Dynamic switching time < 1.3 seconds without system restart

- Constructed a 21,000-sample multi-task inference dataset:
  - Aggregated from real enterprise tickets and internal queries
  - Applied regex-based cleaning and instruction formatting
  - Tasks included generation, classification, summarization, and NER

- Optimized GPU allocation:
  - Tuned tensor_parallel_size and async_batching settings
  - Resolved contention issues between vLLM and pipeline schedulers
  - Increased GPU utilization and task throughput by ~2.4×

- Conducted comprehensive benchmarking:
  - Outperformed baseline systems by >30% in throughput, API stability, and model switch latency
  - Validated deployment in quantitative research platforms, government knowledge bases, and CRM systems

---

## Tech Stack

ChatGLM2‑6B, DeepSpeed, vLLM, Tensor Parallelism, Pipeline Parallelism, INT8 Quantization, QAT, OpenVINO, FastAPI, JSON-RPC, LoRA/QLoRA, Docker Compose, Nginx, SSL, Token Auth, Weights & Biases
