# AI Research Explorations

Hands-on research and technical exploration of modern OCR, computer vision,
and multimodal AI systems.

This repository documents structured analysis of state-of-the-art
open-source models with emphasis on:

- Architecture understanding
- Pipeline breakdown
- Controlled experimentation
- Performance evaluation
- Deployment trade-offs
- System-level reasoning

This is a research and engineering analysis repository — not a fork showcase.

---

# Repository Structure


ai-research-explorations/

sources/
├── easyocr/
├── jamma/
└── deepseek_ocr/

notes/
├── easyocr.md
├── jamma.md
└── deepseek_ocr.md

README.md


---

# Projects Covered

## 1. EasyOCR

**Focus:** Traditional deep learning–based OCR pipeline

- CRAFT text detection
- CRNN recognition
- Multi-language OCR support
- Practical deployment considerations
- Performance in noisy documents

Original Repository:  
https://github.com/JaidedAI/EasyOCR  

License: Apache 2.0

---

## 2. DeepSeek-OCR

**Focus:** Advanced OCR using large multimodal models

- Structured document parsing
- Complex layout understanding
- Vision-language modeling
- Enterprise document extraction use-cases

Original Repository:  
https://github.com/deepseek-ai/DeepSeek-OCR  

License: As specified by upstream repository

---

## 3. JamMa

**Focus:** Multimodal LLM architecture exploration

- Vision + language integration
- Model reasoning behavior
- Generative output evaluation
- Prompt experimentation

Original Repository:  
https://github.com/leoluxxx/JamMa  

License: MIT

---

# Research Methodology

For each model:

1. Studied documentation and source code
2. Analyzed architecture and training pipeline
3. Conducted controlled experiments
4. Evaluated performance and limitations
5. Documented findings in `/notes`
6. Assessed deployment feasibility

Approach:

Model → Architecture → Experiment → Observation → Trade-off Analysis

---

# What This Repository Demonstrates

This project demonstrates the ability to:

- Read and understand large open-source ML codebases
- Reverse-engineer model pipelines
- Analyze multimodal architectures
- Evaluate real-world limitations
- Think beyond model usage toward system design
- Document technical findings clearly

It reflects a transition from “using AI models” to
“understanding and evaluating AI systems.”

---

# Key Themes Explored

- OCR pipeline design
- Text detection vs recognition trade-offs
- Multimodal LLM reasoning
- Layout understanding challenges
- Model generalization limits
- Practical inference constraints
- Deployment considerations

---

# Future Explorations

Planned additions:

- LayoutLM and document transformers
- Multimodal LLM fine-tuning
- OCR + RAG integration pipelines
- Document intelligence systems
- Benchmark comparison studies

---

# Important Note

This repository does not claim ownership of any upstream models.
All source code remains attributed to original authors.
This project focuses strictly on research analysis and experimentation.

---
