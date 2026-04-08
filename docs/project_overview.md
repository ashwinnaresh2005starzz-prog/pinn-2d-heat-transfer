# Project Overview

This project studies transient 2D heat transfer in homogeneous materials using a physics-guided neural network framework.

## Domains studied
1. Solid square plate
2. Square plate with a central void

## Inputs
- x-coordinate
- y-coordinate
- time

## Output
- temperature in Kelvin

## Workflow
- ANSYS simulation data generation
- dataset preprocessing
- neural network training
- physics-guided loss formulation
- comparison with reference temperature fields
- visualization through convergence plots, scatter plots, contour maps, and absolute error maps

## Project goal
To evaluate whether a neural network guided by physical structure can approximate transient temperature distribution for both regular and complex geometries.
