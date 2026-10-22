<div class="dpr-topic-result-actions"><button type="button" data-topic-copy="docs/starter-pack/20261022-7dd45f1f8e74/papers.md">复制论文清单</button> <a href="docs/starter-pack/20261022-7dd45f1f8e74/papers.md" download data-no-router>下载 Markdown</a> <a href="docs/starter-pack/20261022-7dd45f1f8e74/papers.json" download data-no-router>下载 JSON</a> <button type="button" data-topic-continue="20261022-7dd45f1f8e74">继续生成阅读内容</button></div>

# hf · 入门导读

> 本导读基于所列论文的标题、摘要和已有速览，不代表已阅读全部全文。近期窗口不是完整领域史；检索不保证覆盖全部相关论文。模型导读需结合原文核验。

检索窗口：arXiv &#91;2025-10-22, 2026-10-22&#41;；会议 &#91;2024-10-22, 2026-10-22&#41;（UTC，结束日不含）

## 方向概览

本导读围绕离线文本行手写识别（HTR）的入门路径、技术路线与可复现基线，基于给定检索窗口内的论文整理。核心研究问题包括：如何在有限标注与书写风格差异下稳定识别文本行；CTC、编码器-解码器、Transformer、状态空间模型与脉冲网络等序列建模范式如何取舍；跨语言、跨域与低资源场景下如何迁移与适配；以及如何用公开基准与数据集质量评估真实进展。需要说明：本导读只覆盖近期检索窗口，不是完整领域史；未提供经典参考文献、外部链接或未在摘要中出现的实验数字，因此不补写。阅读路线按方法由浅入深组织，不是时间排序。

依据：[Systematic Literature Review of Machine Learning Models and Applications for Text Recognition](/20251022-20261021/2608.26500v1)；[Performance Gap Analysis between Latin and Arabic Scripts HTR](/20251022-20261021/2606.18884v1)；[On the Generalization of Handwritten Text Recognition Models](/conference/cvpr-2025/cvpr-2025-garrido-munoz-on-the-generalization-of-handwritten-text-recognition-models-cvpr-2025-paper-on-the-generalization-of-handwritten-text-recognition-models)；[Understanding Cross-Language Transfer Improvements in Low-Resource HTR: The Role of Sequence Modeling](/20251022-20261021/2605.05900v1)；[Cross-Lingual Learning within Arabic Script for Low-Resource HTR](/20251022-20261021/2605.02089v2)；[ExpertHTR: Unified Handwritten Text Recognition with Multi-Task Learning and Sparse Mixture-of-Experts](/20251022-20261021/2609.12705v1)；[A Text Recognition Dataset from Sahidic Coptic Ancient Manuscripts](/20251022-20261021/2606.15987v2)；[A Free Lunch? Adapting PP-OCRv6 for Historical Text Recognition](/20251022-20261021/2609.20064v1)；[Efficient Domain Adaptation for Text Line Recognition via Decoupled Language Models](/20251022-20261021/2603.28028v1)；[Exploring In-Context Learning for Handwritten Text Recognition](/20251022-20261021/2609.37195v1)

## 子方向一：序列建模与识别架构（CTC、编码器-解码器、Transformer、SSM、SNN）

这一子方向回答“文本行图像如何映射为字符序列”。给定论文覆盖多条路线：CRNN加CTC是常见基线，Urdu Katib数据集论文以CNN-BGRU-CTC作为基线并比较CRNN混合模型；跨语言研究把CNN-only加CTC与CRNN对比，指出序列建模对迁移的作用。Transformer路线包括TrOCR微调、HTR-VT、以及HTR-ConvText用卷积与MobileViT结合并注入文本上下文缓解CTC弱点。DRetHTR用RetNet解码器替代softmax注意力，强调线性时间与内存。状态空间模型方面，Mamba被用于历史报纸OCR与从行到段落的消融，显示长序列效率优势但在真实手写行上落后于Transformer基线。Spike-HTR探索脉冲神经网络与CTC引导的长度压缩。ExpertHTR则用稀疏专家与多任务统一页面级训练。证据边界：各论文的CER数字仅在各自实验设置下成立，不能直接横向合并；部分论文的代码链接在摘要中出现，但本导读不转写链接。

