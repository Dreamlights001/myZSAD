# 零样本工业瑕疵检测方法综述

## 引言
零样本工业瑕疵检测（Zero-Shot Anomaly Detection, ZSAD）是一种新兴的机器学习范式，旨在在没有特定瑕疵类别训练数据的情况下检测工业产品中的异常。这种方法特别适用于工业场景，因为收集标注的瑕疵数据往往成本高昂或受限于隐私问题。近年来，随着视觉-语言模型（如CLIP）、基础模型（如Segment Anything, SAM）和多模态大语言模型（Multimodal Large Language Models, MLLMs）的发展，ZSAD在工业瑕疵检测中取得了显著进展。本综述整理了2023年至2025年（截至2025年5月10日）的关键方法，分析其核心技术、性能和应用场景，旨在为研究和实践提供参考。

## 方法分类与描述

### 1. 基于CLIP的零样本异常检测方法
CLIP（Contrastive Language-Image Pretraining）是一种强大的视觉-语言模型，广泛用于零样本任务。以下方法基于CLIP的扩展：

#### 1.1 WinCLIP/WinCLIP+（2023）
- **描述**：WinCLIP利用基于窗口的策略，通过CLIP匹配图像块的视觉特征与描述正常和异常状态的文本提示，进行分割和分类。WinCLIP+结合少量正常样本的参考关联和Compositional Prompt Ensemble (CPE)，增强性能。
- **核心技术**：窗口化特征匹配、CPE、参考关联。
- **性能**：在 [MVTec-AD](https://www.mvtec.com/company/research/datasets/mvtec-ad) 和 [VisA](https://github.com/VisA-Dataset) 数据集上表现出色，提供灵活的零/少样本性能，但对逻辑异常和小瑕疵的检测能力有限。
- **应用场景**：适合快速部署的2D图像瑕疵检测。
- **代码**：可用代码仓库 [GitHub - caoyunkang/WinCLIP](https://github.com/caoyunkang/WinClip)。

#### 1.2 AnoVL（2023）
- **描述**：通过训练免费的适应（Training-Free Adaptation, TFA）和测试时适应（Test-Time Adaptation, TTA）模块，增强CLIP进行统一异常定位，优化视觉-语言对齐和定位精度。
- **核心技术**：TFA、TTA、伪标签优化。
- **性能**：提供真正的零样本能力，效率高，但在性能上可能落后于完全监督的方法。
- **应用场景**：适用于数据稀缺的工业场景。
- **代码**：可用代码仓库 [GitHub - hq-deng/AnoVL](https://github.com/hq-deng/AnoVL)。

#### 1.3 AnomalyCLIP（2023）
- **描述**：学习对象无关的文本提示，捕获通用的正常和异常状态，适用于多样化数据集的异常检测。
- **核心技术**：对象无关提示学习、语义泛化。
- **性能**：在跨数据集泛化中表现优异，特别适合语义多样性高的场景。
- **应用场景**：适合多类别工业产品的异常检测。
- **状态**：详情见 [GitHub - AnomalyCLIP (Train once and test other)](https://github.com/zqhang/AnomalyCLIP)。

#### 1.4 PromptAD（2023）
- **描述**：采用双分支框架，利用CLIP的文本提示和跨视图学习，分别建模正常和异常状态。
- **核心技术**：双分支架构、跨视图学习。
- **性能**：提高特征可分性和鲁棒性，在零样本检测和定位中优于WinCLIP。
- **应用场景**：适合需要高鲁棒性的工业场景。
- **状态**：详情见 [GitHub - PromptAD Few-Shot Anomaly Detection](https://github.com/FuNz-0/PromptAD)。

#### 1.5 Random Word Data Augmentation with CLIP（2023）
- **描述**：通过随机词语操作CLIP的文本编码器生成合成训练数据，训练简单的前馈网络进行异常评分。
- **核心技术**：随机词语增强、简单前馈网络。
- **性能**：减少对复杂提示工程的依赖，提供竞争力的零样本性能，简单易用。
- **应用场景**：适合资源受限的快速部署场景。
- **状态**：待发布。

#### 1.6 AA-CLIP（2025）
- **描述**：通过使CLIP模型变得异常感知（anomaly-aware），显著提升零样本异常检测性能。采用两阶段适应策略：第一阶段创建异常感知文本锚点，第二阶段通过残差适配器对齐图像块级别视觉特征。
- **核心技术**：异常感知文本锚点、残差适配器、两阶段适应。
- **性能**：在工业和医疗数据集上显著优于原始CLIP模型，代码即将发布。
- **应用场景**：适合快速部署的工业和医疗场景。
- **论文**：[arXiv - AA-CLIP](https://arxiv.org/abs/2503.06661)。
- **代码**：[GitHub - Mwxinnn/AA-CLIP](https://github.com/Mwxinnn/AA-CLIP)。

#### 1.7 PA-CLIP（2025）
- **描述**：通过生成伪异常（pseudo-anomalies）增强CLIP的性能，帮助模型更好地泛化到未见过的异常类别。
- **核心技术**：伪异常感知、CLIP增强。
- **性能**：详情待2025年发布。
- **应用场景**：适合需要泛化能力的工业场景。
- **状态**：待发布。

#### 1.8 MFP-CLIP（2025）
- **描述**：探索不同形式提示（如文本提示、视觉提示）的功效，以增强CLIP在零样本工业异常检测中的表现。
- **核心技术**：多形式提示学习。
- **性能**：详情待2025年发布。
- **应用场景**：适合多样化提示需求的场景。
- **状态**：待发布。

#### 1.9 Crane（2025）
- **描述**：使用上下文引导的提示学习（context-guided prompt learning）和注意力细化（attention refinement）技术，通过利用上下文信息提高零样本异常检测的泛化能力。
- **核心技术**：上下文引导提示、注意力细化。
- **性能**：详情待2025年发布。
- **代码**：可用代码仓库 [GitHub - AlirezaSalehy/Crane](https://github.com/AlirezaSalehy/Crane)。

### 2. 基于SAM的零样本异常分割
这些方法利用现代基础模型（如Segment Anything）的零样本泛化能力，结合提示正则化技术：

#### 2.1 Segment Any Anomaly + (SAA+)（2023）
- **描述**：结合SAM和Grounding DINO，通过混合提示正则化（Hybrid Prompt Regularization）进行训练免费的异常分割，提示来源于领域专家知识和图像上下文。
- **核心技术**：混合提示正则化、SAM和Grounding DINO整合。
- **性能**：在 [VisA](https://github.com/VisA-Dataset)、[MVTec-AD](https://www.mvtec.com/company/research/datasets/mvtec-ad)、MTD和KSDD2等多个基准测试中达到最先进性能，无需标注数据。
- **应用场景**：适合高精度异常分割的工业场景。
- **代码**：可用代码仓库 [GitHub - caoyunkang/Segment-Any-Anomaly](https://github.com/caoyunkang/Segment-Any-Anomaly)。

#### 2.2 ClipSAM（2023）
- **描述**：整合CLIP的语义理解和SAM的精确分割，通过多尺度跨模态交互和掩码优化增强定位精度。
- **核心技术**：多尺度跨模态交互、掩码优化。
- **性能**：结合两者的优势，提高定位准确性，但增加复杂性，依赖初步CLIP输出。
- **应用场景**：适合需要高精度定位的场景。
- **状态**：详情见 [GitHub - lszcoding/ClipSAM](https://github.com/lszcoding/clipsam)。

### 3. 基于MLLMs的零样本异常检测与推理
这些方法利用多模态大语言模型（MLLMs）的推理能力：

#### 3.1 Anomaly-OV（2025）
- **描述**：引入Anomaly-OneVision（Anomaly-OV）视觉助手，利用MLLMs增强零样本异常检测和推理能力。通过“Look-Twice Feature Matching”机制突出异常区域，并创建Anomaly-Instruct-125k数据集和VisA-D&R基准。
- **核心技术**：MLLMs、Look-Twice Feature Matching、指令调优数据集。
- **性能**：在 [VisA-D&R](https://github.com/VisA-Dataset) 基准上优于现有MLLMs，细粒度异常检测表现突出，但复杂场景泛化能力需验证。
- **应用场景**：适合需要深入解释和决策支持的工业场景。
- **论文**：[arXiv - Anomaly-OV](https://arxiv.org/abs/2502.07601)。
- **状态**：详情见 [GitHub - honda-research-institute/Anomaly-OneVision](https://github.com/honda-research-institute/Anomaly-OneVision)。

#### 3.2 EIAD（2025）
- **描述**：专注于使用MLLMs提供可解释的异常检测洞察，增强工业应用的信任和决策支持。
- **核心技术**：MLLMs、可解释推理。
- **性能**：整合MLLM推理与视觉特征复杂，需进一步优化。
- **应用场景**：适合需要高可解释性的场景。
- **状态**：详情见 [GitHub - LeonardBarrera/eIAD](https://github.com/LeonardBarrera/eIAD)。

#### 3.3 LogSAD（2025）
- **描述**：训练免费的多模态框架，使用MLLMs（如GPT-4V）通过“match-of-thought”方法检测逻辑和结构异常。
- **核心技术**：MLLMs、match-of-thought推理。
- **性能**：解决工业过程中的复杂逻辑错误，在少样本设置中优于监督方法，但需要高级MLLM能力。
- **应用场景**：适合逻辑瑕疵检测。
- **状态**：详情见 [GitHub - zhang0jhon/LogSAD](https://github.com/zhang0jhon/LogSAD)。

### 4. 其他方法

#### 4.1 Bayesian Prompt Flow Learning for Zero-Shot Anomaly Detection（2025）
- **描述**：应用贝叶斯技术进行提示流学习，生成有效的提示以实现零样本异常检测。
- **核心技术**：贝叶斯提示学习。
- **性能**：详情待2025年发布。
- **应用场景**：适合需要动态提示优化的场景。
- **状态**：待发布。

#### 4.2 FiLo++（2025）
- **描述**：通过Fused Fine-Grained Descriptions (FusDes)和Deformable Localization (DefLoc)实现零/少样本异常检测。FusDes利用LLMs生成细粒度异常描述，DefLoc通过Grounding DINO和多尺度变形交互模块实现精确定位。
- **核心技术**：FusDes、DefLoc、多尺度交互。
- **性能**：在 [MVTec-AD](https://www.mvtec.com/company/research/datasets/mvtec-ad) 和 [VisA](https://github.com/VisA-Dataset) 数据集上取得最先进性能，图像级AUC达83.9%，像素级AUC达95.9%。
- **应用场景**：适合多样化异常和快速适应新类别的场景。
- **论文**：[arXiv - FiLo++](https://arxiv.org/abs/2501.10067)。
- **状态**：详情见 [GitHub - CASIA-IVA-Lab/FiLo](https://github.com/casia-iva-lab/filo)。
### 性能与比较
以下表格总结了主要方法的发布年份、核心技术、主要数据集和相关链接：

| 方法名称                                                                 | 发布年份 | 核心技术                                                                                     | 主要数据集                     | 相关链接                                                                                     |
|--------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------|-------------------------------|----------------------------------------------------------------------------------------------|
| WinCLIP/WinCLIP+                                                        | 2023     | 窗口策略、CPE、参考关联                                                           | MVTec-AD, VisA               | [GitHub](https://github.com/caoyunkang/WinClip)                     |
| AnoVL                                                                   | 2023     | TFA、TTA、伪标签优化                                                             | 多样化数据集                 | [GitHub](https://github.com/hq-deng/AnoVL)                                                   |
| AnomalyCLIP                                                             | 2023     | 对象无关提示学习、语义泛化                                                       | 多样化数据集                 | [GitHub](https://github.com/zqhang/AnomalyCLIP)                     |
| PromptAD                                                                | 2023     | 双分支架构、跨视图学习                                                           | MVTec-AD, VisA               | [GitHub](https://github.com/FuNz-0/PromptAD)                    |
| Random Word Data Augmentation with CLIP                                 | 2023     | 随机词语增强、简单前馈网络                                                       | MVTec-AD, VisA               |  待发布                                                                                 |
| SAA+                                                                    | 2023     | 混合提示正则化、SAM和Grounding DINO                                              | VisA, MVTec-AD, MTD, KSDD2   | [GitHub](https://github.com/caoyunkang/Segment-Any-Anomaly)                                  |
| ClipSAM                                                                 | 2023     | 多尺度跨模态交互、掩码优化                                                       | 工业数据集                   | [GitHub](https://github.com/lszcoding/clipsam)                 |
| Anomaly-OV                                                              | 2025     | MLLMs、Look-Twice Feature Matching、指令调优数据集                               | VisA-D&R                     | [arXiv](https://arxiv.org/abs/2502.07601), [GitHub](https://github.com/honda-research-institute/Anomaly-OneVision) |
| EIAD                                                                    | 2025     | MLLMs、可解释推理                                                                | 工业数据集                   | [GitHub](https://github.com/LeonardBarrera/eIAD)                     |
| LogSAD                                                                  | 2025     | MLLMs、match-of-thought推理                                                      | 工业数据集                   | [GitHub](https://github.com/zhang0jhon/LogSAD)                     |
| Bayesian Prompt Flow Learning                                           | 2025     | 贝叶斯提示学习                                                                   | 待定                         | 待发布                                                                                       |
| PA-CLIP                                                                 | 2025     | 伪异常感知、CLIP增强                                                             | 待定                         | 待发布                                                                                       |
| MFP-CLIP                                                                | 2025     | 多形式提示学习                                                                   | 待定                         | 待发布                                                                                       |
| Crane                                                                   | 2025     | 上下文引导提示、注意力细化                                                       | 待定                         | [GitHub](https://github.com/AlirezaSalehy/Crane)                                             |
| FiLo++                                                                  | 2025     | FusDes、DefLoc、多尺度交互                                                       | MVTec-AD, VisA               | [arXiv](https://arxiv.org/abs/2501.10067), [GitHub](https://github.com/casia-iva-lab/filo)      |
| AA-CLIP                                                                 | 2025     | 异常感知文本锚点、残差适配器、两阶段适应                                         | 工业和医疗数据集             | [arXiv](https://arxiv.org/abs/2503.06661), [GitHub](https://github.com/Mwxinnn/AA-CLIP)      |

## 讨论与未来方向
研究表明，基于CLIP的方法（如AnoVL、AA-CLIP）在零样本工业瑕疵检测中表现突出，适合快速部署和2D图像瑕疵检测。基于SAM的方法（如SAA+）在异常分割中精度高，无需标注数据，适合高精度需求场景。基于MLLMs的方法（如Anomaly-OV）提供推理和解释能力，适合需要决策支持的复杂场景。然而，不同数据集（如 [MVTec-AD](https://www.mvtec.com/company/research/datasets/mvtec-ad) 和 [VisA](https://github.com/VisA-Dataset)）上的性能可能因数据分布差异而异，复杂工业场景（如3D点云数据）的泛化能力仍需验证。

未来方向包括：
- **3D点云数据检测**：探索如 [Towards Zero-shot Point Cloud Anomaly Detection](https://arxiv.org/abs/2306.12345) 的方法，适应复杂工业场景。
- **无监督/半监督方法**：减少对领域专家知识的依赖，提升自动化程度。
- **多模态融合**：结合视觉、语言和逻辑推理，进一步提升检测精度和解释性。

## 结论
零样本工业瑕疵检测方法为工业场景提供了高效的异常检测解决方案，特别适合数据稀缺的情况。2023年至2025年间，基于CLIP、SAM和MLLMs的方法显著推动了该领域发展，2025年新方法如FiLo++和AA-CLIP进一步提升了细粒度检测和多样化异常处理能力。建议根据具体应用场景（如2D图像、3D点云或逻辑瑕疵）选择合适方法，并参考相关论文和代码仓库进行深入研究。

## 关键引文
- [Awesome Industrial Anomaly Detection GitHub Repository](https://github.com/M-3LAB/awesome-industrial-anomaly-detection)
- [AnoVL: Adapting Vision-Language Models for Unified Zero-shot Anomaly Localization](https://github.com/hq-deng/AnoVL)
- [Segment Any Anomaly without Training via Hybrid Prompt Regularization](https://github.com/caoyunkang/Segment-Any-Anomaly)
- [Crane: Context-Guided Prompt Learning and Attention Refinement](https://github.com/AlirezaSalehy/Crane)
- [FiLo++: Zero-/Few-Shot Anomaly Detection by Fused Fine-Grained Descriptions](https://arxiv.org/abs/2501.10067)
- [AA-CLIP: Enhancing Zero-Shot Anomaly Detection via Anomaly-Aware CLIP](https://arxiv.org/abs/2503.06661)
- [Towards Zero-Shot Anomaly Detection and Reasoning with Multimodal Large Language Models](https://arxiv.org/abs/2502.07601)
- [AA-CLIP GitHub Official Implementation](https://github.com/Mwxinnn/AA-CLIP)
- [MVTec Anomaly Detection Dataset](https://www.mvtec.com/company/research/datasets/mvtec-ad)
- [VisA Dataset for Industrial Anomaly Detection](https://github.com/VisA-Dataset)
- [Towards Zero-shot Point Cloud Anomaly Detection](https://arxiv.org/abs/2306.12345)
