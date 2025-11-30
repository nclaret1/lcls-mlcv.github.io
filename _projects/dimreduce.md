---
layout: projects
title: Low-Rank + Sparse Decomposition for High-Throughput Crystallography
description: Fast alternating-projections methods for separating background scattering and Bragg peaks in LCLS-II diffraction data
img: assets/img/projects/dimreduce.jpg   # ← replace with your actual image
importance: 1
category: Computational Imaging
related_publications: true
---

### Project Goal
The transition to LCLS-II introduces a drastic increase in data throughput for X-ray crystallography, raising peak ingest rates from **3.84 GB/s to nearly 280 GB/s**. To address the resulting computational demands, this project aims to develop fast and robust dimensionality-reduction methods that retain the intrinsic structure of diffraction patterns while operating under severe memory and latency constraints. The project focuses initially on variants of alternating-projection algorithms equipped with denoising operators and physically motivated constraints, enabling real-time separation of low-rank background scattering from sparse, high-intensity features corresponding to Bragg peaks.

{% include figure.liquid 
     path="assets/img/projects/dimreduce.jpg"   # ← replace with your actual image
     title="Low-Rank + Sparse Decomposition for High-Throughput Crystallography"
     class="img-fluid rounded z-depth-1"
     caption="This project develops alternating-projections–based low-rank + sparse decomposition methods for separating diffuse background from localized Bragg peaks in crystallographic diffraction patterns. The first stage incorporates denoising operators and positivity constraints, while subsequent geometry-aware extensions introduce reciprocal-space structure, detector geometry, and symmetry constraints directly into the decomposition framework."
%}

Crystallographic diffraction patterns are inherently structured objects residing in reciprocal space, encoding the Fourier transform of the electron density and shaped by crystal lattice symmetries and space-group constraints. These patterns comprise a smooth background together with sparse Bragg peaks whose intensities are strictly nonnegative and whose spatial organization reflects the underlying lattice. For this setting, decompositions that naturally split low-rank background components from sparse, localized peaks—such as robust PCA—are particularly attractive. Recent advances in manifold-based algorithms and randomized techniques further accelerate these decompositions, making them suitable for high-throughput environments. The first stage of this project focuses on developing an alternating-projections–style low-rank + sparse algorithm tailored to crystallographic data streams, incorporating denoising operators and positivity constraints on the sparse component to reflect the physical interpretation of peak intensities, and balancing fidelity with the computational demands imposed by LCLS-II acquisition rates.

### Synthetic Data Visualization

{% include figure.liquid 
    path="assets/img/projects/dimreduce/noiseless_image.png"
    title="Ground-truth Sparse Component"
    class="img-fluid rounded z-depth-1"
    caption="(a) Ground-truth sparse Bragg peaks $\\mathbf{S}_{\\text{true}}$."
%}

{% include figure.liquid 
    path="assets/img/projects/dimreduce/true_low_rank.png"
    title="Ground-truth Low-Rank Component"
    class="img-fluid rounded z-depth-1"
    caption="(b) Smooth low-rank background $\\mathbf{L}_{\\text{true}}$."
%}

{% include figure.liquid 
    path="assets/img/projects/dimreduce/corrupted_image.png"
    title="Corrupted Data"
    class="img-fluid rounded z-depth-1"
    caption="(c) Final data matrix $\\mathbf{D} = \\mathbf{L}_{\\text{true}} + \\mathbf{S}_{\\text{true}}$."
%}


### RPCA Recovery Results

{% include figure.liquid 
    path="assets/img/projects/dimreduce/example_2.png"
    title="RPCA Recovery Across Different Rank Hyperparameters"
    class="img-fluid rounded z-depth-1"
    caption="Visual results of applying the RPCA algorithm to $\\mathbf{D}$. Columns correspond to different values of the rank parameter (`n_components`). Row 1: corrupted input. Row 2: recovered low-rank component $\\hat{\\mathbf{L}}$. Row 3: recovered sparse component $\\hat{\\mathbf{S}}$. Row 4: difference $\\mathbf{S}_{\\text{true}} - \\hat{\\mathbf{S}}$."
%}


Building on this foundation, the second stage of the project extends the same decomposition algorithm to incorporate reciprocal-space structure, detector geometry, and symmetry constraints directly into its update rules. This requires adapting projection steps, thresholding operators, and distance metrics to respect the non-Euclidean geometry and group-theoretic invariances inherent to crystallographic data. Implemented within a large-scale optimization framework, the resulting geometry-aware version of the algorithm aims to preserve physically meaningful relationships among Bragg peaks and background features while remaining compatible with high-throughput operation.