依据：[Urdu Katib Handwritten Dataset: A Historical Document Dataset for Offline Urdu Handwritten Text Recognition with CRNN-Based Baseline Evaluation](/20251022-20261021/2606.19139v1)；[Understanding Cross-Language Transfer Improvements in Low-Resource HTR: The Role of Sequence Modeling](/20251022-20261021/2605.05900v1)；[Cross-Lingual Learning within Arabic Script for Low-Resource HTR](/20251022-20261021/2605.02089v2)；[HTR-ConvText: Leveraging Convolution and Textual Information for Handwritten Text Recognition](/20251022-20261021/2512.05021v1)；[DRetHTR: Linear-Time Decoder-Only Retentive Network for Handwritten Text Recognition](/20251022-20261021/2602.17387v1)；[A Benchmark of State-Space Models vs. Transformers and BiLSTM-based Models for Historical Newspaper OCR](/20251022-20261021/2604.00725v2)；[Scaling State-Space Models from Lines to Paragraphs: An Ablation of Mamba-based OCR](/20251022-20261021/2606.23524v1)；[Spike-HTR: Spiking Neural Transformer for Handwritten Text Recognition](/20251022-20261021/2608.01646v1)；[ExpertHTR: Unified Handwritten Text Recognition with Multi-Task Learning and Sparse Mixture-of-Experts](/20251022-20261021/2609.12705v1)；[TrOCR for Medieval HTR: A Systematic Ablation Study with Cross-Dataset Validation](/20251022-20261021/2606.24302v1)

## 子方向二：预训练、自监督与语言模型/上下文增强

这一子方向关注“在标注有限时如何获得可迁移表示”以及“如何利用文本先验”。给定论文中，Handwritten Text Recognition Lives in the High-Pixel Variance Subspace系统比较像素重建、JEPA与对比学习三类自监督方法，主张HTR的判别信号集中在高方差像素方向，像素重建类迁移最好。TrOCR for Medieval HTR研究对比归一化、数据增强与层冻结等微调选择。N-gram Injection into Transformers在解码器早期注入n-gram语言模型以应对目标语料语言分布偏移。Learning to Align用Wasserstein距离约束字符频率分布，并可作为引导解码评分。Efficient Domain Adaptation用解耦的检测加语言纠正器，以合成噪声训练纠正器实现无标注域适配。In-Context Learning与Few-shot Writer Adaptation探索不更新参数、用上下文示例适配新集合或新书写者。证据不足说明：这些方法的预训练数据规模、算力与统计显著性在摘要中多未完整给出，入门者应把它们视为路线示例而非可直接复现的配方。

依据：[Handwritten Text Recognition Lives in the High-Pixel Variance Subspace](/20251022-20261021/2609.35473v1)；[TrOCR for Medieval HTR: A Systematic Ablation Study with Cross-Dataset Validation](/20251022-20261021/2606.24302v1)；[N-gram Injection into Transformers for Dynamic Language Model Adaptation in Handwritten Text Recognition](/20251022-20261021/2603.03930v2)；[Learning to Align: Addressing Character Frequency Distribution Shifts in Handwritten Text Recognition](/conference/emnlp-2025/anthology-2025findings-emnlp1014-learning-to-align-addressing-character-frequency-distribution-shifts-in-handwritten-text-recognition)；[Efficient Domain Adaptation for Text Line Recognition via Decoupled Language Models](/20251022-20261021/2603.28028v1)；[Exploring In-Context Learning for Handwritten Text Recognition](/20251022-20261021/2609.37195v1)；[Few-shot Writer Adaptation via Multimodal In-Context Learning](/20251022-20261021/2603.29450v1)；[MetaWriter: Personalized Handwritten Text Recognition Using Meta-Learned Prompt Tuning](/conference/cvpr-2025/cvpr-2025-gu-metawriter-personalized-handwritten-text-recognition-using-meta-learned-prompt-tuning-cvpr-2025-paper-metawriter-personalized-handwritten-text-recognition-using-meta-learned-prompt-tuning)

## 子方向三：低资源、跨语言与跨域泛化

这一子方向回答“标注少、脚本不同、域偏移时怎么办”。给定论文中，Understanding Cross-Language Transfer Improvements与Cross-Lingual Learning within Arabic Script在阿拉伯字母系语言上做受控低资源实验，比较CRNN与HTR-VT，指出序列级建模对跨语言收益的作用，并报告CRNN在极端少数据时更稳。Zero-Shot Synthetic-to-Real HTR用任务类比把合成到真实的参数修正迁移到新语言。On the Generalization of HTR Models分析多模型多数据集的分布外表现，指出文本差异比视觉差异更关键。Performance Gap Analysis between Latin and Arabic Scripts用统一CRNN比较九数据集，讨论标注质量与字符频率重尾。Low Resource Languages论文提出段落级隐式行分割的ViT-Transformer-LM架构。UniLipi做多脚本统一OCR与合成数据。证据边界：低资源实验的K值、数据集划分与清洗方式差异大，跨论文比较需谨慎；部分数据集非公开或评估集保密。

