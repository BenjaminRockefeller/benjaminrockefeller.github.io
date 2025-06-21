---
layout: page
title: Projects
permalink: /projects/
description: A showcase of my AI, NLP, and Quant Finance projects.
nav: true
nav_order: 2
---
## Quick Navigation

- [Project 1 – Financial Research Report Generation Platform](#project-1--financial-research-report-generation-platform)
- [Project 2 – Intelligent Quantitative Strategy Platform](#project-2--intelligent-quantitative-strategy-platform)
- [Project 3 – AI-Driven Financial Fraud Detection System](#project-3--ai-driven-financial-fraud-detection-system)
- [Project 4 – Enterprise LLM Deployment Optimization](#project-4--enterprise-llm-deployment-optimization)
- [Project 5 – High-Performance Multi-Model Inference Platform](#project-5--high-performance-multi-model-inference-platform)
- [Project 6 – Multimodal Content Generation Platform](#project-6--multimodal-content-generation-platform)
---
## Project 1 | Financial Research Report Generation Platform: A RAG-Enhanced, Locally Deployed Contextual Reasoning System for US Stock Analysis

### Overview

This project addresses major pain points in financial research report generation, including information redundancy, hallucination-prone outputs, poor content structure, and low automation efficiency. We developed a modular, controllable, and citation-grounded RAG (Retrieval-Augmented Generation) system tailored for financial applications. The system integrates multi-source data collection, a three-stage retrieval pipeline, dynamic prompt injection, multi-model fine-tuning, and full-stack private deployment. Emphasis is placed on reusability, traceability, and deployability.

### Motivation

Based on interviews with 30+ hedge funds and equity research firms, we identified three core issues:

1. General-purpose LLMs exhibit high hallucination rates due to lack of authoritative sources.
2. API-based solutions incur high costs and lack permission control, making them unsuitable for private environments.
3. Reports suffer from fragmented structure and repetitive writing—highlighting the need for modular generation tools.

The system is designed around four tightly coupled objectives: **RAG Enhancement + On-Prem Deployment + Modular Reuse + Trustworthy Generation**

### System Architecture

```
Data Ingestion → Multi-Stage Retrieval (Recall → Dense → Re-rank) → Prompt Injection → LLM Generation → Hallucination Filtering → Private Deployment
```

### Data Acquisition & Structuring

- Built custom crawlers for bilingual financial sources (Yahoo Finance, CNBC, EDGAR, WallstreetCN), collecting 386,000+ documents.
- Parsed earnings reports (PDF) using Unstructured, with manual verification and table reconstruction.
- Final dataset includes 243,000 structured paragraph segments after normalization.

### Three-Stage Retrieval System

- **Recall Phase**: BM25, Recall@10 = 82.3%
- **Dense Search**: FAISS-HNSW (384-dim)
- **Re-ranking**: BERT cross-encoder, Top-1 accuracy from 60.2% → 80.1%
- Prompt assembly: length trimming, topic clustering, positional encoding

### Prompt Injection & LLM Optimization

- Prompt template: task description + retrieved snippets + user instruction
- Models: ChatGLM2-6B, InternLM2, Yi-6B
- Control tokens: summarization paths, reduce drift/redundancy

### Hallucination Evaluation Experiments

- **TruthfulQA-Fin**: 30 fact-checking questions
- **MMLU-Finance Derivation**: 20 paragraph-summary pairs
- Evaluation: 5 human annotators + GPT-4

| Model Type           | Hallucination Rate | Consistency Score | Structure Completeness |
| -------------------- | ------------------ | ----------------- | ---------------------- |
| Baseline ChatGLM2-6B | 27.5%              | 3.6 / 5.0         | 71.4%                  |
| RAG-Enhanced System  | 12.8%              | 4.7 / 5.0         | 91.3%                  |

### Case Example

**Q**: What was the Fed’s rate hike in March 2023?

- **ChatGLM2**: "50bp" (incorrect)
- **RAG System**: "25bp" with EDGAR citation (correct)

### Private Deployment & Inference Optimization

- **Stack**: FastAPI + Docker + Redis
- **Hardware**: RTX A100, 52 QPS @ <300ms
- **Costs**: Training = $65, Deployment Hardware = ~$8,000
- **Interface**: OpenAI-style Chat API

### Key Performance Metrics

| Metric                  | Value     | Notes                      |
| ----------------------- | --------- | -------------------------- |
| Recall@10 (BM25)        | 82.3%     | Initial retrieval accuracy |
| Top-1 Re-rank Accuracy  | 80.1%     | Cross-encoder boost        |
| BLEU Improvement        | +25.2%    | Over baseline              |
| Hallucination Reduction | -14.7%    | TruthfulQA verified        |
| Consistency Score       | 4.7 / 5.0 | Human+GPT-4                |
| Generation Latency      | <300ms    | Benchmark                  |

### Real-World Validation

Three U.S. analysts gave positive feedback:

- Better terminology and summarization
- Improved structure and traceability
- Future Suggestions: chart parsing, event-chain reasoning

### Future Directions

- **Expansion**: Charts + events = "Text + Visual + Chain"
- **Research**: ACL/EMNLP Demo track
- **Business**: Piloting with financial SaaS vendors

**Tech Stack**: ChatGLM2-6B, InternLM2, Yi-6B · BM25, FAISS · BERT · Prompt + LoRA/QLoRA · TruthfulQA, MMLU · FastAPI, Docker, Redis · PyTorch Lightning · Streamlit

## Project 2 | Intelligent Quantitative Strategy Generation Platform: Causality-Aware and RLHF-Enhanced Backtesting Optimization System

### Overview

This project tackles three longstanding challenges in quantitative strategy development: lack of verifiable output, absence of causal structure, and resource-intensive deployment. We built an end-to-end system that integrates strategy generation, causal graph extraction, RLHF fine-tuning, and feedback-driven backtesting—achieving a closed-loop architecture with strong explainability and practical deployability. The platform combines multi-task knowledge distillation, a custom structured reward mechanism, and backtesting-aware reinforcement learning to deliver a highly generalizable and interpretable solution.

### Key Contributions

- Constructed a large-scale multi-source strategy dataset (800K+ samples) including hedge fund documents, causal event chains, and Tushare-based market behavior data.
  - Designed three structured corpora:
    1. 12,000 strategy abstracts
    2. 11,000 technical indicator chains
    3. 9,000 causal market responses
- Solved noisy text and indicator nesting via:
  - spaCy + regex tree extraction
  - Graph-based entity alignment for causal chain consistency (71.2% → 94.6%)
- Multi-task distillation:
  - Teacher: LLaMA‑2‑7B with Soft Label (T=2.0)
  - Task weight: 0.4 (abstracts), 0.4 (indicators), 0.2 (causal)
- Custom RLHF reward = Causal Coverage + Coherence + Backtest Return
  - Early baseline + reward clipping to stabilize training
- Feedback loop:
  - Generated strategies compiled via Backtrader → Return + Sharpe fed into PPO
- Deployment:
  - QLoRA (rank=8) + TensorRT INT4, size ↓65%
  - RTX 3090 @ 26 QPS, 270ms latency
  - Output formats: JSON / XML / GraphML

### Experimental Results

| Metric               | Value     | Notes                |
| -------------------- | --------- | -------------------- |
| BLEU Improvement     | +14.6%    | Text quality         |
| Redundancy Reduction | -21.2%    | Phrase-level         |
| Causal Match Rate    | 85.4%     | vs. ground truth     |
| Strategy Execution   | 78.9%     | Backtest pass rate   |
| Human Eval Score     | 4.7 / 5.0 | Subjective quality   |
| RLHF Convergence     | +32%      | With backtest signal |

### Future Directions

- **Ablation Study**: Isolate effect of causal, RLHF, backtest signals
- **Visualization**: D3.js + Plotly for generation-to-return traceability
- **Transferability**: Reproduced on InternLM, Mistral-7B, Yi-6B (<2.7% deviation)
- **RL Agent Rewrite**: Add Q-learning module to rewrite poor strategies

**Tech Stack**: LLaMA‑2‑7B, InternLM, Yi-6B · QLoRA, Soft Label · RLHF · Backtrader · GraphDB · FastAPI, Docker, TensorRT · PyTorch Lightning · WandB · JSON/XML/GraphML

...

## Project 3 | Multi-Agent Financial Fraud Detection System: Robust Risk Control via LangGraph, GAT, RLHF, and Prompt Injection Defense

### Overview

To address key limitations in financial risk control—such as delayed fraud detection, high false positive rates, pipeline discontinuity, and vulnerability to adversarial prompts—we developed a multi-agent fraud detection system that integrates Graph Attention Networks (GAT), agent-based task routing, RLHF reward alignment, and prompt injection defense. The platform handles both structured behavior modeling and unstructured intent classification, covering the full decision-making flow from transaction analysis to compliance auditing.

### Key Contributions

- **Multi-Agent Coordination**:
  - Designed a reactive agent chain using LangGraph: `Risk Detector → Rule Evaluator → Human Review Agent`
  - Implemented dynamic routing and shared state via `AgentNode` + `AgentState`, resolving workflow discontinuities
- **Graph-Based Behavior Modeling**:
  - Built a heterogeneous transaction graph (n = 42,000) with GAT
  - Node features: transaction frequency, device fingerprint
  - Edge features: amount spikes, address connectivity
  - Achieved F1 = 0.918 (val), F1 = 0.911 (test), outperforming GraphSAGE & LightGBM
- **Unstructured Intent Recognition**:
  - Fine-tuned ChatGLM3‑6B on 11K-sample corpus, 14 intent types
  - Applied QLoRA + GPT-3.5 reward in RLHF
  - Output consistency improved by +11.3%
- **Prompt Injection Defense**:
  - Collected 36 attack patterns (e.g., role reversal, DoS prompts)
  - Integrated Detoxify for toxicity detection
  - Reward formula: `0.5 × Task Success + 0.3 × Consistency + 0.2 × Safety Score`
  - Results:
    - Jailbreak success ↓ from 31.2% → 9.6%
    - Toxicity score ↓ from 0.23 → 0.07
    - Bias trigger rate ↓ 42.5%
- **Ablation Study**:
  - Compared: (1) No defense, (2) Defense-only, (3) Full RLHF+Defense
  - Results: F1 +3.4%, Attack success ↓19.8%, Convergence speed +24%
- **Hybrid Rule System**:
  - Combined GAT results with 17 handcrafted business rules
  - Enhanced real-world applicability & interpretability
- **Traceability & Logging**:
  - Used LangSmith to log agent paths, model calls for audit purposes
- **Deployment**:
  - Stack: FastAPI + Redis + Docker Compose
  - Monitoring: Prometheus + Grafana
  - Inference latency: <450ms, supports 50 QPS per node

### Commercial Readiness

System is integration-ready for loan approval and risk scoring pipelines, with extensibility for:

- Insurance underwriting
- E-commerce trust/risk modules
- Web3 transaction compliance

### Experimental Results

| Metric                  | Value  | Notes                     |
| ----------------------- | ------ | ------------------------- |
| GAT Test F1             | 0.911  | Model accuracy            |
| Output Consistency Gain | +11.3% | Post RLHF tuning          |
| Jailbreak Success ↓     | 21.6%  | Full defense enabled      |
| Toxicity Score ↓        | 69.6%  | Detoxify-based eval       |
| RL Convergence Speed    | +24%   | With safety reward module |

**Tech Stack**: ChatGLM3‑6B · QLoRA · RLHF (GPT-3.5 Reward) · LangGraph, LangChain, LangSmith · GAT (DGL, PyTorch) · Prompt Injection Eval, Detoxify · FastAPI, Redis, Docker Compose · Prometheus, Grafana · Sklearn, WandB

...

## Project 4 | Enterprise-Grade Fine-Tuning and Deployment Optimization Platform for LLMs (Sentiment Analysis + NER Tasks)

### Overview

This project addresses the critical bottlenecks in enterprise-level large language model (LLM) deployment: high fine-tuning cost, inefficient inference, and poor task generalization. We developed a lightweight multi-task fine-tuning platform tailored for sentiment classification and named entity recognition (NER). Leveraging QLoRA parameter compression, RLHF alignment, and inference optimization, the system enables stable training, scalable deployment, and real-world applicability across government, finance, and e-commerce domains.

### Key Contributions

- **QLoRA Fine-Tuning Architecture**:
  - Frozen ChatGLM2‑6B backbone, trained only LoRA adapters (rank=8)
  - Reduced GPU memory from 24 GB → 7.2 GB
  - Training cost ↓ ~60%
- **Multi-Task Dataset Construction**:
  - Chinese sentiment dataset (5,000 labeled samples)
  - Renmin Daily-based NER corpus (~120,000 characters)
  - Unified prompts ensured consistent generation
- **Dual-Stage RLHF Optimization**:
  - Stage 1: GPT-3.5 rated instruction-following accuracy
  - Stage 2: PPO reward = 0.5 (F1) + 0.3 (NER Recall) + 0.2 (Adherence)
  - Improved consistency by +12%, resolved non-convergence issues
- **Robust RLHF Training Pipeline**:
  - Dynamic baseline, reward clipping, exception handling
  - Ensured stable convergence across tasks
- **Low-Cost Remote Training**:
  - Ran on Magicoder.ai + Paperspace A100 GPUs (40+ hrs)
  - Total cost: $50–60
- **Distributed Training Framework**:
  - PyTorch Lightning + DDP
  - Checkpointing, failure recovery, monitoring supported
- **Optimized Inference**:
  - vLLM + TensorRT INT4
  - Latency ↓ <350ms, supports 50 QPS on-prem

### Experimental Results

| Metric            | Baseline | Fine-Tuned (QLoRA + RLHF) |
| ----------------- | -------- | ------------------------- |
| Sentiment F1      | 88.1%    | 92.3%                     |
| NER Recall        | 83.5%    | 90.2%                     |
| Inference Latency | >800ms   | <350ms                    |
| Training Cost     | —        | ↓ ~60%                    |

### Deployment

- Exported LoRA weights in OpenAI-compatible API format
- Deployed to gov/fintech/e-commerce support systems

**Tech Stack**: ChatGLM2‑6B · QLoRA, LoRA Adapter · PyTorch Lightning, DDP · Huggingface TRL, PPO · GPT-3.5 Reward · vLLM, TensorRT INT4 · FastAPI, Docker · Magicoder.ai, Paperspace · WandB

...

## Project 5 | High-Performance Multi-Model Inference Optimization Platform: Low-Latency Deployment via Tensor Parallelism and INT8 Quantization

### Overview

This project tackles core challenges in enterprise-scale LLM inference: excessive memory usage, high latency, and difficulty supporting heterogeneous endpoints. We built a high-throughput, low-latency deployment platform that integrates Tensor Parallelism, Pipeline Parallelism, and mixed-precision quantization. The system supports multi-modal tasks, private deployments, LoRA hot-swapping, and adaptive device scheduling—making it ideal for finance, government, and manufacturing environments.

### Key Contributions

- **Distributed Inference Architecture**:
  - Huggingface Transformers + DeepSpeed
  - Combined Tensor + Pipeline Parallelism
  - Integrated vLLM engine; extended context window to 128K
  - Achieved 3.7× QPS improvement, stable multi-turn dialogue
- **Mixed-Precision Quantization**:
  - Applied Quantization Aware Training (QAT)
  - INT8 + FP16 hybrid model with OpenVINO CPU acceleration
  - Reduced memory usage by 53%, latency <2.8s
- **Unified API Layer**:
  - Built with FastAPI + JSON-RPC
  - Supports dynamic prompt routing, concurrent task handling
  - Response success rate ↑ from 92.6% → 99.3%
- **Containerized Deployment**:
  - Docker Compose packaging
  - Nginx for load balancing + SSL encryption
  - Enabled secure CPU↔GPU switching under access control
- **Model Hot-Swapping**:
  - LoRA/QLoRA runtime replacement without restart
  - Average model switch time: <1.3s
- **Prompt Compliance Dataset**:
  - 21K samples from enterprise logs, support tickets
  - Cleaned and aligned across generation/summarization/classification/NER
- **Stability Optimization**:
  - Resolved vLLM vs. Pipeline Parallelism scheduling conflicts
  - Sustained 8-GPU parallel execution, 2.4× throughput gain

### Deployment Results

| Metric            | Value  | Notes                  |
| ----------------- | ------ | ---------------------- |
| QPS Improvement   | 3.7×   | Over baseline          |
| Latency           | <2.8s  | Hybrid INT8/FP16 model |
| Memory Usage      | ↓ 53%  | Post-QAT               |
| Response Success  | ↑ 6.7% | To 99.3%               |
| Model Switch Time | <1.3s  | Hot-swap mode          |

### Use Cases

- Deployed in:
  - Quant research engines
  - Government QA systems
  - Internal CRM support tools

**Tech Stack**: ChatGLM2‑6B · DeepSpeed, vLLM · Tensor/Pipeline Parallelism · INT8 QAT, OpenVINO · FastAPI, JSON-RPC · LoRA/QLoRA · Docker Compose, Nginx, SSL · WandB

...

## Project 6 | ChatPPT: Multi-Modal Content Generation and Publishing Platform with Causal Reasoning and Controllable Generation (Video Scripts + Image-Text + Voice Commands)

### Overview

This project presents ChatPPT, a multi-modal content automation system designed for content creators—such as short video teams, MCNs, and e-commerce operators—to streamline script writing, image-text matching, and voice-controlled publishing. The platform supports natural language input and real-time voice interaction, automatically generating structured image-text assets for platforms like TikTok, Xiaohongshu, and Instagram. It significantly improves creative efficiency and expression quality by closing the loop between content generation and user feedback.

### Key Contributions

- **End-to-End Creative Chain**:
  - Full workflow: Text Input → Image-Text Generation → Voice Editing → Web Preview
  - Enables structured content creation from scratch with real-time interaction
- **Multi-Modal Dataset Construction**:
  - Text: 20K scripts (GPT-generated + template mining across marketing/education/lifestyle)
  - Image: 25K open-source images (Pexels/Pixabay), 15K aligned pairs (via BERTScore + manual review)
  - Voice: 8K+ voice commands for editing ("add slide", "replace image", etc.)
- **Text Generation Module**:
  - ChatGLM2.5 + structured prompt: Theme → Plot Outline → Detailed Content
  - Supports style conditioning and persona control
- **Image Matching Module**:
  - CLIP + BM25 hybrid retrieval
  - Top-1 accuracy = 89.3%, high content-image alignment
- **Voice Control Module**:
  - Whisper transcription + 12-class intent classifier
  - Speech-driven editing, accuracy = 93.5%
- **System Architecture**:
  - Backend: FastAPI + Redis async queue
  - Frontend: Streamlit for preview/editing
  - Deployed as web app for real-time collaboration

### Performance & Cost

- Avg. time to generate 5-slide content unit: <90 sec (vs. ~3 hrs manual)
- Deployed on Hugging Face Spaces (free tier, A10 GPU)
- Marginal cost: < $0.005 per unit

### Future Roadmap (v2.0)

- **Causal Graphs for Optimization**:
  - Model user clicks → conversion outcomes → feedback to generation
- **Multilingual & Style Transfer**:
  - Extend to CN/EN/JP/KR, support regional aesthetics
- **Agent Integration & A/B Testing**:
  - Personalized generation based on user feedback loops
- **Cross-Platform Extensions**:
  - Chrome extension + WeChat mini-program for multi-device delivery

**Tech Stack**: ChatGLM2.5 · CLIP, Whisper · BM25, BERTScore · FastAPI, Redis, Streamlit · PPTX Generator · MongoDB, Docker · Hugging Face Spaces · LangChain · Pexels API

