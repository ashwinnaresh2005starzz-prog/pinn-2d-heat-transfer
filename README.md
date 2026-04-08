# Physics-Guided Neural Network for 2D Heat Transfer in Homogeneous Materials

A portfolio-ready academic project that studies transient two-dimensional heat transfer using a physics-guided neural network framework on two domains: a solid square plate and a square plate with a central void.

## Overview

This project explores whether a neural network can learn the evolution of temperature over space and time while remaining guided by the physical structure of the heat-transfer problem. The study uses ANSYS-generated datasets and evaluates predictions using convergence analysis, scatter plots, temperature-field visualizations, and absolute error maps.

## Problem Statement

Transient heat conduction is important in thermal engineering, materials analysis, and electronics cooling. Traditional numerical methods such as finite element analysis require meshing, repeated solves, and careful geometry handling. This project investigates a neural surrogate approach for predicting temperature fields directly from coordinates and time.

## Domains Studied

### 1. Solid Square Plate
- Domain size: **0.02 m × 0.02 m**
- Coordinate range: **x, y in [-0.01, 0.01]**

### 2. Square Plate with a Central Void
- Outer domain size: **0.03 m × 0.03 m**
- Outer coordinate range: **x, y in [-0.015, 0.015]**
- Central void size: **0.01 m × 0.01 m**
- Void coordinate range: **x, y in [-0.005, 0.005]**

## Boundary Conditions

- West boundary: **500 K**
- East boundary: **0 K**
- Top and bottom boundaries: treated as adiabatic in the project description

## Project Workflow

1. Generate thermal datasets using ANSYS
2. Export node-wise temperature data over time
3. Preprocess spatial and temporal inputs
4. Train separate neural models for each domain
5. Evaluate predictions against ANSYS reference data
6. Visualize learning behaviour and temperature distributions

## Repository Structure

```text
pinn-2d-heat-transfer/
├── notebooks/
│   ├── solid_square_pinn.ipynb
│   └── square_with_void_pinn.ipynb
├── data/
│   ├── square.xlsx
│   └── void.xlsx
├── reports/
│   ├── final_report.docx
│   └── project_paper.pdf
├── results/
│   ├── convergence/
│   │   ├── solid_square_loss.png
│   │   └── square_with_void_loss.png
│   ├── solid_square/
│   │   ├── temp_error_1s.png
│   │   ├── temp_error_5s.png
│   │   ├── temp_error_10s.png
│   │   ├── temp_error_15s.png
│   │   └── predicted_vs_actual.png
│   └── square_with_void/
│       ├── temp_error_1s.png
│       ├── temp_error_5s.png
│       ├── temp_error_10s.png
│       ├── temp_error_15s.png
│       └── predicted_vs_actual.png
├── assets/
│   ├── solid_square_mesh.jpeg
│   └── square_with_void_mesh.jpeg
├── docs/
│   └── project_overview.md
├── requirements.txt
├── LICENSE
├── .gitignore
└── README.md