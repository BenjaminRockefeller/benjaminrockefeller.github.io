---
layout: page
title: "Project 3｜Multi-Agent Financial Fraud Detection System: LangGraph + GAT + RLHF + Prompt Defense"
permalink: /projects/project3/
importance: 1
category: work
---

# Project 3｜Multi-Agent Financial Fraud Detection System

### Integrating LangGraph, Graph Attention Networks, RLHF, and Prompt Defense for High-Fidelity Risk Control

#### Project Overview

This project addresses four major challenges in enterprise-grade financial risk control systems: delayed fraud detection, high false-positive rates, fragmented decision pipelines, and susceptibility to prompt injection attacks. By building a multi-agent system integrating LangGraph task routing, GAT-based graph learning, RLHF-enhanced intent classification, and a security-oriented prompt defense module, we construct an end-to-end, interpretable, and robust fraud detection pipeline. The system has been tested in real-world loan approval and risk scoring scenarios with promising outcomes.

#### Key Contributions and Implementation

- **Multi-Agent Scheduling Architecture**: Designed a three-stage agent chain (`Risk Identification → Rule Judgment → Manual Review`) using LangGraph's `AgentNode + AgentState` mechanism. Enabled dynamic task allocation, memory routing, and upstream–downstream context preservation. Resolved fragmented workflows common in traditional financial pipelines.

- **Graph-Based Behavior Modeling**: Constructed a heterogeneous transaction graph (42,000 samples) with device fingerprints, address linkage, and transaction frequency as node/edge features. Trained a Graph Attention Network (GAT) using DGL + PyTorch, achieving F1 scores of 0.918 (validation) and 0.911 (test), outperforming GraphSAGE and LightGBM in fraud pattern detection.

- **Unstructured Intent Classification with RLHF**: Fine-tuned ChatGLM3-6B on 11,000 annotated queries across 14 financial intent categories. Integrated GPT-3.5 as the reward model within an RLHF training loop to improve semantic consistency and domain alignment. Achieved +11.3% increase in intent labeling accuracy.

- **Prompt Injection Defense Module**: Collected and labeled 36 types of prompt attacks, including role misuse, denial chaining, and indirect bypasses. Combined Detoxify-based toxicity filtering with reward-weighted reinforcement:  
  `R_total = 0.5 × Task Fidelity + 0.3 × Output Consistency + 0.2 × Safety Score`.  
  Results: reduced jailbreak success rate from 31.2% to 9.6%, toxicity score dropped from 0.23 to 0.07, and bias-trigger activation rate decreased by 42.5%.

- **Adversarial Robustness Validation**: Conducted ablation experiments to quantify the contribution of each component. Reward fusion within the prompt defense module improved F1 by +3.4%, reduced attack bypass by 19.8%, and accelerated convergence speed by 24% relative to baseline RLHF without defenses.

- **Hybrid Rules + Model Fusion Engine**: Combined learned GAT outputs with 17 domain-specific hard rules. Boosted generalization and decision controllability in real-world regulatory environments.

- **Traceable Audit Logging**: Integrated LangSmith to record agent-level decision steps and transitions. Enabled regulatory compliance and human-in-the-loop audit in high-stakes banking applications.

#### Deployment and Performance

- Deployed with FastAPI + Redis in Docker Compose architecture, supporting over 50 QPS per node with inference latency under 450 ms.

- System monitored via Prometheus and Grafana dashboards for real-time service health and alerting.

#### Future Extensions

- Scenarios: Scalable to insurance fraud detection, e-commerce risk scoring, Web3 compliance audits.

- Modular plug-ins: Designed with flexible API endpoints and event hooks for third-party decision engines.

- Defense-as-a-Service: Planning export of defense modules as stand-alone evaluators for LLM deployment pipelines.

#### Tech Stack

ChatGLM3-6B, QLoRA, RLHF, GPT-3.5 Reward Model, LangGraph, LangChain, LangSmith, GAT (DGL + PyTorch), Prompt Injection Detection, Detoxify, Hybrid Rules Engine, FastAPI, Redis, Docker Compose, Prometheus, Grafana, SMOTE, Z-Score Normalization, Isolation Forest, Sklearn, Pandas, WandB, Kaggle Dataset
