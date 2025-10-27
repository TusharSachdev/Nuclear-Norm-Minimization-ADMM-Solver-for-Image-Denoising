# 🖼️ Nuclear Norm Minimization & ADMM Solver for Image Denoising

## 🧭 Project Overview

This project demonstrates **convex optimization techniques** applied to **image denoising** using nuclear norm minimization. Two approaches are explored:

1. **CVXPY Solver** – general-purpose convex optimization solver.  
2. **ADMM (Alternating Direction Method of Multipliers)** – a scalable **first-order algorithm** for large-scale matrix optimization.

The project bridges **optimization theory, convex analysis, and statistical learning**, aligning with research interests in **large-scale convex optimization, decomposition methods, and first/second-order methods**.

---

## 🎯 Objectives

- Implement image denoising via nuclear norm minimization.
- Compare general-purpose solvers (CVXPY) with **ADMM**.
- Evaluate performance with **PSNR metrics**.
- Visualize original, noisy, and denoised images.
- Highlight connections to **optimization, matrix recovery, and statistical learning**.

---

## ⚙️ Methodology / Work Performed

1. **Data Preparation**
   - Loaded grayscale images and added Gaussian noise to simulate corrupted observations.
2. **Nuclear Norm Minimization via CVXPY**
   - Solved the problem:
     \[
     \min_X \|X\|_* + \frac{\lambda}{2} \|X - M\|_F^2
     \]
     where \(M\) is the noisy image and \(\|\cdot\|_*\) is the nuclear norm.
   - Solver: **SCS v3.2.9**, sparse-direct linear system, max 100,000 iterations.
3. **First-Order ADMM Solver**
   - X-update: quadratic minimization  
   - Z-update: singular value thresholding  
   - U-update: dual ascent  
   - Iterated until convergence.
4. **Performance Evaluation**
   - Calculated **PSNR (Peak Signal-to-Noise Ratio)** for different λ values.
   - Visualized original, noisy, CVXPY-denoised, and ADMM-denoised images.

---

## 📊 Results

**CVXPY Solver Logs & Performance:**

- Problem: 16,384 variables, 0 constraints  
- Compilation time: 0.481 sec  
- Solver time: 5.398 sec  
- Optimal objective: 243.693  

**PSNR Evaluation:**

| Lambda (λ) | PSNR (dB) |
|------------|------------|
| 0.1        | 12.87      |
| 0.5        | 19.87      |
| 1.0        | 21.99      |
| 5.0        | 20.79      |

- PSNR (Noisy): 19.97 dB  
- PSNR (After Denoising, λ=1.0): 21.99 dB  

**Visualization:**  
Side-by-side comparison of:

1. Original image  
2. Noisy image  
3. CVXPY-denoised image  
4. ADMM-denoised image

**ADMM Performance:**

- Scales efficiently for **large matrices**.  
- Converges with comparable PSNR to CVXPY but faster for larger datasets.  

---

## 🧠 Discussion & Inference

### ADMM vs CVXPY Solver

- **ADMM** is a **first-order method** suitable for **large-scale problems**; CVXPY general solvers are slower for large matrices.
- ADMM splits the optimization into **subproblems**:
  - X-update: quadratic  
  - Z-update: singular value thresholding  
  - U-update: dual ascent  
- Demonstrates **scalable convex optimization** bridging theory and practical matrix recovery.
- Aligns with research on **large-scale convex optimization, decomposition methods, and first/second-order methods**.

**Inference:**

- Nuclear norm minimization via ADMM effectively denoises images with comparable PSNR to CVXPY.  
- Optimal λ selection is critical for balancing noise removal and detail preservation.  
- Large-scale convex problems benefit from **first-order methods like ADMM**, especially in applications like **matrix completion, neuroimaging, and network data analysis**.

**Potential Extensions:**

1. **Online/Streaming ADMM** for real-time recovery.  
2. **Matrix completion** for partially observed data, linking with **statistics and ML applications**.  
3. **Integration with probabilistic models** (Bayesian low-rank priors) for **neuroimaging or network analysis**.

---

## ✅ Outcome

This project successfully:

- Implements **image denoising via nuclear norm minimization** (CVXPY).  
- Develops a **first-order ADMM solver** for large-scale convex optimization.  
- Evaluates performance via **PSNR metrics** and **visualizations**.  
- Bridges **optimization theory, convex analysis, statistical learning, and applications**.

---

## 📚 References

- Boyd, S., Parikh, N., Chu, E., Peleato, B., & Eckstein, J. (2011). *Distributed Optimization and Statistical Learning via the Alternating Direction Method of Multipliers*. Foundations and Trends in Machine Learning.  
- Recht, B., Fazel, M., & Parrilo, P. A. (2010). *Guaranteed minimum-rank solutions of linear matrix equations via nuclear norm minimization*. SIAM Review.  
- CVXPY Documentation: https://www.cvxpy.org/
