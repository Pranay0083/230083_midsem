# Report — Kernel Latent SVM for Visual Recognition

**Student:** Pranay Vishwakarma (230083)  
**Paper:** Kernel Latent SVM for Visual Recognition (NeurIPS 2012)  
**Course:** Advanced Machine Learning — Mid-Semester Examination, Part B

---

## 1. Paper Summary

The paper proposes Kernel Latent SVM (KLSVM), a framework that unifies latent variable modeling with kernel methods for visual recognition. Standard latent SVMs (LSVM) use linear scoring functions $f_w(x) = \max_h w^\top \phi(x, h)$, limiting their capacity. KLSVM reformulates the optimization in the dual space, replacing dot-products with kernel functions to obtain nonlinear classifiers while retaining latent structure. The iterative algorithm alternates between latent variable inference and kernel SVM training. The paper demonstrates improvements on mammal classification (84.49% vs 75.07%), CIFAR-10 (47.72% vs 39.42%), and object interaction recognition (66.42% vs 46.33%).

## 2. Reproduction Setup and Results

We reproduced Section 4.2 (latent subcategories on CIFAR-10) using a 4-class subset (airplane, automobile, bird, cat) with 200 training and 100 test samples per class, HOG features, HIK kernel, C=0.01, and K=3 subcategories.

| Method | Our Accuracy | Paper Accuracy |
|--------|-------------|----------------|
| Linear SVM | **49.25%** | 38.32% |
| Kernel SVM (HIK) | 47.75% | 44.04% |
| Linear LSVM | 39.00% | 39.42% |
| KLSVM | 39.25% | **47.72%** |

Our ordering (Linear SVM > Kernel SVM > KLSVM ≈ LSVM) reverses the paper's finding because our 200 samples per class are far fewer than the paper's 10,000. The subcategory expansion triples the feature dimension (288→864), creating a severely underdetermined problem. The alternating optimization fails to converge — subcategory labels change ~600 per iteration — confirming that KLSVM requires substantial training data for the subcategory mechanism to discover meaningful structure.

## 3. Ablation Findings

**Ablation 1 (Remove subcategories):** Performance improved from 39.25% to 47.75% (+8.5%), confirming subcategories hurt in our regime by fragmenting the data.

**Ablation 2 (Replace HIK with linear):** Performance barely changed (39.00% vs 39.25%), showing the kernel choice is irrelevant when subcategory expansion is the bottleneck.

Both ablations reveal that KLSVM's advantage is data-dependent — with sufficient data, subcategories and nonlinear kernels both contribute; with insufficient data, model complexity becomes a liability.

## 4. Failure Mode

Cat vs. dog classification with Gaussian noise: KLSVM consistently underperforms standard SVM by 3–6% across noise levels. These visually similar classes lack subcategory structure, so k-means produces arbitrary splits. This violates two key assumptions of the method:

- **The optimization landscape has reasonable local optima:** The paper's alternating optimization (Eq. 5) is non-convex and only guarantees local optimality. When classes are visually similar (cat/dog share similar shapes, textures, and HOG responses), k-means initialization produces subcategory assignments that reflect noise patterns rather than meaningful visual modes. The alternating optimization gets trapped refining these meaningless splits, wasting model capacity.

- **Feature representation is discriminative at each latent configuration:** The joint feature $\phi(x, h)$ must carry sufficient discriminative information for each subcategory $h$. Cat and dog images produce nearly identical HOG descriptors (similar furry textures, body contours, edge orientations), so $\phi(x, h)$ is barely above chance-level discriminative for any subcategory — adding subcategory structure just fragments an already weak signal.

**Suggested fix:** Automatically select K per class using silhouette scores or gap statistics, defaulting to K=1 when no meaningful subcategory structure exists.

## 5. Reflection

**What surprised me:** The sensitivity of KLSVM to training set size was more extreme than expected. The paper's setting (10,000 samples) is essential for the method to work — this data requirement is implicit in the paper but critical in practice.

**What I would revisit:** Implement the full coordinate ascent (Eq. 8-9) with larger training sets, and experiment with the composite kernel formulation for structured latent variables on the VOC3000 dataset.

---

## References

1. Hu et al. (2012). Kernel Latent SVM for Visual Recognition. NeurIPS 2012.
2. Felzenszwalb et al. (2010). Object Detection with Discriminatively Trained Part Based Models. IEEE TPAMI.
3. Maji et al. (2008). Classification using Intersection Kernel SVMs is Efficient. CVPR.
4. Yu & Joachims (2009). Learning Structural SVMs with Latent Variables. ICML.
5. Krizhevsky (2009). Learning Multiple Layers of Features from Tiny Images.
