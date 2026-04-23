# CSE 5280 — Camera Trajectory Animation Using Lie Group Interpolation

Nick Speranza

This project studies camera trajectory generation on matrix Lie groups for smooth motion in 3D graphics. Instead of treating camera translation and rotation as unrelated quantities in Euclidean space, the trajectory is modeled using rigid-body transformations on \( SE(3) \), with interpolation performed through Lie-group exponential and logarithm maps.

The notebook builds and compares several camera trajectories defined by keyframe poses, including:
- a simpler baseline using linear translation with SLERP rotation
- a piecewise \( SE(3) \) geodesic trajectory
- a smoother bonus trajectory built in Lie algebra coordinates

The project includes both geometric trajectory visualizations and a rendered camera flythrough. It also examines how Lie-group interpolation compares with simpler Euclidean-style motion in terms of smoothness, consistency, and geometric meaning.

## 📄 View Report

Open the full notebook here:

https://nbviewer.org/github/nicolas-speranza/cse5280-camera-trajectory-nicolas-speranza/blob/main/cse5280_camera_trajectory.ipynb

## Project Contents

- mathematical background on \( SO(3) \), \( SE(3) \), and Lie algebra maps
- construction of keyframe camera poses around a target
- piecewise Lie-group interpolation between poses
- static trajectory visualizations in 3D
- frame-to-frame motion analysis for path smoothness
- a camera trajectory animation
- a ray-traced flythrough generated from the moving camera
- bonus experiments on manifold interpolation and perturbations

## Main Ideas

A camera pose in 3D is not just a point. It contains:
- a position
- an orientation

Because of this, camera motion is more naturally modeled as motion on a manifold rather than by interpolating unrelated vector components independently. Lie-group methods make this possible by:
- mapping poses into a tangent-space representation with the logarithm map
- interpolating there in a structured way
- mapping the motion back to the group using the exponential map

This helps preserve rigid-motion structure and produces motion that is more geometrically meaningful than a purely Euclidean construction.

## Methods

The notebook uses several keyframe camera poses arranged around a scene and aimed toward a target. From these keyframes, multiple trajectory constructions are compared:

### 1. Baseline interpolation
This method uses:
- linear interpolation for camera centers
- SLERP for camera orientation

It is simple and often reasonable, but translation and rotation are still handled separately.

### 2. Piecewise \( SE(3) \) geodesic interpolation
This method interpolates directly between rigid transforms using

\[
T(\alpha) = T_0 \exp\left(\alpha \log(T_0^{-1}T_1)\right)
\]

This produces a trajectory that respects the structure of rigid motion more directly.

### 3. Bonus smooth trajectory in Lie algebra coordinates
A smoother trajectory is also constructed using interpolation in Lie algebra coordinates across multiple keyframes. This gives a more continuous global curve, while also showing that higher-order smoothing can introduce different motion behavior and nonuniform pacing.

## Bonus Experiments

The notebook also includes bonus-style experiments beyond the core requirements:

- **\( SO(3) \) plus Euclidean translation vs full \( SE(3) \)**  
  Compares separate rotation/translation treatment against direct rigid-motion interpolation.

- **Tangent-space twist perturbations**  
  Small twists are applied in Lie algebra coordinates to perturb the trajectory.

- **Left vs right perturbations**  
  Demonstrates noncommutative behavior by comparing left-multiplied and right-multiplied perturbations.

- **Multiple keyframes / closed-loop style trajectory**  
  Uses several keyframes arranged around the scene to form a more complex orbit-like path.

## Results

The report includes:
- 3D trajectory plots showing keyframes, centers, and selected coordinate frames
- a frame-to-frame motion comparison for smoothness analysis
- a cleaned camera trajectory animation
- a ray-traced camera flythrough from the moving viewpoint
- a discussion of why Lie-group interpolation is more principled than a simpler Euclidean baseline

The final notebook also uses a constant-speed version of the \( SE(3) \) path for the main trajectory animation so that the motion is easier to interpret visually.

## Files

- `cse5280_camera_trajectory.ipynb` — main notebook/report
- `README.md` — project overview

## Running the Notebook

This project is designed to run in Google Colab.

Typical dependencies:
- `numpy`
- `matplotlib`
- `scipy`
- `imageio`
- standard Python libraries used in the notebook

Run the notebook from top to bottom to generate:
- trajectory figures
- smoothness plots
- trajectory animations
- the ray-traced flythrough

## Summary

This project shows that Lie-group interpolation provides a natural mathematical framework for camera motion in 3D graphics. Modeling poses on \( SE(3) \) leads to trajectories that are more structured and geometrically meaningful than treating translation and rotation independently. The experiments and visualizations also show how tangent-space perturbations and different manifold constructions influence the resulting motion.
