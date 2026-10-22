---
title: "MetaWriter: Personalized Handwritten Text Recognition Using Meta-Learned Prompt Tuning"
authors: "Gu, Wenhao, Gu, Li, Suen, Chingyee Yee, Wang, Yang"
date: 2025
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gu_MetaWriter_Personalized_Handwritten_Text_Recognition_Using_Meta-Learned_Prompt_Tuning_CVPR_2025_paper.pdf"
tags: ["query:hf"]
score: 8
source: CVPR-2025-Accepted
selection_source: long-range
publication_date: 2025
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
id: cvpr-2025-gu-metawriter-personalized-handwritten-text-recognition-using-meta-learned-prompt-tuning-cvpr-2025-paper
canonical_id: "work:3ddb5a2c764ac2f5c0bbb7c7"
research_run_id: 20261022-7dd45f1f8e74
research_mode: starter
reading_status: pending
---

## Abstract
Recent advancements in handwritten text recognition (HTR) have enabled the effective conversion of handwritten text to digital formats. However, achieving robust recognition across diverse writing styles remains challenging. Traditional HTR methods lack writer-specific personalization at test time due to limitations in model architecture and training strategies. Existing attempts to bridge this gap, through gradient-based meta-learning, still require labeled examples and suffer from parameter-inefficient fine-tuning, leading to substantial computational and memory overhead. To overcome these challenges, we propose an efficient framework that formulates personalization as prompt tuning, incorporating an auxiliary image reconstruction task with a self-supervised loss to guide prompt adaptation with unlabeled test-time examples. To ensure self-supervised loss effectively minimizes text recognition error, we leverage meta-learning to learn the optimal initialization of the prompts. As a result, our method allows the model to efficiently capture unique writing styles by updating less than 1% of its parameters and eliminating the need for time-intensive annotation processes. We validate our approach on the RIMES and IAM Handwriting Database benchmarks, where it consistently outperforms previous state-of-the-art methods while using 20x fewer parameters. We believe this represents a significant advancement in personalized handwritten text recognition, paving the way for more reliable and practical deployment in resource-constrained scenarios.

## 专题评审

专题相关性评分：8/10。

直接研究手写文本识别的个性化提示微调，属专题核心。

<!-- research-reading-pending -->
中文总结与全文内容待生成；当前仅提供原始论文元数据与摘要。
<!-- /research-reading-pending -->