依据：[Understanding Cross-Language Transfer Improvements in Low-Resource HTR: The Role of Sequence Modeling](/20251022-20261021/2605.05900v1)；[Cross-Lingual Learning within Arabic Script for Low-Resource HTR](/20251022-20261021/2605.02089v2)；[Zero-Shot Synthetic-to-Real Handwritten Text Recognition via Task Analogies](/20251022-20261021/2604.09713v1)；[On the Generalization of Handwritten Text Recognition Models](/conference/cvpr-2025/cvpr-2025-garrido-munoz-on-the-generalization-of-handwritten-text-recognition-models-cvpr-2025-paper-on-the-generalization-of-handwritten-text-recognition-models)；[Performance Gap Analysis between Latin and Arabic Scripts HTR](/20251022-20261021/2606.18884v1)；[Handwritten Text Recognition for Low Resource Languages](/20251022-20261021/2512.01348v1)；[UniLipi: A Unified Multi-Script OCR for Historical Indic Manuscripts](/20251022-20261021/2608.28195v1)；[Digitizing Nepal&&#35;x27;s Written Heritage: A Comprehensive HTR Pipeline for Old Nepali Manuscripts](/20251022-20261021/2512.17111v2)

## 子方向四：数据集、标注质量与评测基准

这一子方向覆盖“用什么数据训练与评测、标注错误如何影响结论”。给定论文提供多类资源：Urdu Katib、BullingerDB、SCAM、DohaScript、HANS、OmniHandwritingOCR、WildHandBench等，分别面向历史乌尔都文、历史多语手稿、科普特手稿、天城文连续手写、学生答题纸、多模态大模型诊断与真实退化手写理解。RefLAM提出参考文本对齐的行级标注流水线与AraMS-28k。CER-HV提出基于CRNN的标签错误检测加人工复核。Measuring Annotation Efficiency用样本复杂度曲线量化预训练节省的标注量。评测方面，OmniHandwritingOCR与WildHandBench强调多模态模型在复杂手写与公式上的失败模式与先验驱动错误。证据不足说明：各数据集的许可、划分与基线协议在摘要中未必完整；本导读不补写未给出的基准数字。

依据：[Urdu Katib Handwritten Dataset: A Historical Document Dataset for Offline Urdu Handwritten Text Recognition with CRNN-Based Baseline Evaluation](/20251022-20261021/2606.19139v1)；[BullingerDB: A Dataset for Handwritten Text Recognition and Writer Retrieval](/20251022-20261021/2605.30235v1)；[A Text Recognition Dataset from Sahidic Coptic Ancient Manuscripts](/20251022-20261021/2606.15987v2)；[DohaScript: A Large-Scale Multi-Writer Dataset for Continuous Handwritten Hindi Text](/20251022-20261021/2602.18089v1)；[HANS: A Handwritten Answer Sheet Dataset for Noisy Hybrid Document Parsing](/20251022-20261021/2610.12363v1)；[OmniHandwritingOCR: A Diagnostic Benchmark for Evaluating Multimodal LLMs in Handwritten OCR Scenarios](/20251022-20261021/2608.18586v1)；[WildHandBench: A Benchmark for Handwritten Text Understanding that Challenges MLLMs and Humans](/20251022-20261021/2608.22959v1)；[RefLAM: A Reference-Grounded Line Annotation Pipeline for Historical Arabic Manuscripts](/20251022-20261021/2608.25140v1)；[A Human-in-the-Loop Label Error Detection Framework Applied to Arabic-Script HTR Datasets](/20251022-20261021/2601.16713v4)；[Measuring Annotation Efficiency for Handwritten Devanagari Recognition: Sample-Complexity Curves for Four Pretraining Regimes](/20251022-20261021/2609.16859v1)

## 子方向五：历史文档、版面与端到端流水线

这一子方向关注“从整页图像到文本”的工程链路，包括行检测、阅读顺序、行识别与后处理。给定论文中，FP-THD把版面分析模型与文本行识别结合做整页转写；End-to-End Text Line Detection and Ordering把行检测与阅读顺序统一为图像到序列问题；Application of deep learning approaches for medieval historical documents展示中世纪拉丁文献的检测到词识别流程；TrOCR for Medieval HTR与BullingerDB提供历史手写适配与评测场景；CHURRO用开放权重视觉语言模型覆盖大规模历史语料；Adapting PP-OCRv6 for Historical Text Recognition比较紧凑识别器与CRNN在历史行上的表现；A Benchmark of State-Space Models vs. Transformers and BiLSTM-based Models for Historical Newspaper OCR比较多种序列模型与现成OCR引擎。证据边界：这些工作多依赖各自馆藏与标注协议，跨集合可复现性需以论文公开的代码与协议为准；摘要中出现的链接不在此转写。

依据：[FP-THD: Full page transcription of historical documents](/20251022-20261021/2601.17040v1)；[End-to-End Text Line Detection and Ordering](/20251022-20261021/2606.04166v1)；[Application of deep learning approaches for medieval historical documents transcription](/20251022-20261021/2512.18865v1)；[TrOCR for Medieval HTR: A Systematic Ablation Study with Cross-Dataset Validation](/20251022-20261021/2606.24302v1)；[BullingerDB: A Dataset for Handwritten Text Recognition and Writer Retrieval](/20251022-20261021/2605.30235v1)；[CHURRO: Making History Readable with an Open-Weight Large Vision-Language Model for High-Accuracy, Low-Cost Historical Text Recognition](/conference/emnlp-2025/anthology-2025emnlp-main1763-churro-making-history-readable-with-an-open-weight-large-vision-language-model-for-high-accuracy-low-cost-historical-text-recognition)；[A Free Lunch? Adapting PP-OCRv6 for Historical Text Recognition](/20251022-20261021/2609.20064v1)；[A Benchmark of State-Space Models vs. Transformers and BiLSTM-based Models for Historical Newspaper OCR](/20251022-20261021/2604.00725v2)

## 评测、进展与局限（跨子方向综合）

综合给定论文可见的进展：序列建模从CRNN-CTC扩展到Transformer编码器-解码器、线性时间RetNet、Mamba与脉冲网络；预训练与上下文适配被用于缓解标注稀缺与书写者差异；低资源跨语言研究开始用受控实验区分视觉共享与序列建模的贡献；数据集与标注质量工作表明标签错误和字符分布偏移会显著影响评测。局限也很明确：不同论文的数据集、划分、语言与解码设置不同，CER/WER不可直接横比；多模态大模型在复杂手写、公式与真实退化场景仍出现幻觉与先验驱动错误；状态空间模型在真实手写行上仍落后于Transformer基线，且被指出对长序列数据更饥渴；部分低资源评估集保密或非公开，复现需依赖作者释放的代码与配置。证据不足说明：本导读未获得统一的基准复跑结果，因此不给出跨论文排名或“最佳模型”结论。

依据：[Systematic Literature Review of Machine Learning Models and Applications for Text Recognition](/20251022-20261021/2608.26500v1)；[On the Generalization of Handwritten Text Recognition Models](/conference/cvpr-2025/cvpr-2025-garrido-munoz-on-the-generalization-of-handwritten-text-recognition-models-cvpr-2025-paper-on-the-generalization-of-handwritten-text-recognition-models)；[Performance Gap Analysis between Latin and Arabic Scripts HTR](/20251022-20261021/2606.18884v1)；[WildHandBench: A Benchmark for Handwritten Text Understanding that Challenges MLLMs and Humans](/20251022-20261021/2608.22959v1)；[OmniHandwritingOCR: A Diagnostic Benchmark for Evaluating Multimodal LLMs in Handwritten OCR Scenarios](/20251022-20261021/2608.18586v1)；[Scaling State-Space Models from Lines to Paragraphs: An Ablation of Mamba-based OCR](/20251022-20261021/2606.23524v1)；[A Human-in-the-Loop Label Error Detection Framework Applied to Arabic-Script HTR Datasets](/20251022-20261021/2601.16713v4)；[Measuring Annotation Efficiency for Handwritten Devanagari Recognition: Sample-Complexity Curves for Four Pretraining Regimes](/20251022-20261021/2609.16859v1)

## 建议阅读顺序

以下为建议学习顺序，不是公布时间排序。

1. [Systematic Literature Review of Machine Learning Models and Applications for Text Recognition](/20251022-20261021/2608.26500v1) · 入门
   - 阅读理由：系统综述提供OCR/HTR模型、应用与挑战的整体地图，适合建立术语与问题框架。
   - 公布时间：2026-08-27（日精度）
   - arxiv · 2026-08-27（日精度）：[原文](https://arxiv.org/pdf/2608.26500v1)

2. [Urdu Katib Handwritten Dataset: A Historical Document Dataset for Offline Urdu Handwritten Text Recognition with CRNN-Based Baseline Evaluation](/20251022-20261021/2606.19139v1) · 入门
   - 阅读理由：以CRNN混合模型与CTC基线展示文本行识别的基本训练与评测流程，并附数据集背景。
   - 公布时间：2026-06-17（日精度）
   - arxiv · 2026-06-17（日精度）：[原文](https://arxiv.org/pdf/2606.19139v1) / [PDF](https://arxiv.org/pdf/2606.19139v1)

3. [Understanding Cross-Language Transfer Improvements in Low-Resource HTR: The Role of Sequence Modeling](/20251022-20261021/2605.05900v1) · 入门
   - 阅读理由：受控比较CNN-CTC与CRNN，帮助理解序列建模在低资源迁移中的作用。
   - 公布时间：2026-05-07（日精度）
   - arxiv · 2026-05-07（日精度）：[原文](https://arxiv.org/pdf/2605.05900v1) / [PDF](https://arxiv.org/pdf/2605.05900v1)

4. [Cross-Lingual Learning within Arabic Script for Low-Resource HTR](/20251022-20261021/2605.02089v2) · 入门
   - 阅读理由：在阿拉伯字母系多语言上比较CRNN与HTR-VT，适合作为跨语言入门案例。
   - 公布时间：2026-05-03（日精度）
   - arxiv · 2026-05-03（日精度）：[原文](https://arxiv.org/pdf/2605.02089v2) / [PDF](https://arxiv.org/pdf/2605.02089v2)

5. [HTR-ConvText: Leveraging Convolution and Textual Information for Handwritten Text Recognition](/20251022-20261021/2512.05021v1) · 进阶
   - 阅读理由：展示卷积加MobileViT与文本上下文注入的混合架构，连接CNN与Transformer路线。
   - 公布时间：2025-12-04（日精度）
   - arxiv · 2025-12-04（日精度）：[原文](https://arxiv.org/pdf/2512.05021v1) / [PDF](https://arxiv.org/pdf/2512.05021v1)

6. [DRetHTR: Linear-Time Decoder-Only Retentive Network for Handwritten Text Recognition](/20251022-20261021/2602.17387v1) · 进阶
   - 阅读理由：用RetNet解码器讨论线性时间与内存，适合理解Transformer解码的效率瓶颈。
   - 公布时间：2026-02-19（日精度）
   - arxiv · 2026-02-19（日精度）：[原文](https://arxiv.org/pdf/2602.17387v1) / [PDF](https://arxiv.org/pdf/2602.17387v1)

7. [TrOCR for Medieval HTR: A Systematic Ablation Study with Cross-Dataset Validation](/20251022-20261021/2606.24302v1) · 进阶
   - 阅读理由：系统消融TrOCR微调选择，适合学习预训练模型适配小数据集的实验设计。
   - 公布时间：2026-06-23（日精度）
   - arxiv · 2026-06-23（日精度）：[原文](https://arxiv.org/pdf/2606.24302v1) / [PDF](https://arxiv.org/pdf/2606.24302v1)

8. [Handwritten Text Recognition Lives in the High-Pixel Variance Subspace](/20251022-20261021/2609.35473v1) · 进阶
   - 阅读理由：比较三类自监督目标并讨论像素空间判别信号，适合理解预训练为何有效。
   - 公布时间：2026-09-28（日精度）
   - arxiv · 2026-09-28（日精度）：[原文](https://arxiv.org/pdf/2609.35473v1)

9. [N-gram Injection into Transformers for Dynamic Language Model Adaptation in Handwritten Text Recognition](/20251022-20261021/2603.03930v2) · 进阶
   - 阅读理由：n-gram注入解码器处理语言分布偏移，适合学习语言模型与识别器的结合方式。
   - 公布时间：2026-03-04（日精度）
   - arxiv · 2026-03-04（日精度）：[原文](https://arxiv.org/pdf/2603.03930v2) / [PDF](https://arxiv.org/pdf/2603.03930v2)

10. [On the Generalization of Handwritten Text Recognition Models](/conference/cvpr-2025/cvpr-2025-garrido-munoz-on-the-generalization-of-handwritten-text-recognition-models-cvpr-2025-paper-on-the-generalization-of-handwritten-text-recognition-models) · 进阶
   - 阅读理由：分布外泛化分析覆盖多模型多数据集，适合建立对真实部署风险的判断。
   - 公布时间：2025（年精度）
   - CVPR-2025-Accepted · 2025（年精度）：[原文](https://openaccess.thecvf.com/content/CVPR2025/html/Garrido-Munoz_On_the_Generalization_of_Handwritten_Text_Recognition_Models_CVPR_2025_paper.html)

11. [Performance Gap Analysis between Latin and Arabic Scripts HTR](/20251022-20261021/2606.18884v1) · 进阶
   - 阅读理由：统一CRNN比较拉丁与阿拉伯脚本，讨论标注质量与字符分布，适合深入评测偏差。
   - 公布时间：2026-06-17（日精度）
   - arxiv · 2026-06-17（日精度）：[原文](https://arxiv.org/pdf/2606.18884v1) / [PDF](https://arxiv.org/pdf/2606.18884v1)

12. [A Benchmark of State-Space Models vs. Transformers and BiLSTM-based Models for Historical Newspaper OCR](/20251022-20261021/2604.00725v2) · 专题
   - 阅读理由：比较SSM、Transformer与BiLSTM及多种解码策略，适合理解长序列OCR的架构取舍。
   - 公布时间：2026-04-01（日精度）
   - arxiv · 2026-04-01（日精度）：[原文](https://arxiv.org/pdf/2604.00725v2) / [PDF](https://arxiv.org/pdf/2604.00725v2)

13. [Scaling State-Space Models from Lines to Paragraphs: An Ablation of Mamba-based OCR](/20251022-20261021/2606.23524v1) · 专题
   - 阅读理由：从行到段落的Mamba消融，揭示状态空间模型在真实手写上的数据饥渴问题。
   - 公布时间：2026-06-22（日精度）
   - arxiv · 2026-06-22（日精度）：[原文](https://arxiv.org/pdf/2606.23524v1) / [PDF](https://arxiv.org/pdf/2606.23524v1)

14. [Spike-HTR: Spiking Neural Transformer for Handwritten Text Recognition](/20251022-20261021/2608.01646v1) · 专题
   - 阅读理由：脉冲神经网络与CTC引导压缩代表非主流高效推理路线，适合作为专题拓展。
   - 公布时间：2026-08-03（日精度）
   - arxiv · 2026-08-03（日精度）：[原文](https://arxiv.org/pdf/2608.01646v1)
   - ICML-2026-Accepted · 2026（年精度）：[原文](https://openreview.net/forum?id=3UcWAgr0jx) / [PDF](https://openreview.net/pdf/33ce4b0405d1a93156996cf3f098918cfdaaac7d.pdf)

15. [ExpertHTR: Unified Handwritten Text Recognition with Multi-Task Learning and Sparse Mixture-of-Experts](/20251022-20261021/2609.12705v1) · 专题
   - 阅读理由：多任务与稀疏专家统一页面级训练，适合研究异构数据联合训练与条件容量。
   - 公布时间：2026-09-11（日精度）
   - arxiv · 2026-09-11（日精度）：[原文](https://arxiv.org/pdf/2609.12705v1)

16. [Exploring In-Context Learning for Handwritten Text Recognition](/20251022-20261021/2609.37195v1) · 专题
   - 阅读理由：上下文学习不更新参数做转写，适合评估通用视觉语言模型在HTR中的边界。
   - 公布时间：2026-09-29（日精度）
   - arxiv · 2026-09-29（日精度）：[原文](https://arxiv.org/pdf/2609.37195v1)

17. [WildHandBench: A Benchmark for Handwritten Text Understanding that Challenges MLLMs and Humans](/20251022-20261021/2608.22959v1) · 专题
   - 阅读理由：诊断基准揭示多模态模型先验驱动错误，适合专题研究评测指标与失败模式。
   - 公布时间：2026-08-24（日精度）
   - arxiv · 2026-08-24（日精度）：[原文](https://arxiv.org/pdf/2608.22959v1)

18. [A Human-in-the-Loop Label Error Detection Framework Applied to Arabic-Script HTR Datasets](/20251022-20261021/2601.16713v4) · 专题
   - 阅读理由：标签错误检测与人工复核框架，适合专题研究数据质量对HTR评测的影响。
   - 公布时间：2026-01-23（日精度）
   - arxiv · 2026-01-23（日精度）：[原文](https://arxiv.org/pdf/2601.16713v4) / [PDF](https://arxiv.org/pdf/2601.16713v4)

19. [Measuring Annotation Efficiency for Handwritten Devanagari Recognition: Sample-Complexity Curves for Four Pretraining Regimes](/20251022-20261021/2609.16859v1) · 专题
   - 阅读理由：样本复杂度曲线量化预训练节省的标注量，适合专题研究标注效率实验设计。
   - 公布时间：2026-09-15（日精度）
   - arxiv · 2026-09-15（日精度）：[原文](https://arxiv.org/pdf/2609.16859v1)

20. [RefLAM: A Reference-Grounded Line Annotation Pipeline for Historical Arabic Manuscripts](/20251022-20261021/2608.25140v1) · 专题
   - 阅读理由：参考文本对齐的行级标注流水线，适合专题研究可扩展标注与质量保证。
   - 公布时间：2026-08-25（日精度）
   - arxiv · 2026-08-25（日精度）：[原文](https://arxiv.org/pdf/2608.25140v1)

任务：研究方向大礼包

固定窗口：arXiv &#91;2025-10-22, 2026-10-22&#41;；会议 &#91;2024-10-22, 2026-10-22&#41;（UTC，结束日不含）

本次候选评审上限 300，最终名单上限 100；本轮内容预算 10。

覆盖限制：仅检索配置范围内已有库存与预算内候选；向量/会议Top-k召回并非全库遍历，不保证找全相关论文。未核实录用、日期边界和缺失库存不能当作已覆盖。

缺失库存：eccv 2025、emnlp 2026、neurips 2026。

研究需求：离线文本行手写识别入门、技术路线与可复现基线

# hf

以下为本次固定最终名单，按相关性评分降序；不代表全部相关论文。

1. [HTR-ConvText: Leveraging Convolution and Textual Information for Handwritten Text Recognition](https://arxiv.org/abs/2512.05021v1) · 分数 9
2. [Spike-HTR: Spiking Neural Transformer for Handwritten Text Recognition](https://arxiv.org/abs/2608.01646v1) · 分数 9
3. [DRetHTR: Linear-Time Decoder-Only Retentive Network for Handwritten Text Recognition](https://arxiv.org/abs/2602.17387v1) · 分数 9
4. [ExpertHTR: Unified Handwritten Text Recognition with Multi-Task Learning and Sparse Mixture-of-Experts](https://arxiv.org/abs/2609.12705v1) · 分数 9
5. [Handwritten Text Recognition Lives in the High-Pixel Variance Subspace](https://arxiv.org/abs/2609.35473v1) · 分数 9
6. [TrOCR for Medieval HTR: A Systematic Ablation Study with Cross-Dataset Validation](https://arxiv.org/abs/2606.24302v1) · 分数 9
7. [Digitizing Nepal&&#35;x27;s Written Heritage: A Comprehensive HTR Pipeline for Old Nepali Manuscripts](https://arxiv.org/abs/2512.17111v2) · 分数 9
8. [Understanding Cross-Language Transfer Improvements in Low-Resource HTR: The Role of Sequence Modeling](https://arxiv.org/abs/2605.05900v1) · 分数 9
9. [Cross-Lingual Learning within Arabic Script for Low-Resource HTR](https://arxiv.org/abs/2605.02089v2) · 分数 9
10. [Urdu Katib Handwritten Dataset: A Historical Document Dataset for Offline Urdu Handwritten Text Recognition with CRNN-Based Baseline Evaluation](https://arxiv.org/abs/2606.19139v1) · 分数 9
11. [A Free Lunch? Adapting PP-OCRv6 for Historical Text Recognition](https://arxiv.org/abs/2609.20064v1) · 分数 9
12. [On the Generalization of Handwritten Text Recognition Models](https://openaccess.thecvf.com/content/CVPR2025/html/Garrido-Munoz_On_the_Generalization_of_Handwritten_Text_Recognition_Models_CVPR_2025_paper.html) · 分数 8
13. [Exploring In-Context Learning for Handwritten Text Recognition](https://arxiv.org/abs/2609.37195v1) · 分数 8
14. [Few-shot Writer Adaptation via Multimodal In-Context Learning](https://arxiv.org/abs/2603.29450v1) · 分数 8
15. [Performance Gap Analysis between Latin and Arabic Scripts HTR](https://arxiv.org/abs/2606.18884v1) · 分数 8
16. [N-gram Injection into Transformers for Dynamic Language Model Adaptation in Handwritten Text Recognition](https://arxiv.org/abs/2603.03930v2) · 分数 8
17. [MetaWriter: Personalized Handwritten Text Recognition Using Meta-Learned Prompt Tuning](https://openaccess.thecvf.com/content/CVPR2025/html/Gu_MetaWriter_Personalized_Handwritten_Text_Recognition_Using_Meta-Learned_Prompt_Tuning_CVPR_2025_paper.html) · 分数 8
18. [Zero-Shot Synthetic-to-Real Handwritten Text Recognition via Task Analogies](https://arxiv.org/abs/2604.09713v1) · 分数 8
19. [BullingerDB: A Dataset for Handwritten Text Recognition and Writer Retrieval](https://arxiv.org/abs/2605.30235v1) · 分数 8
20. [Learning to Align: Addressing Character Frequency Distribution Shifts in Handwritten Text Recognition](https://aclanthology.org/2025.findings-emnlp.1014/) · 分数 8
21. [A Benchmark of State-Space Models vs. Transformers and BiLSTM-based Models for Historical Newspaper OCR](https://arxiv.org/abs/2604.00725v2) · 分数 8
22. [A Text Recognition Dataset from Sahidic Coptic Ancient Manuscripts](https://arxiv.org/abs/2606.15987v2) · 分数 8
23. [Measuring Annotation Efficiency for Handwritten Devanagari Recognition: Sample-Complexity Curves for Four Pretraining Regimes](https://arxiv.org/abs/2609.16859v1) · 分数 8
24. [Scaling State-Space Models from Lines to Paragraphs: An Ablation of Mamba-based OCR](https://arxiv.org/abs/2606.23524v1) · 分数 8
25. [Application of deep learning approaches for medieval historical documents transcription](https://arxiv.org/abs/2512.18865v1) · 分数 8
26. [Handwritten Text Recognition for Low Resource Languages](https://arxiv.org/abs/2512.01348v1) · 分数 7
27. [Efficient Domain Adaptation for Text Line Recognition via Decoupled Language Models](https://arxiv.org/abs/2603.28028v1) · 分数 7
28. [OmniHandwritingOCR: A Diagnostic Benchmark for Evaluating Multimodal LLMs in Handwritten OCR Scenarios](https://arxiv.org/abs/2608.18586v1) · 分数 7
29. [RefLAM: A Reference-Grounded Line Annotation Pipeline for Historical Arabic Manuscripts](https://arxiv.org/abs/2608.25140v1) · 分数 7
30. [Seeing Justice Clearly: Handwritten Legal Document Translation with OCR and Vision-Language Models](https://arxiv.org/abs/2512.18004v1) · 分数 7
31. [DTRNet: Dual Text-Radical Decoding for Handwritten Chinese Text Recognition with Faked Character Detection](https://arxiv.org/abs/2608.05848v1) · 分数 7
32. [DohaScript: A Large-Scale Multi-Writer Dataset for Continuous Handwritten Hindi Text](https://arxiv.org/abs/2602.18089v1) · 分数 7
33. [UniLipi: A Unified Multi-Script OCR for Historical Indic Manuscripts](https://arxiv.org/abs/2608.28195v1) · 分数 7
34. [Generative Text Modelling and Language-Guided Visual Attention for Deciphering Palimpsests](https://arxiv.org/abs/2610.24060v1) · 分数 7
35. [FP-THD: Full page transcription of historical documents](https://arxiv.org/abs/2601.17040v1) · 分数 7
36. [End-to-End Text Line Detection and Ordering](https://arxiv.org/abs/2606.04166v1) · 分数 6
37. [A Human-in-the-Loop Label Error Detection Framework Applied to Arabic-Script HTR Datasets](https://arxiv.org/abs/2601.16713v4) · 分数 6
38. [Adapting TrOCR for Printed Tigrinya Text Recognition: Word-Aware Loss Weighting for Cross-Script Transfer Learning](https://arxiv.org/abs/2604.20813v1) · 分数 6
39. [WildHandBench: A Benchmark for Handwritten Text Understanding that Challenges MLLMs and Humans](https://arxiv.org/abs/2608.22959v1) · 分数 6
40. [Towards a Joint Khmer Text Recognition and Word Segmentation](https://arxiv.org/abs/2608.30213v1) · 分数 6
41. [An Effective Data Augmentation Method by Asking Questions about Scene Text Images](https://arxiv.org/abs/2603.03580v1) · 分数 6
42. [LLM-Driven AutoML for Cross-Lingual Handwritten OCR: Closed-Loop Neural Architecture Search with GPT-5, GPT-4o, and Claude Sonnet 4](https://arxiv.org/abs/2607.15509v3) · 分数 6
43. [HANS: A Handwritten Answer Sheet Dataset for Noisy Hybrid Document Parsing](https://arxiv.org/abs/2610.12363v1) · 分数 6
44. [ScribeTokens: Fixed-Vocabulary Tokenization of Digital Ink](https://arxiv.org/abs/2603.02805v1) · 分数 6
45. [How Far Can Synthetic Data Take Thai OCR?](https://arxiv.org/abs/2609.03595v1) · 分数 6
46. [CHURRO: Making History Readable with an Open-Weight Large Vision-Language Model for High-Accuracy, Low-Cost Historical Text Recognition](https://aclanthology.org/2025.emnlp-main.1763/) · 分数 6
47. [Systematic Literature Review of Machine Learning Models and Applications for Text Recognition](https://arxiv.org/abs/2608.26500v1) · 分数 6

[按公布时间查看](#/starter-pack/20261022-7dd45f1f8e74/dates)

阅读内容：已完成 10，待补充 37。
