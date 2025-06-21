---
layout: page
title: "Project 6｜Multimodal Content Generation and Publishing Platform"
description: "Causality-Aware and Controllable Generation System for Short Video Scripts, Image+Text Content, and Voice-Based Editing"
importance: 6
category: work
---

# Project 6｜Multimodal Content Generation and Publishing Platform  
## Causality-Aware and Controllable Generation System for Short Video Scripts, Image+Text Content, and Voice-Based Editing

---

### Project Overview

This project introduces **ChatPPT**, a full-stack multimodal content automation platform designed for creators in short video, marketing, and e-commerce domains. The system supports content generation across multiple modalities—text, image, and voice—and enables seamless end-to-end workflows for platforms such as TikTok, Xiaohongshu, and Instagram. It significantly improves productivity by allowing structured creative output from simple natural language instructions, with real-time visual and voice-based control capabilities.

---

### Project Contributions

- Designed a full-chain multimodal content pipeline:  
  **Text Input → Image/Text Synthesis → Voice Command Execution → Web-Based Preview**  
  enabling end-to-end creative automation.

- Constructed a custom multimodal dataset:
  - **Text**: 20,000 GPT-generated scripts covering marketing, lifestyle, and educational categories.
  - **Images**: 25,000 sourced via Pexels/Pixabay APIs; 15,000 high-quality text-image pairs selected using hybrid manual and BERTScore filtering.
  - **Voice**: 8,000+ annotated real user voice commands covering key interactions (e.g., regenerate, add-slide, replace-visual).

- Implemented a modular script generator based on ChatGLM2.5:  
  **Three-stage prompt sequence** covering theme selection, plot outline, and segment-wise generation.  
  Incorporated stylistic and persona-level control switches.

- Developed an image selection engine integrating **CLIP similarity + BM25 retrieval**:  
  Achieved **Top-1 matching accuracy of 89.3%**, ensuring high semantic-visual alignment.

- Deployed voice control with Whisper + custom intent classification model:  
  Supported 12 core actions with **93.5% execution accuracy**, enabling hands-free editing and publishing.

- Engineered the backend with FastAPI + Redis (async task queue), and the front-end with Streamlit for real-time user interaction and visualization.  
  Enabled full remote access and real-time update of generated content.

- Reduced average generation time per 5-slide unit from **~3 hours (manual)** to **<90 seconds (automated)**.  
  Maintained low compute cost: **<$0.005 per content unit** on A10 GPU using Hugging Face Spaces.

---

### Future Roadmap

- Integrate **causal graph modeling** to link content structure with behavioral outcomes (e.g., clickstream → conversion).
- Expand to **cross-lingual and culturally adaptive generation**, supporting Chinese, English, Japanese, and Korean.
- Develop an **autonomous content agent** capable of adaptive generation based on user profile and real-time feedback.
- Launch **Chrome extension** and **WeChat Mini Program** for cross-platform delivery and mobile workflow.

---

### Tech Stack

ChatGLM2.5, CLIP, Whisper, BM25, BERTScore, FastAPI, Redis, Streamlit, Hugging Face Spaces, MongoDB, Docker, LangChain, PPTX Generator, Pexels API
