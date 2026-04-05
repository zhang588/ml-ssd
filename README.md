# Simple Self-Distillation (SSD) - 简单自蒸馏

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)
![Stars](https://img.shields.io/github/stars/zhang588/ml-ssd?style=social)

> 🔥 **Apple Research 开源代码** - 一种简单却极其有效的代码生成模型后训练方法

## 📖 项目简介

本仓库是 Apple Research 论文 **"Embarrassingly Simple Self-Distillation Improves Code Generation"** 的复现实现。

**核心发现**：代码模型的"正确能力"其实已经藏在权重里了，只是被 greedy decoding 锁住了。用自己生成的数据再训练一轮，就能挖掘出隐藏实力！

## 🎯 三步实现

```
1. Sample  → 从冻结模型采样（非单位温度）
2. Fine-tune → 用原始未验证输出做标准交叉熵微调  
3. Decode → 用单独调优的温度解码
```

**不需要：**
- ❌ 更好的教师模型
- ❌ 验证器（正确性检查）
- ❌ 强化学习
- ❌ 代码执行环境
- ❌ 外部标签

## 📊 效果惊艳

| 模型 | Pass@1 提升 | Pass@5 提升 |
|------|------------|------------|
| Qwen3-30B-Instruct | 42.4% → 55.3% (+30%) | 31.1% → 54.1% |

- 每个 prompt 只需一个样本
- 在 4B、8B、30B 规模都有效
- 困难问题提升尤为显著

## 🚀 快速开始

### 安装

```bash
git clone https://github.com/zhang588/ml-ssd.git
cd ml-ssd
uv sync --group evaluation
```

### 使用

```bash
# 评估
python -m evaluation.eval --help

# 运行基准测试
python -m evaluation.benchmark --model <model_name>
```

## 📁 项目结构

```
ml-ssd/
├── evaluation/
│   ├── eval.py              # CLI 入口
│   ├── benchmark.py          # LiveCodeBench v6 实现
│   └── livecodebench_utils.py # 代码执行工具
├── figures/
│   └── fig_teaser.png       # 论文图表
├── pyproject.toml
└── README.md
```

## 📄 原论文

- **arXiv**: [2604.01193](https://arxiv.org/abs/2604.01193)
- **作者**: Ruixiang Zhang*, Richard He Bai*, Huangjie Zheng*, Navdeep Jaitly, Ronan Collobert, Yizhe Zhang*

## 🔗 相关链接

- 🌐 [GitHub 仓库](https://github.com/zhang588/ml-ssd)
- 📄 [原仓库 (apple/ml-ssd)](https://github.com/apple/ml-ssd)
- 📝 [论文 (arXiv)](https://arxiv.org/abs/2604.01193)
- 🤗 模型权重 (即将发布)

## 📚 引用

```bibtex
@misc{zhang2026embarrassinglysimpleselfdistillationimproves,
  title={Embarrassingly Simple Self-Distillation Improves Code Generation},
  author={Ruixiang Zhang and Richard He Bai and Huangjie Zheng and Navdeep Jaitly and Ronan Collobert and Yizhe Zhang},
  year={2026},
  eprint={2604.01193},
  archivePrefix={arXiv},
  primaryClass={cs.CL}
}
```

## 📝 License

Apache 2.0 License
