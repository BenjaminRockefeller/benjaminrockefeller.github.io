---
layout: page
title: "Project 4｜Enterprise-Grade LLM Fine-Tuning and Deployment Optimization Platform"
description: "Focused on Sentiment Classification and Named Entity Recognition Tasks"
permalink: /projects/project4/
importance: 4
category: work
---

# Project 4｜Enterprise-Grade LLM Fine-Tuning and Deployment Optimization Platform  
### Focused on Sentiment Classification and Named Entity Recognition Tasks

## Project Overview
To address key challenges in enterprise-level large language model deployment—namely high fine-tuning cost, low inference efficiency, and poor cross-task generalization—we built a lightweight fine-tuning platform tailored for sentiment analysis and named entity recognition (NER). The system integrates QLoRA-based parameter-efficient tuning with RLHF-based instruction alignment, supports multi-task adaptation, enables stable training, and delivers fast, high-throughput inference in private environments. The solution is applicable to government, finance, and e-commerce sectors.

## Project Contributions

- **QLoRA-Based Lightweight Tuning Pipeline**  
  Designed and implemented using ChatGLM2‑6B as the backbone with LoRA Adapter (rank=8) tuning only. Reduced GPU memory usage from 24 GB to 7.2 GB, cutting training costs by ~60% and enhancing enterprise deployability.

- **Unified Multi-Task Dataset Construction**  
  Combined 5,000 sentiment classification samples and ~120,000 characters of annotated NER data from the People’s Daily corpus. Applied unified prompting and label alignment to improve cross-task consistency.

- **Two-Stage RLHF Reward Strategy**  
  Stage 1: GPT-3.5 scored instruction execution quality.  
  Stage 2: PPO optimization with weighted reward ratios (0.5: Sentiment F1, 0.3: NER Recall, 0.2: Instruction Score). Improved consistency by ~12%.

- **Complete RLHF Loop with Huggingface TRL**  
  Applied reward clipping and dynamic baselines. Solved gradient explosion and improved training stability.

- **Cost-Efficient Remote Training**  
  Used Magicoder (¥7–15/h) and Paperspace ($1.25/h) A100 instances. Trained over 40 hours with cost under $60.

- **Distributed Fault-Tolerant Framework**  
  Built with PyTorch Lightning + DDP. Enabled checkpoint recovery, error resilience, and real-time logging for extended training jobs.

- **vLLM + TensorRT INT4 Deployment**  
  Delivered sub-350ms latency and 50+ req/s throughput. Suitable for private on-premise deployment in mid-size enterprises.

- **Performance Benchmarking**  
  Compared QLoRA+RLHF vs. full-parameter baseline:  
  - Sentiment F1: 88.1% → 92.3%  
  - NER Recall: 83.5% → 90.2%

- **Private Deployment Readiness**  
  Exported LoRA weights in OpenAI-compatible format. Verified across customer service scenarios in government, financial, and e-commerce sectors.

## Tech Stack
ChatGLM2‑6B, QLoRA, LoRA Adapter, PyTorch Lightning, DistributedDataParallel, Unified Prompting, Huggingface TRL, PPO, GPT-3.5 Reward Model, vLLM, TensorRT INT4, FastAPI, Docker, WandB, Magicoder.ai, Paperspace
