# AI Research Explorations 🔬
### OCR, Computer Vision & Multimodal AI Architecture Analysis

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11+-blue?style=for-the-badge&logo=python)
![Research](https://img.shields.io/badge/Type-Research_Analysis-purple?style=for-the-badge)
![OCR](https://img.shields.io/badge/Focus-OCR_&_Vision-orange?style=for-the-badge)
![Published](https://img.shields.io/badge/Published-Computer_R&D_Vol24-green?style=for-the-badge)

**Structured analysis of state-of-the-art open-source AI systems — architecture deep dives, controlled experiments, and production feasibility assessment**

[EasyOCR](#1-easyocr) · [DeepSeek-OCR](#2-deepseek-ocr) · [JamMa](#3-jamma) · [Publication](#publication) · [Methodology](#methodology)

</div>

---

## What is This?

A research and engineering analysis repository studying three state-of-the-art open-source AI systems. For each system, I:

1. Read and understood the full source code
2. Analyzed the architecture and training pipeline
3. Conducted controlled experiments with standardized inputs
4. Evaluated real-world performance and limitations
5. Assessed production deployment feasibility

This demonstrates the ability to **move from "using AI models" to "understanding and evaluating AI systems"** — a critical skill for AI engineering.

---

## Systems Analyzed

### 1. EasyOCR
**Focus:** Traditional deep learning OCR pipeline

**Architecture:**
```
Input Image
     │
     ▼
┌─────────────────────────────────────────────────────────┐
│                   STAGE 1: CRAFT                        │
│              Text Region Detection                      │
│                                                         │
│  Conv Layers → Feature Maps → Character Attention Maps  │
│                                                         │
│  Output: Bounding boxes around text regions            │
└──────────────────────┬──────────────────────────────────┘
                       │ Cropped text regions
                       ▼
┌─────────────────────────────────────────────────────────┐
│                   STAGE 2: CRNN                         │
│              Text Recognition                           │
│                                                         │
│  ┌─────────┐   ┌──────────┐   ┌──────────────────────┐ │
│  │   CNN   │ → │  BiLSTM  │ → │   CTC Decoder        │ │
│  │Features │   │ Sequence │   │ → Final Text Output  │ │
│  └─────────┘   └──────────┘   └──────────────────────┘ │
│                                                         │
│  Convolutional → Recurrent → Connectionist Temporal    │
│  Feature Ext.    Processing   Classification           │
└─────────────────────────────────────────────────────────┘
                       │
                       ▼
               Extracted Text
```

**Key Findings:**

| Scenario | Performance |
|----------|------------|
| Printed text, high contrast | ✅ Excellent |
| Standard document layouts | ✅ Good |
| Multiple languages | ✅ 80+ languages supported |
| Handwritten text | ⚠️ Limited |
| Complex layouts (tables, multi-column) | ⚠️ Struggles |
| Very small text | ⚠️ Reduced accuracy |
| GPU deployment | ✅ 3-5x speedup |
| CPU-only deployment | ✅ Feasible |

**Deployment Analysis:**
- Docker-compatible — isolated environment
- CPU inference: ~2-5 seconds per image
- GPU inference: ~0.5-1 second per image
- Memory: ~800MB model weights

---

### 2. DeepSeek-OCR
**Focus:** Advanced OCR using large multimodal models (LMMs)

**Architecture:**
```
Input Document
     │
     ▼
┌─────────────────────────────────────────────────────────┐
│              Vision Encoder (ViT-based)                 │
│                                                         │
│  Image Patches → Visual Tokens → Projected Embeddings  │
└──────────────────────┬──────────────────────────────────┘
                       │ Visual embeddings
                       ▼
┌─────────────────────────────────────────────────────────┐
│         Cross-Attention: Vision + Language              │
│                                                         │
│  Visual Tokens ──┐                                      │
│                  ├──► Cross-Attention ──► Language LM  │
│  Text Prompt  ───┘                                      │
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
           Structured Document Output
     (text, tables, layout preserved)
```

**Comparison vs EasyOCR:**

| Capability | EasyOCR (CRAFT+CRNN) | DeepSeek-OCR (LMM) |
|-----------|---------------------|-------------------|
| Simple printed text | ✅ Excellent | ✅ Excellent |
| Complex layouts | ⚠️ Struggles | ✅ Better |
| Tables | ❌ Limited | ✅ Good |
| Handwriting | ⚠️ Limited | ⚠️ Improved |
| CPU deployment | ✅ Feasible | ❌ Impractical |
| GPU requirement | Optional | Required |
| Inference speed | Fast | Slower |
| Novel document types | Limited generalization | Better generalization |

---

### 3. JamMa
**Focus:** Multimodal LLM Architecture Exploration

**Architecture:**
```
┌──────────────┐    ┌──────────────────────────────────┐
│    Image     │    │         Language Model            │
│   Input      │    │                                  │
│              │    │  Token Embeddings                │
│  ┌─────────┐ │    │         │                        │
│  │ Vision  │ │    │         ▼                        │
│  │ Encoder │ │    │  ┌─────────────────────────┐    │
│  │ (ViT)   │ │    │  │  Cross-Attention Layer  │    │
│  └────┬────┘ │    │  │                         │    │
│       │      │    │  │  Visual ──► Language    │    │
│  Visual      │    │  │  Tokens    Tokens       │    │
│  Tokens ─────┼────┼──►         ↓               │    │
│              │    │  └─────────────────────────┘    │
└──────────────┘    │         │                        │
                    │         ▼                        │
                    │  Transformer Layers              │
                    │         │                        │
                    │         ▼                        │
                    │  Generated Text Output           │
                    └──────────────────────────────────┘
```

**Research Focus Areas:**
- Vision + language integration via cross-attention mechanisms
- Prompt engineering for multimodal inputs
- Generative output evaluation methodology
- Reasoning behavior analysis across modalities
- Model generalization to out-of-distribution inputs

---

## Research Methodology

```
For Each Model:

Step 1: Source Code Study
  ├── Read full repository
  ├── Understand module dependencies
  └── Map data flow through codebase

Step 2: Architecture Analysis
  ├── Identify key components
  ├── Understand training approach
  └── Document design decisions

Step 3: Controlled Experiments
  ├── Standardized test inputs
  ├── Consistent evaluation conditions
  └── Multiple runs for reliability

Step 4: Performance Evaluation
  ├── Accuracy on standard benchmarks
  ├── Failure mode identification
  └── Edge case behavior

Step 5: Deployment Assessment
  ├── Hardware requirements
  ├── Inference speed
  ├── Memory footprint
  └── Production feasibility

Step 6: Documentation
  └── Findings in /notes/*.md
```

---

## Repository Structure

```
ai-research-explorations/
├── sources/
│   ├── easyocr/           # EasyOCR source analysis
│   ├── deepseek_ocr/      # DeepSeek-OCR analysis
│   └── jamma/             # JamMa architecture analysis
├── notes/
│   ├── easyocr.md         # Detailed EasyOCR findings
│   ├── deepseek_ocr.md    # DeepSeek analysis notes
│   └── jamma.md           # JamMa architecture notes
└── README.md
```

---

## Key Themes Explored

| Theme | Findings |
|-------|---------|
| **OCR Pipeline Design** | Two-stage (detect+recognize) vs end-to-end VLM approaches |
| **Text Detection vs Recognition** | CRAFT excels at detection; CRNN handles recognition |
| **Multimodal LLM Reasoning** | Cross-attention enables vision-language integration |
| **Layout Understanding** | LMMs significantly outperform traditional OCR on complex layouts |
| **Model Generalization** | LMMs generalize better; traditional models need domain data |
| **Inference Constraints** | Traditional OCR is CPU-feasible; LMMs require GPU |
| **Deployment Trade-offs** | Speed vs accuracy vs hardware cost |

---

## Publication

This research contributed to a peer-reviewed publication:

> **"Enhancing Text Extraction: The Evolution and Future Potential of EasyOCR"**
> *Computer Research and Development, Vol. 24, Issue 6, 2024*
> Author: Yeshwanth Akula

The controlled experiments and architecture analysis from this repository provided the empirical foundation for the paper's conclusions about OCR system design trade-offs and future directions.

---

## Future Research Directions

- [ ] LayoutLM and document transformer architectures
- [ ] Multimodal LLM fine-tuning for domain-specific OCR
- [ ] OCR + RAG integration pipeline (extract → embed → retrieve)
- [ ] Document intelligence systems for enterprise use cases
- [ ] Benchmark comparison study across all three systems
- [ ] Distillation: Can a smaller model match LMM OCR accuracy?

---

## Attribution

This repository analyzes open-source models. All source code remains attributed to original authors:

| Model | Repository | License |
|-------|-----------|---------|
| EasyOCR | [JaidedAI/EasyOCR](https://github.com/JaidedAI/EasyOCR) | Apache 2.0 |
| DeepSeek-OCR | [deepseek-ai/DeepSeek-OCR](https://github.com/deepseek-ai/DeepSeek-OCR) | As specified upstream |
| JamMa | [leoluxxx/JamMa](https://github.com/leoluxxx/JamMa) | MIT |

---

## Author

**Yeshwanth Akula**
M.S. Computer Science — Saint Louis University (May 2026)
Focus: AI Engineering, Computer Vision, LLM Systems

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/yeshwanth-akula-0339a925b)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/Yesh-is-here2)
