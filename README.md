# Physics-Guided Neural Network for Transient 2D Heat Transfer in Homogeneous Materials

A portfolio-ready machine learning and scientific computing project that models transient two-dimensional heat transfer in both regular and complex geometries using a physics-guided neural network framework.

This work studies temperature evolution in:
- a **solid square plate**
- a **square plate with a central void**

The project combines **ANSYS-generated simulation data**, **deep learning**, and **physics-aware loss formulation** to learn temperature fields over space and time. It is designed as both an academic thermal-modelling study and a practical demonstration of coordinate-based neural surrogate modelling.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Why This Project Matters](#why-this-project-matters)
- [Objectives](#objectives)
- [Problem Formulation](#problem-formulation)
- [Domains Studied](#domains-studied)
- [Boundary Conditions](#boundary-conditions)
- [Dataset Description](#dataset-description)
- [Methodology](#methodology)
- [Model Architecture](#model-architecture)
- [Training Strategy](#training-strategy)
- [Repository Structure](#repository-structure)
- [Results](#results)
- [Key Observations](#key-observations)
- [Technical Stack](#technical-stack)
- [How to Run the Project](#how-to-run-the-project)
- [Project Deliverables](#project-deliverables)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Professional Relevance](#professional-relevance)
- [Authors](#authors)

---

## Project Overview

Transient heat conduction is a core problem in thermal engineering, simulation, and scientific computing. In many real-world systems, temperature is not only a function of position but also changes over time. Traditional numerical approaches such as finite element analysis are highly effective, but they often require mesh generation, repeated numerical solves, and careful handling of complex geometries.

This project explores an alternative approach using a **physics-guided neural network** that learns temperature directly from spatial coordinates and time. The model is trained on simulation data exported from ANSYS and evaluated on two domain types:
1. a simple conductive square plate
2. a square plate with a central geometric exclusion (void)

The goal is to examine whether a neural model can capture global thermal behaviour, transient evolution, and geometry-dependent heat-flow patterns while remaining guided by the underlying physical structure of the problem.

---

## Why This Project Matters

This project is relevant because it sits at the intersection of:
- **machine learning**
- **scientific computing**
- **thermal simulation**
- **surrogate modelling**
- **physics-aware AI**

It demonstrates the ability to:
- work with simulation-generated engineering datasets
- preprocess spatial-temporal data for neural learning
- design coordinate-based prediction models
- compare model behaviour across multiple geometries
- communicate technical results through plots, reports, and structured documentation

For portfolio and job purposes, this project shows applied experience in building machine-learning solutions for physics-based problems rather than only standard classification or regression tasks.

---

## Objectives

The major objectives of this project are:

- To model transient 2D heat transfer using a neural-network-based surrogate framework
- To study how geometry affects temperature prediction performance
- To compare behaviour across a regular conductive domain and a complex domain with an internal void
- To evaluate prediction quality using convergence plots, scatter plots, temperature fields, and error maps
- To demonstrate a structured workflow from simulation data to trained model to engineering interpretation

---

## Problem Formulation

The thermal process is based on **transient two-dimensional heat conduction**, where temperature depends on:
- spatial location: **x, y**
- time: **t**

The learning task is:

\[
(x, y, t) \rightarrow T
\]

where:
- \(x, y, t\) are the inputs
- \(T\) is the predicted temperature in Kelvin

The project is based on the transient heat equation:

\[
\frac{\partial T}{\partial t} = \alpha \left( \frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} \right)
\]

where:
- \(T\) = temperature
- \(\alpha\) = thermal diffusivity

This equation provides the physical structure that motivates the learning framework.

---

## Domains Studied

### 1. Solid Square Plate

- Domain size: **0.02 m × 0.02 m**
- Coordinate range: **x, y ∈ [-0.01, 0.01]**

This domain represents a continuous conductive region with no internal interruptions. It serves as the simpler benchmark case.

### 2. Square Plate with a Central Void

- Outer domain size: **0.03 m × 0.03 m**
- Outer coordinate range: **x, y ∈ [-0.015, 0.015]**
- Central void size: **0.01 m × 0.01 m**
- Void coordinate range: **x, y ∈ [-0.005, 0.005]**

This domain introduces geometry-driven complexity. Heat cannot pass through the central void, so the thermal field must redistribute around it.

---

## Boundary Conditions

The thermal setup used in the project follows the problem description below:

- **West boundary:** 500 K
- **East boundary:** 0 K
- **North boundary:** adiabatic
- **South boundary:** adiabatic

This creates a left-to-right thermal gradient across the plate and drives the transient conduction behaviour over time.

---

## Dataset Description

The datasets used in this project were generated using **ANSYS simulations** and exported into Excel format.

### Files
- `data/square.xlsx`
- `data/void.xlsx`

### Dataset Structure

Each row represents one node or spatial point at one time instant and contains:
- node number
- x-coordinate
- y-coordinate
- time
- temperature

### Dataset Sizes
- **Solid square dataset:** 7,695 points
- **Square-with-void dataset:** 3,600 points

### Time Range
- **1 s to 15 s**

### Preprocessing Steps
- loading Excel files into Python
- selecting input and output variables
- removing inconsistent or missing entries
- normalizing spatial and temporal inputs
- applying train-test split
- handling geometry-aware masking for the void domain during visualization

The output temperature values are kept in **Kelvin** for physical interpretability.

---

## Methodology

The project uses a coordinate-based neural approach in which the network receives \((x, y, t)\) and predicts temperature \(T\).

The methodology includes:
1. generating transient thermal data in ANSYS
2. exporting the simulation results
3. preprocessing spatial and temporal coordinates
4. training neural models on both domains
5. monitoring convergence during training
6. evaluating predictions visually and numerically

The framework is called **physics-guided** because the training is designed around the physical structure of the heat-transfer problem and uses a combined learning objective motivated by both data consistency and equation-based behaviour.

---

## Model Architecture

The predictive model is a fully connected feedforward neural network.

### Architecture
- Input layer: **3 features** \((x, y, t)\)
- Hidden layers:
  - 64 neurons
  - 32 neurons
  - 16 neurons
  - 8 neurons
- Output layer: **1 neuron** \((T)\)

### Activation Function
- **ReLU**

### Why this architecture?
This architecture provides a balance between:
- expressive power
- training stability
- manageable computational cost

Because the task is coordinate-based and the output is a continuous scalar field, a fully connected network is a reasonable approximation framework for this problem.

---

## Training Strategy

### Optimizer
- **Adam**

### Learning Rate
- **0.001**

### Epochs
- **3000**

### Data Split
- **70% training**
- **30% testing**

### Loss Design
The model training combines:
- **data consistency**
- **physics-guided structure**

The idea is to encourage the model not only to fit ANSYS temperature samples, but also to learn behaviour aligned with the thermal problem.

### Evaluation Strategy
The trained models are analysed using:
- convergence curves
- predicted vs actual scatter plots
- temperature distribution plots
- absolute error maps
- cross-domain interpretation

The temperature and error plots are examined at:
- **1 s**
- **5 s**
- **10 s**
- **15 s**

---

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