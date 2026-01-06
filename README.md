# AS-NMRer: Improving Autoformalization for Non-monotonic Reasoning via Abstraction, Search, and Fine-tuning

This repository contains the source code and datasets for the paper **"AS-NMRer: Improving Autoformalization for Non-monotonic Reasoning via Abstraction, Search, and Fine-tuning"**.

**Note:** This submission is **anonymous** for double-blind review. All identifying information (author names, affiliations, specific paths) has been removed or obfuscated.

## 📖 Overview

AS-NMRer is a neuro-symbolic framework designed to enhance Large Language Models (LLMs) in non-monotonic reasoning (NMR) tasks. [cite_start]It addresses the challenges of linguistic noise and ambiguity through a three-stage process:

1.  **Abstraction:** Distills raw noisy contexts into atomic facts and default rules.
2.  **Step-wise Formalization:** Maps abstracted sentences to Answer Set Programming (ASP) logic programs using a verification-guided Best-of-N search.
3.  **Symbolic Solving:** Derives rigorous answers using a deterministic ASP solver.

Additionally, the framework includes an **Expert Iteration** mechanism for self-improvement via supervised fine-tuning on solver-verified trajectories.

## 📂 Repository Structure

The repository is organized into two main directories: `Code` and `Dataset`.

```text
.
├── Code/
│   └── AS_NMRer_with_DL_for_LogicBench/
│       ├── Ablation_Anaysis/            # Scripts for ablation studies (e.g., w/o Abstraction, w/o Search)
│       ├── AS-NMRer_for_LogicBench/     # Core implementation of the AS-NMRer framework
│       ├── Fine_Tuned_Models/           # Code for Expert Iteration and SFT using Unsloth/LoRA
│       ├── LLASP_for_LogicBench/        # Implementation of the LLM2ASP baseline
│       └── Zero_Few_Shot_for_LogicBench/# Scripts for Zero-shot and Few-shot prompting baselines
│
└── Dataset/
    ├── LogicBench/       # LogicBench (BQA task) dataset
    ├── Multi-LogiEval/        # Multi-LogiEval dataset (Reasoning depths 1-5)
    ├── LogicNMR/         # LogicNMR synthetic dataset (Dynamic updates)
    └── MultiLogicNMR/    # MultiLogicNMR dataset (Multi-extension scenarios)
```

### Prerequisites
To reproduce the experiments, you will need the following dependencies.
* Python 3.11
* ASP Solver: This project uses Answer Set Programming. You must install clingo to run the symbolic solver.

## 🚀 Usage
### 1. Running AS-NMRer (Main Framework)
The main inference pipeline (Abstraction → Step-wise Search → Solving) is located in Code/AS_NMRer_with_DL_for_LogicBench/AS-NMRer_for_LogicBench.

### 2. Running Baselines
To run the baseline models for comparison:
* LLM2ASP: Run the scripts located in LLASP_for_LogicBench.
* Prompting (Zero/Few-Shot): Run the scripts located in Zero_Few_Shot_for_LogicBench.
* Fine-tuning: Use the scripts in Fine_Tuned_Models. We utilize Unsloth for efficient LoRA fine-tuning .

## 📊 Datasets
We provide the four benchmarks used in our experiments in the Dataset/ directory:

1. LogicBench: A dataset evaluating robustness against linguistic noise in Binary Question Answering (BQA) tasks. It includes patterns like DRD, DRI, DRS, etc.

2. LogicEval (Multi-LogiEval): Assesses multi-step reasoning capabilities across increasing reasoning depths (from Depth 1 to Depth 5).

3. LogicNMR: A synthetic benchmark for probing non-monotonic reasoning in dynamic knowledge bases, with updates ranging from U=1 to U=5.

4. MultiLogicNMR: Evaluates reasoning in complex scenarios with multiple valid answer sets, supporting both Credulous and Skeptical reasoning modes.


  
