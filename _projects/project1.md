---
layout: page
title: "Project 1｜Financial Research Report Generation Platform: RAG-Enhanced Contextual Reasoning with On-Premise Deployment (Tailored for U.S. Equity Market)"
permalink: /projects/project1/
importance: 1
category: work
---

<style>
  h1.project-title {
    font-size: 32px;
    font-weight: bold;
    color: #1a1a1a;
  }
  h2.project-subtitle {
    font-size: 24px;
    color: #333333;
    margin-bottom: 0.5em;
  }
  p, li {
    font-size: 17px;
    line-height: 1.7;
    color: #2c2c2c;
  }
  .highlight {
    font-weight: bold;
    color: #0051ba;
  }
</style>

# <span class="project-title">📚 Project 1｜Financial Research Report Generation Platform</span>

## <span class="project-subtitle">RAG-Enhanced Contextual Reasoning with On-Premise Deployment (Tailored for U.S. Equity Market)</span>

---

## 🔍 Project Overview

This project addresses major challenges in financial research report generation, including redundant content, hallucination-prone outputs, unstructured formatting, and low automation levels. We built a RAG-enhanced system capable of controllable generation, modular maintenance, and high-fidelity citation, with full support for on-premise deployment. The pipeline integrates financial corpus collection, multi-stage semantic retrieval, prompt injection, multi-model tuning, and optimized inference.

---

## 🧭 Motivation & Problem Statement

Based on interviews with over 30 private equity and research institutions, we identified the following pain points:

- High hallucination rates due to lack of authoritative sources in general-purpose LLMs.
- Expensive and uncontrollable external APIs, limiting suitability for private deployments.
- Repetitive manual writing and fragmented output structure, requiring modularized automation.

<span class="highlight">Positioning</span>: End-to-end solution with 4 goals:  
<span class="highlight">RAG-enhancement · Local deployment · Module reusability · Faithful generation</span>

---

## 🛠️ System Architecture

**Pipeline**:  
Data Collection → BM25 → Dense Retrieval → Cross-Encoder → Prompt Injection → LLM Inference → Hallucination Filtering → On-Prem Deployment

- Collected <span class="highlight">386,000 bilingual financial documents</span>.
- BM25 recall@10: <span class="highlight">82.3%</span>, reranked Top-1: <span class="highlight">80.1%</span> via BERT Cross-Encoder.
- Models: ChatGLM2-6B, InternLM2, Yi-6B.

---

## 📊 Evaluation Results

| Model                | Hallucination Rate | Consistency Score | Structural Integrity |
|---------------------|--------------------|-------------------|----------------------|
| ChatGLM2-6B         | 27.5%              | 3.6 / 5.0         | 71.4%                |
| RAG-Enhanced System | <span class="highlight">12.8%</span>              | <span class="highlight">4.7 / 5.0</span>         | <span class="highlight">91.3%</span>                |

---

## 🚀 Deployment & Performance

- <span class="highlight">Latency</span> < 300ms, <span class="highlight">QPS = 52</span>
- <span class="highlight">48 GPU-hours</span>, ~$65 cost
- Hardware: <span class="highlight">RTX A100</span>

---

## 👨‍⚖️ Expert Validation

- Reviewed by U.S. equity analysts
- Reported improvements in:
  - Terminology accuracy
  - Summary coherence
  - Citation traceability

---

## 🧭 Roadmap

- Chart-to-text generation
- Event-chain reasoning
- Preparing paper for ACL Industry or EMNLP Systems Demo

---

## 🧰 Tech Stack

ChatGLM2-6B, InternLM2, Yi-6B, BM25, Faiss-HNSW, Chinese-BERT Cross-Encoder,  
TruthfulQA, MMLU-Finance, Prompt Injection, LoRA, QLoRA, FastAPI, Docker, Redis, PyTorch Lightning, WandB
