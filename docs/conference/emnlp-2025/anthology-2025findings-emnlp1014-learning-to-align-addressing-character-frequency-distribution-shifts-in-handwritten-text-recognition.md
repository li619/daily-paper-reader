---
title: "Learning to Align: Addressing Character Frequency Distribution Shifts in Handwritten Text Recognition"
authors: "Panagiotis Kaliosis, John Pavlopoulos"
date: 2025
pdf: "https://aclanthology.org/2025.findings-emnlp.1014.pdf"
tags: ["query:hf"]
score: 8
source: EMNLP-2025-Findings
selection_source: long-range
publication_date: 2025
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
id: anthology-2025.findings-emnlp.1014
canonical_id: "work:46e1dc273f0abcfaccc6cd74"
research_run_id: 20261022-7dd45f1f8e74
research_mode: starter
reading_status: pending
---

## Abstract
Handwritten text recognition aims to convert visual input into machine-readable text, and it remains challenging due to the evolving and context-dependent nature of handwriting. Character sets change over time, and character frequency distributions shift across historical periods or regions, often causing models trained on broad, heterogeneous corpora to underperform on specific subsets. To tackle this, we propose a novel loss function that incorporates the Wasserstein distance between the character frequency distribution of the predicted text and a target distribution empirically derived from training data. By penalizing divergence from expected distributions, our approach enhances both accuracy and robustness under temporal and contextual intra-dataset shifts. Furthermore, we demonstrate that character distribution alignment can also improve existing models at inference time without requiring retraining by integrating it as a scoring function in a guided decoding scheme. Experimental results across multiple datasets and architectures confirm the effectiveness of our method in boosting generalization and performance. We open source our code at https://github.com/pkaliosis/fada.

## 专题评审

专题相关性评分：8/10。

直接研究手写文本识别，提出字符分布对齐损失，属专题核心。

<!-- research-reading-pending -->
中文总结与全文内容待生成；当前仅提供原始论文元数据与摘要。
<!-- /research-reading-pending -->
