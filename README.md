
# Phase-Blind GAT: Adversarial Vulnerability in Complex-Valued GNN Beamformers

## Overview

This repository contains a proof-of-concept implementation 
demonstrating adversarial vulnerability in complex-valued Graph 
Attention Network (GAT) beamformers for multi-user MISO (MU-MISO) 
wireless networks.

The architecture under study is based on Reference [57] in:

> Lu, Y., Zhang, S., Liu, C., Zhang, R., Ai, B., Niyato, D., Ni, W., 
> Wang, X., & Jamalipour, A. (2025). Agentic Graph Neural Networks 
> for Wireless Communications and Networking Towards Edge General 
> Intelligence: A Survey. arXiv:2508.08620

## Key Findings

**Finding 1: Adversarial Vulnerability**
A complex FGSM attack on CSI input achieves 70.3% sum rate 
degradation at perturbation strength ε=0.05 — smaller than 
typical channel estimation error in real deployments.

| Condition | Sum Rate |
|-----------|----------|
| Clean baseline | 23.95 bits/s/Hz |
| ε = 0.05 (attack) | 7.12 bits/s/Hz |
| Degradation | 70.3% |

**Finding 2: Phase Blindness**
The trained model fails to learn global phase equivariance 
despite SINR being phase-invariant by physical law.

| Metric | Value |
|--------|-------|
| Equivariance score (ideal) | 0.0 |
| Equivariance score (ours) | 1.2901 |

Standard GAT with LeakyReLU activations cannot be made 
phase-equivariant through loss regularization alone. 
The architecture requires equivariant-by-design layers — 
identified as an open problem in Section VII-B of the survey.

## Experimental Setup

- **Architecture:** Complex-valued GAT with residual connections
- **Dataset:** DeepMIMO O1 scenario, 28 GHz, 250,000 user locations
- **BS antennas:** 64-element ULA
- **Users per graph:** K = 8
- **Training:** Unsupervised Lagrangian loss, 2000 steps
- **Attack:** Complex FGSM on CSI input

## Repository Structure


phase-blind-gat/
  complex_gat_fgsm_deepmimo.ipynb   ← main notebook
  figures/
    attack_curve.png                 ← Figure 1: robustness curve
    convergence_curves.png           ← Figure 2: training convergence
    pe_training_curves.png           ← Figure 3: PE regularization
  README.md


## Status

Preliminary implementation. Results obtained on a single run 
without fixed random seed. Reproducible version in progress.

## Citation

If referencing this work, please also cite the survey:

bibtex
@article{lu2025agentic,
  title={Agentic Graph Neural Networks for Wireless Communications 
         and Networking Towards Edge General Intelligence: A Survey},
  author={Lu, Yang and Zhang, Shengli and Liu, Chang and Zhang, 
          Ruichen and Ai, Bo and Niyato, Dusit and Ni, Wei and 
          Wang, Xianbin and Jamalipour, Abbas},
  journal={arXiv preprint arXiv:2508.08620},
  year={2025}
}
```
```

---
