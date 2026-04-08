# Physics-Guided Neural Network for Transient 2D Heat Transfer in Homogeneous Materials

A portfolio-ready machine learning and scientific computing project that models transient two-dimensional heat transfer in both regular and complex geometries using a physics-guided neural network framework.

This project studies temperature evolution in:
- a **solid square plate**
- a **square plate with a central void**

It combines **ANSYS-generated simulation data**, **deep learning**, and **physics-aware modelling** to learn temperature fields over space and time. The work is presented as both an academic thermal-modelling study and a practical demonstration of coordinate-based neural surrogate modelling.

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
- [Technical Stack](#technical-stack)
- [Installation and Usage](#installation-and-usage)
- [Results Summary](#results-summary)
- [Key Observations](#key-observations)
- [Project Deliverables](#project-deliverables)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Professional Relevance](#professional-relevance)
- [Acknowledgement](#acknowledgement)
- [Keywords](#keywords)
- [Authors](#authors)
- [License](#license)

---

## Project Overview

Transient heat conduction is a fundamental problem in thermal engineering, simulation, and scientific computing. In many real-world systems, temperature varies not only with spatial position but also with time. Traditional numerical approaches such as finite element analysis, finite difference methods, and finite volume methods are effective, but they often require mesh generation, repeated numerical solves, and careful handling of boundary conditions and domain geometry.

This project explores an alternative approach using a **physics-guided neural network** that learns temperature directly from spatial coordinates and time. The model is trained on simulation data exported from ANSYS and evaluated on two different domain types:
1. a simple conductive square plate
2. a square plate with a central geometric exclusion, or void

The objective is to examine whether a neural model can capture global thermal behaviour, transient temperature evolution, and geometry-dependent heat-flow patterns while remaining guided by the physical structure of the problem.

---

## Why This Project Matters

This project is important because it lies at the intersection of:
- machine learning
- scientific computing
- thermal simulation
- surrogate modelling
- physics-aware AI

It demonstrates the ability to:
- work with simulation-generated engineering datasets
- preprocess spatial-temporal data for learning
- design coordinate-based prediction models
- organize experiments across multiple geometries
- interpret results using both numerical and visual analysis
- document a technical project in a clean and professional way

From a portfolio perspective, it shows applied experience in solving physics-based modelling problems rather than only standard tabular, classification, or regression tasks.

---

## Objectives

The main objectives of this project are:

- To model transient 2D heat transfer using a neural-network-based surrogate framework
- To study how geometry affects temperature prediction performance
- To compare prediction behaviour across a regular conductive domain and a complex domain with an internal void
- To evaluate model performance using convergence plots, scatter plots, temperature fields, and error maps
- To build a structured workflow from simulation data to model training to engineering interpretation

---

## Problem Formulation

The thermal process studied in this project is **transient two-dimensional heat conduction**, where temperature depends on:
- spatial location: **x, y**
- time: **t**

The learning task is:

`(x, y, t) -> T`

where:
- `(x, y, t)` are the model inputs
- `T` is the predicted temperature in Kelvin

The physical problem is motivated by the transient heat equation:

`dT/dt = alpha * (d²T/dx² + d²T/dy²)`

where:
- `T` is temperature
- `alpha` is thermal diffusivity

This equation defines the physical structure behind the modelling task.

---

## Domains Studied

### 1. Solid Square Plate

- Domain size: **0.02 m x 0.02 m**
- Coordinate range: **x, y in [-0.01, 0.01]**

This domain represents a continuous conductive plate with no internal interruptions. It serves as the simpler benchmark case for the study.

### 2. Square Plate with a Central Void

- Outer domain size: **0.03 m x 0.03 m**
- Outer coordinate range: **x, y in [-0.015, 0.015]**
- Central void size: **0.01 m x 0.01 m**
- Void coordinate range: **x, y in [-0.005, 0.005]**

This domain introduces geometric complexity. Since heat cannot pass through the central void, the thermal field must redistribute around it.

---

## Boundary Conditions

The thermal setup used in this project follows the stated problem description:

- **West boundary:** 500 K
- **East boundary:** 0 K
- **North boundary:** adiabatic
- **South boundary:** adiabatic

These conditions create a left-to-right thermal gradient and drive the transient conduction process over time.

---

## Dataset Description

The datasets used in this project were generated using **ANSYS simulations** and exported into Excel format.

### Files
- `data/square.xlsx`
- `data/void.xlsx`

### Dataset Structure

Each row represents one spatial point at one time instant and contains:
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

The preprocessing workflow includes:
- loading Excel data into Python
- selecting input and target variables
- removing inconsistent or missing entries
- normalizing spatial and temporal inputs
- applying train-test split
- handling geometry-aware masking for the void domain during visualization

The output temperatures are retained in **Kelvin** to preserve physical interpretability.

---

## Methodology

The project uses a coordinate-based neural modelling approach in which the network receives `(x, y, t)` and predicts temperature `T`.

The overall methodology includes:
1. generating transient thermal data using ANSYS
2. exporting simulation results to spreadsheet format
3. preprocessing spatial and temporal coordinates
4. training neural models for both domains
5. monitoring loss and prediction behaviour
6. evaluating results through visual and regression-style analysis

The framework is described as **physics-guided** because the training process is designed around the physical structure of the heat-transfer problem and uses a learning objective motivated by both data consistency and equation-based behaviour.

---

## Model Architecture

The predictive model is a fully connected feedforward neural network.

### Architecture
- Input layer: **3 features** `(x, y, t)`
- Hidden layers:
  - 64 neurons
  - 32 neurons
  - 16 neurons
  - 8 neurons
- Output layer: **1 neuron** for temperature prediction

### Activation Function
- **ReLU**

### Rationale

This architecture was chosen to balance:
- expressive capability
- computational efficiency
- training stability

Since the task is coordinate-based and the output is a continuous scalar field, a fully connected neural network provides a practical approximation framework for this problem.

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

### Training Objective

The training process is designed around:
- **data consistency**
- **physics-guided structure**

The aim is to encourage the network not only to fit the ANSYS reference samples, but also to learn behaviour aligned with the thermal problem.

### Evaluation Approach

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
|-- notebooks/
|   |-- solid_square_pinn.ipynb
|   `-- square_with_void_pinn.ipynb
|-- data/
|   |-- square.xlsx
|   `-- void.xlsx
|-- reports/
|   |-- final_report.docx
|   `-- project_paper.pdf
|-- results/
|   |-- convergence/
|   |   |-- solid_square_loss.png
|   |   `-- square_with_void_loss.png
|   |-- solid_square/
|   |   |-- temp_error_1s.png
|   |   |-- temp_error_5s.png
|   |   |-- temp_error_10s.png
|   |   |-- temp_error_15s.png
|   |   `-- predicted_vs_actual.png
|   `-- square_with_void/
|       |-- temp_error_1s.png
|       |-- temp_error_5s.png
|       |-- temp_error_10s.png
|       |-- temp_error_15s.png
|       `-- predicted_vs_actual.png
|-- assets/
|   |-- solid_square_mesh.jpeg
|   `-- square_with_void_mesh.jpeg
|-- docs/
|   |-- project_overview.md
|   |-- results_summary.md
|   |-- resume_project_summary.md
|   `-- notebook_notes.md
|-- src/
|   `-- README.md
|-- requirements.txt
|-- CONTRIBUTING.md
|-- CITATION.cff
|-- LICENSE
|-- .gitignore
`-- README.md
