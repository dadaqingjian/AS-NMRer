# AS-NMRer: Improving Autoformalization for Non-monotonic Reasoning via Abstraction, Search, and Fine-tuning

This repository contains the source code, benchmark datasets, and human-evaluation annotations for the paper **"AS-NMRer: Improving Autoformalization for Non-monotonic Reasoning via Abstraction, Search, and Fine-tuning"**.

**Anonymous submission.** This repository is provided for anonymous double-blind review.

## Overview

AS-NMRer is a neuro-symbolic framework for natural-language non-monotonic reasoning (NMR). Its inference pipeline consists of three stages.

1. **Abstraction** selects and simplifies query-relevant facts and default rules from the supplied context.
2. **Step-wise Formalization** translates abstracted sentences into Answer Set Programming (ASP) fragments through default-logic representations. A verification-guided Best-of-N search combines solver-based syntax checks with LLM-based semantic scoring to select candidate fragments.
3. **Symbolic Solving** executes the generated ASP program with clingo to determine the query answer, supporting skeptical and credulous reasoning when multiple answer sets arise.

AS-NMRer also supports **Expert Iteration**, which fine-tunes open-source backbones on training instances selected by agreement between solver outputs and gold answers. This selection criterion does not guarantee that every intermediate abstraction or formalization is semantically correct.

## Repository Structure

The repository contains two main directories, `Code` and `Dataset`.

```text
.
├── Code/
│   └── AS_NMRer_with_DL_for_LogicBench/
│       ├── Ablation_Anaysis/             # Component ablation studies
│       ├── AS-NMRer_for_LogicBench/      # Main AS-NMRer inference pipeline
│       ├── Fine_Tuned_Models/           # Expert iteration and supervised fine-tuning
│       ├── LLASP_for_LogicBench/        # LLM2ASP baseline
│       └── Zero_Few_Shot_for_LogicBench/ # Zero-shot and few-shot prompting baselines
│
└── Dataset/
    ├── Examples of Human Validation of the Semantic Verifier/
    │   └── Semantic_Verifier_Examples.json
    ├── LogicBench/                      # LogicBench BQA NMR subsets
    ├── LogicEval/                       # Multi-LogiEval NMR subsets, depths 1–5
    ├── LogicNMR/                        # Sequential knowledge-base updates
    └── MultiLogicNMR/                   # Multiple-answer-set reasoning
```

The `LogicEval` directory contains the Multi-LogiEval data.

## Prerequisites

- Python 3.11.
- clingo for executing ASP programs.
- Access to the model backend required by the selected inference script.
- Unsloth and a compatible CUDA environment for the fine-tuning experiments.

Configure model access, credentials, and dataset paths according to the selected script. Do not commit API keys or other private credentials.

## Usage

### Running AS-NMRer

The main inference pipeline is located in:

```text
Code/AS_NMRer_with_DL_for_LogicBench/AS-NMRer_for_LogicBench/
```

The pipeline performs abstraction, verification-guided step-wise formalization, and symbolic solving.

### Running Baselines

Baseline implementations are located under:

```text
Code/AS_NMRer_with_DL_for_LogicBench/
```

- **LLM2ASP** is implemented in `LLASP_for_LogicBench/`.
- **Zero-shot and few-shot prompting** are implemented in `Zero_Few_Shot_for_LogicBench/`.
- **Fine-tuning and expert iteration** scripts are provided in `Fine_Tuned_Models/`.

### Running Ablation Studies

Component ablation scripts are located in:

```text
Code/AS_NMRer_with_DL_for_LogicBench/Ablation_Anaysis/
```

These scripts examine the contributions of abstraction, step-wise search, and verification components.

## Benchmark Datasets

The `Dataset` directory contains the four benchmarks used in the paper.

1. **LogicBench** evaluates the NMR subsets of the Binary Question Answering (BQA) task across eight reasoning patterns, including DRD, DRI, DRO, DRS, RE1–3, and RAP.

2. **Multi-LogiEval** evaluates multi-step logical reasoning across reasoning depths from one to five. Its data are stored in `Dataset/LogicEval/`.

3. **LogicNMR** evaluates non-monotonic reasoning under sequential knowledge-base updates. The variable `U` denotes the number of updates, ranging from 1 to 5.

4. **MultiLogicNMR** evaluates non-monotonic reasoning with multiple answer sets under skeptical and credulous reasoning modes. Skeptical reasoning requires support in all answer sets, whereas credulous reasoning requires support in at least one.

## Human Evaluation of the Semantic Verifier

### Data Location

Sentence–ASP pairs and their annotations are provided in:

```text
Dataset/Examples of Human Validation of the Semantic Verifier/
Semantic_Verifier_Examples.json
```

These records support inspection of agreement and disagreement between semantic-verifier scores and human judgments.

Each record contains a natural-language sentence, its candidate ASP fragment, the verifier score, the sampling stratum, and human-annotation fields.

