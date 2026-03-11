# 📘 Advanced Machine Learning – Mid-Semester Examination

**Student Name:** Pranay Vishwakarma  
**Roll Number:** 230083  
**Course:** Advanced Machine Learning  
**Exam:** Mid-Semester Examination  

**Selected Paper (Part A):**  
**"Kernel Latent SVM for Visual Recognition" – NeurIPS 2012**

---

## 📑 Overview

This repository contains my complete submission for the Advanced Machine Learning Mid-Semester Examination.

| Part | Description | Weightage |
|------|------------|-----------|
| A | Research Paper Selection | 5% |
| B | Reproduction & Experiments | 30% |
| C | Explanation & Reasoning | 5% |
| D | Case Study Questions | 60% |

---

## 📌 Part A – Research Paper Selection

**Title:** Kernel Latent SVM for Visual Recognition  
**Authors:** Wenze Hu, Yongfeng Zhu, Yang Wang, Jae-On Lee, Yiming Ying  
**Venue:** NeurIPS 2012 (CORE A*)  
**Unit:** Support Vector Machines / Kernel Methods  

### Why This Paper?

This paper proposes Kernel Latent SVM (KLSVM), a framework combining latent SVMs with kernel methods for visual recognition. It addresses the limitation of standard latent SVMs (linear models) by introducing a kernelized dual formulation that handles latent variables in a non-parametric way.

---

## 🔬 Part B – Reproduction & Experiments

### Structure

```
partB/
├── task_1_1.ipynb          # Q1: Core Contribution / Architecture
├── task_1_2.ipynb          # Q1: Key Assumptions
├── task_1_3.ipynb          # Q1: What the Paper Claims to Improve
├── task_2_1.ipynb          # Q2: Dataset Selection and Setup
├── task_2_2.ipynb          # Q2: Reproduction of Contribution
├── task_2_3.ipynb          # Q2: Result, Comparison, Reproducibility
├── task_3_1.ipynb          # Q3: Two-Component Ablation
├── task_3_2.ipynb          # Q3: Failure Mode
├── report.md               # Q4: Written Report (markdown)
├── llm_task_1_1.json       # LLM Usage Disclosures
├── ...                     # (10 JSON files total)
├── requirements.txt        # Python dependencies
├── data/                   # Dataset files
│   └── README.md           # Dataset documentation
└── results/                # Plots and figures
```

### Key Experiments

- **Reproduction:** KLSVM with latent subcategories on CIFAR-10 (Sec 4.2 of paper)
- **Ablation 1:** Remove latent subcategories (single component)
- **Ablation 2:** Replace HIK kernel with linear kernel
- **Failure Mode:** Highly overlapping class distributions

All experiments are CPU-based and reproducible.
