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
│       ├── Ablation_Anaysis/            # Scripts for ablation studies (e.g., w/o Abstraction, w/o Search) [cite: 730]
│       ├── AS-NMRer_for_LogicBench/     # Core implementation of the AS-NMRer framework [cite: 163]
│       ├── Fine_Tuned_Models/           # Code for Expert Iteration and SFT using Unsloth/LoRA [cite: 1199]
│       ├── LLASP_for_LogicBench/        # Implementation of the LLM2ASP baseline 
│       └── Zero_Few_Shot_for_LogicBench/# Scripts for Zero-shot and Few-shot prompting baselines 
│
└── Dataset/
    ├── LogicBench/       # LogicBench (BQA task) dataset 
    ├── LogicEval/        # Multi-LogiEval dataset (Reasoning depths 1-5) 
    ├── LogicNMR/         # LogicNMR synthetic dataset (Dynamic updates) 
    └── MultiLogicNMR/    # MultiLogicNMR dataset (Multi-extension scenarios)
  
### Prerequisites
