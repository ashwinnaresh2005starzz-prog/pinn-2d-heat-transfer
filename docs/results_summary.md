# Results Summary

## Datasets
- Solid square dataset: 7695 points
- Square-with-void dataset: 3600 points
- Time range: 1 s to 15 s

## Model Setup
- Inputs: x, y, t
- Output: temperature in Kelvin
- Architecture: 64 -> 32 -> 16 -> 8 -> 1
- Activation: ReLU
- Optimizer: Adam
- Learning rate: 0.001
- Epochs: 3000
- Train-test split: 70:30

## Main Observations
- The solid square domain shows a smooth global thermal gradient
- The square-with-void domain captures heat redistribution around the void
- Scatter plots show strong agreement with the ANSYS reference values
- Error maps indicate larger local errors near boundaries than in the interior

## Limitations
- The study is limited to 2D homogeneous materials
- Results are based on simulation-generated data
- Boundary-condition handling can be improved further
- Stronger transient PDE enforcement would improve physical fidelity
