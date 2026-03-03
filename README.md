# 📘 Advanced Machine Learning – Mid-Semester Examination

**Student Name:** Vishesh
**Enrolment No** 230129 
**Course:** Advanced Machine Learning  
**Exam:** Mid-Semester Examination  

**Selected Paper (Part A):**  
**“Analysis of SVM with Indefinite Kernels” – NeurIPS 2009**

---

# 📑 Overview

This repository contains my complete submission for the Advanced Machine Learning Mid-Semester Examination.

The exam consists of four parts:

| Part | Description | Weightage |
|------|------------|-----------|
| A | Research Paper Selection | 5% |
| B | Reproduction & Experiments | 30% |
| C | Explanation & Reasoning | 5% |
| D | Case Study Questions | 60% |

- Parts A & B: Open-book  
- Parts C & D: Proctored  

---

# 📌 Part A – Research Paper Selection

**Title:** Analysis of SVM with Indefinite Kernels  
**Venue:** NeurIPS 2009 (CORE A*)  
**Unit:** Support Vector Machines  

## Why This Paper?

I selected this paper because it extends classical Support Vector Machine theory to cases where kernel matrices are indefinite (not positive semidefinite). This is important in practice when similarity functions do not satisfy Mercer’s condition.

The paper satisfies all required constraints:

- Published within the allowed time window  
- Appears in a top-tier (A*) venue  
- Primary contribution is classical SVM theory  
- Not deep learning–based  
- Not a survey or benchmarking paper  
- Introduces a core theoretical idea  

---

# 🔬 Part B – Reproduction & Experiments

## Objective

To experimentally demonstrate:

- Behavior of SVM with indefinite kernels  
- Effect of negative eigenvalues  
- Impact of spectral correction  

## Implementation Plan

1. Construct an indefinite kernel matrix.
2. Compute eigenvalues and verify negative values.
3. Apply spectral correction (eigenvalue clipping).
4. Train SVM using:
   - Corrected kernel
   - Standard PSD kernel (baseline)
5. Compare accuracy and stability.

## Tools Used

- Python
- NumPy
- scikit-learn (`SVC` with precomputed kernel)
- Matplotlib (optional)

All experiments are CPU-based and reproducible on a standard laptop.

## Key Observations

- Indefinite kernels produce negative eigenvalues.
- Spectral correction restores positive semidefiniteness.
- SVM training stabilizes after correction.
- Performance depends on degree of indefiniteness.

---

# 🧠 Part C – Explanation & Reasoning (Proctored)

In the proctored section, I will explain:

- Why SVM requires PSD kernels.
- What happens when kernels are indefinite.
- Why eigenvalue clipping works.
- Convex vs non-convex optimization behavior.
- Design choices and parameter settings.

I understand every implementation decision and experimental result.

---

# 📊 Part D – Case Study Questions

Part D will assess understanding of:

- Time Series (ARIMA, stationarity, assumptions)
- Support Vector Machines (margin, duality, kernels)
- Gaussian Mixture Models (EM algorithm, likelihood, convergence)

Preparation includes lecture notes, lab exercises, and conceptual revision.

---


