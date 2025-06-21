---
layout: page
title: "Project 2｜Intelligent Quantitative Strategy Generation Platform: Causality-Aware RLHF with Backtest-Integrated Feedback Loop"
permalink: /projects/project2/
importance: 2
category: work
---

# Project 2｜Intelligent Quantitative Strategy Generation Platform

### Causality-Aware RLHF with Backtest-Integrated Feedback Loop

#### Project Overview

To address three critical challenges in quantitative strategy development—unverifiable generation, lack of causal structure, and high deployment costs—this project builds a closed-loop intelligent strategy generation platform integrating strategy generation, causal inference, RLHF optimization, and backtest feedback. By combining multi-task knowledge distillation, structured reward design, and reinforcement learning-based re-training, it achieves a unified system characterized by causality consistency, evaluation-verified generation, and deployability. The system is applicable to both academic research and enterprise use cases.

#### Key Contributions and Implementation

- Led the construction of a high-quality multi-source dataset (800K+ texts) from hedge fund strategy documents, causal event databases, and Tushare behavioral data. Designed three types of structured corpora: 12,000 strategy abstracts, 11,000 indicator chains, and 9,000 causal graphs.

- Addressed key challenges such as noisy text, structural variance in indicators, and nested causal chains. Developed a spaCy + RegEx-based tree extraction algorithm and an in-house graph alignment mechanism for entity fusion. Multi-round human annotation increased structural consistency from 71.2% to 94.6%.

- Built a multi-task distillation framework using LLaMA-2-7B as the teacher model. Employed soft-label training with temperature T=2.0 and structure-aware prompt templates. Applied weighted loss (0.4:0.4:0.2) across three task types to ensure generalization on causal structured tasks.

- Designed a custom RLHF reward scheme integrating: (1) Causal Coverage, (2) Contextual Coherence Score, and (3) Backtest Execution Score (Return + Stability). Integrated reward clipping and early baseline strategies to avoid reward collapse.

- Introduced a full backtest feedback loop: strategies are compiled and simulated using Backtrader, with metrics (return, Sharpe, max drawdown) injected into PPO training as an additional reward signal, enabling generation-verification-retraining cycle.

- Deployed with QLoRA (rank=8) + TensorRT INT4, achieving a 65% model size reduction. Hosted on RTX 3090 with FastAPI backend, achieving 270ms latency and 26 req/s throughput. Output formats include JSON, XML, and GraphML, supporting integration with notebooks, strategy platforms, and visualization chains.

#### Outcomes and Metrics

- BLEU improved by 14.6%, redundancy rate reduced by 21.2%, and causal path match rate reached 85.4%.

- Strategy execution success rate in simulated environments reached 78.9%, with an average human evaluation of 4.7/5.0.

- Incorporating backtest-based rewards into RLHF led to a 32% faster convergence rate and significantly improved training stability.

- Completed end-to-end closed-loop deployment from "structured summary → causal path → backtest feedback → retraining," with four types of structured output templates ready for system integration.

#### Future Work

- Ablation studies: Construct baseline groups (w/o causal graph, w/o backtest reward, generic RLHF) to quantify module contribution.

- Visualization: Use D3.js and Plotly to visualize causal paths, return curves, and generation–evaluation–backtest chains.

- Model generalization: Verified on InternLM, Mistral-7B, and Yi-6B, maintaining <2.7% deviation in generation consistency and over 90% deployment stability.

- Reinforcement learning path extension: Incorporate Q-learning/R2D2 to create a return trend modeling module. If backtest return falls below a threshold, system auto-adjusts prompt structure and triggers adaptive strategy rewriting loop, advancing toward agent-based closed-loop optimization.

#### Tech Stack

LLaMA-2-7B, QLoRA, LoRA Adapter, Soft Label Distillation, RLHF with Multi-Dimensional Reward, Backtrader, Causal Graph Engine, GraphDB, Prompt Chain, FastAPI, Docker, WandB, PyTorch Lightning, TensorRT INT4, JSON/XML/GraphML output, RTX 3090.
