# Sci-PRM: A Tool-Aware Process Reward Model for Scientific Reasoning Verification

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/InternScience/Sci-PRM)

Welcome to the official repository for **Sci-PRM**, an efficient Process Reward Model (PRM) designed to provide fine-grained supervision for complex scientific reasoning. 

While PRMs have achieved remarkable success in mathematical reasoning, their application in complex scientific domains (such as biology, chemistry, physics, and earth science) remains largely unexplored. Scientific problems demand not only logical rigor but also factual consistency and precise usage of domain-specific tools. Sci-PRM bridges this gap by effectively mitigating hallucinations and verifying tool selection, execution accuracy, and result interpretation.

## ✨ Key Features

* **SCIPRM70K Dataset:** A large-scale, multi-disciplinary dataset featuring "Chain-of-Tool" trajectories that explicitly interleave reasoning with the execution of scientific tools.
* **Fine-Grained Supervision:** Provides accurate step-level evaluation on three dimensions: tool selection correctness, tool calling accuracy, and result validity/utilization.
* **Test-Time Scaling (Best-of-N):** Aggregates trajectory-level rewards to help base models select the most reliable and evidence-consistent reasoning paths during inference.
* **Reinforcement Learning (RL) Integration:** Serves as a dense, high-quality reward signal during RL training, mitigating the issue of sparse advantages and allowing models to break through existing performance ceilings without the prohibitive latency of live sandbox execution.

## 📊 Dataset & Supported Tools

The **SCIPRM70K** dataset contains **17,818 tool-integrated trajectories** and **86,314 annotated reasoning steps**.

* **Domains:** Biology, Chemistry, Physics, Earth Science, and General Scientific inquiry.
* **Tool Suite:**
  * **Web Search:** For factual grounding, evidence retrieval, and citation verification.
  * **Python Code Execution:** For quantitative computation and domain-specific processing using essential scientific libraries such as `rdkit`, `numpy`, `sympy`, `pyscf`, and `biopython`.

## 🧠 Methodology

Sci-PRM is initialized with the **Qwen3-VL-8B** backbone and trained using a two-stage curriculum:

1. **Supervised Fine-Tuning (SFT):** Transfers domain-specific grounding knowledge by training the model to predict the reasoning process and step-correctness labels simultaneously.
2. **Reinforcement Learning (DAPO-GRPO):** Utilizes Dynamic Advantage Policy Optimization to improve verification consistency, allowing the model to explore alternative reasoning paths and self-correct based on relative performance.

## 🚀 Performance Highlights

* **Efficiency & Accuracy:** Sci-PRM accurately detects code logic flaws and citation hallucinations without the massive overhead of live execution. On the Mol-Instructions subset, it achieves an accuracy of 0.76 with an inference speed of only 0.76s per query (compared to ~282s for live execution with external APIs).
* **Superior RL Rewards:** When used for Reinforcement Learning on complex biomolecular reasoning tasks, Sci-PRM achieved a massive **+14.4 point gain** over a standard Outcome Reward Model (ORM).
* **Domain Specialization:** Maintains high accuracy on tool-calling steps in scientific domains, significantly outperforming general-purpose judges like GPT-5-Mini, which tend to degrade substantially in these scenarios.

## 📎 Citation

If you find our model, dataset, or code useful for your research, please consider citing our paper:

```bibtex
@article{zhao2026sciprm,
  title={Sci-PRM: A Tool Aware Process Reward Model for Scientific Reasoning Verification},
  author={Zhao, Xiangyu and Zhao, Henry Hengyuan and Wang, Yiheng and Xu, Wanghan and Zhou, Yuhao and Cao, Qinglong and Zhou, Zhiwang and Bai, Lei and Zhang, Wenlong and Wu, Xiao-Ming},
  journal={arXiv preprint},
  year={2026}
}
