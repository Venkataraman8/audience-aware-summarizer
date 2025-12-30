# From Experts to Novices: Controllable Abstractive Summarization via Audience-Aware Modeling

This repository contains the code, experiments, and analysis for the **CSCI 544 (Applied Natural Language Processing) – Fall 2025** project at the University of Southern California.

The project proposes a **two-stage, audience-aware abstractive summarization pipeline** that jointly addresses **factual consistency** and **readability control**, producing both expert-level and simplified summaries from the same source document.

---

## 📌 Project Overview

Modern abstractive summarization systems often suffer from two key limitations:

1. **Factual inconsistency** (hallucinations or unsupported claims)
2. **Lack of audience adaptation** (same summary for experts and novices)

This project introduces a **Simplify-then-Summarize** framework that decouples linguistic simplification from content selection, enabling:

* Faithful summaries for expert readers
* Accessible summaries for novice or non-native readers

The pipeline is built using **T5-based Transformer models** and evaluated with **rigorous factuality and readability metrics**.

---

## 🧠 Methodology

### Two-Stage Pipeline

1. **Text Simplification (Optional Path)**

   * Model: `T5-small`
   * Dataset: **WikiLarge**
   * Operates sentence-by-sentence
   * Reduces syntactic and lexical complexity while preserving meaning

2. **Abstractive Summarization**

   * Model: `T5-base`
   * Dataset: **CNN/DailyMail**
   * Generates concise, information-dense summaries

### Output Modes

* **Normal Summary** (Expert-oriented):

  ```text
  S_normal = Summarizer(T_original)
  ```

* **Simplified Summary** (Novice-oriented):

  ```text
  S_simple = Summarizer(Simplifier(T_original))
  ```

This modular design ensures that **readability gains do not compromise factual accuracy**.

---

## 📊 Evaluation Metrics

The system is evaluated along **three major dimensions**:

### 1. Content Quality

* **ROUGE-1 / ROUGE-2 / ROUGE-L / ROUGE-Lsum**
* **BERTScore (F1)**
* **BLEU**

### 2. Factual Consistency (Faithfulness)

* **FactCC** (NLI-based factuality verification)
* **QAGS** (Question Answering-based consistency check)

### 3. Audience Alignment

* **Flesch–Kincaid Grade Level (FKGL)**
* **SARI** (for simplification quality)

---

## 📈 Key Results

| Metric | Normal Summary | Simplified Summary |
| ------ | -------------- | ------------------ |
| FKGL   | 8–10           | **6–7**            |
| FactCC | 0.91–0.99      | 0.91–0.99          |
| QAGS   | 0.60–0.62      | **0.62–0.64**      |

**Key Insight:**

> Simplification does *not* reduce factual accuracy — it can actually improve faithfulness by removing linguistic noise.

---

## 🚀 How to Run

### 1. Environment Setup

```bash
pip install -r requirements.txt
```

### 2. Run Notebooks (Recommended Order)

1. `notebooks/simplification.ipynb`
2. `notebooks/summarization.ipynb`
3. `notebooks/faithfulness.ipynb`

Each notebook is self-contained and documented.
---

## 🔮 Future Work

* Continuous audience control (beyond binary expert/novice)
* Adapter-based or prefix-tuning approaches for style control
* Human evaluation with real target users
* Extension to domain-specific corpora (healthcare, education)

---

If you use or build upon this work, please cite the accompanying project report.
