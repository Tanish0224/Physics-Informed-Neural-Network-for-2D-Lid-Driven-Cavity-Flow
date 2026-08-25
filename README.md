# Physics-Informed-Neural-Network-for-2D-Lid-Driven-Cavity-Flow

## 📌 Project Overview

This project develops a **Physics-Informed Neural Network (PINN)** to solve the **steady, incompressible 2D lid-driven cavity (LDC) flow** at **Re = 1000** on the unit-square domain `[0,1]²`. The network enforces the **incompressible Navier–Stokes equations and boundary conditions** at collocation points, providing a **mesh-free alternative to conventional CFD solvers**. The predicted flow field is **validated against the Botella & Peyret (1998) spectral benchmark** to assess solution accuracy.

## 🔬 Methods

- **Governing Equations:** Non-dimensionalized steady incompressible **Navier–Stokes equations** at **Re = 1000**.
- **Boundary Conditions:** Exact enforcement of the **sharp-lid** conditions using an output transformation.
- **Network:** Modified **MLP** with sine activation in the first layer and **8 tanh hidden layers × 64 neurons**, mapping `(x, y) → (u, v, p)`.
- **Training:** Reynolds-number curriculum **(Re = 100 → 400 → 700 → 1000)** using **Adam**, followed by **L-BFGS fine-tuning** at Re = 1000.
- **Collocation:** **128 × 128 Chebyshev–Gauss–Lobatto grid**, clustered near walls and corners to resolve steep flow gradients.

- ## 🛠️ Work Performed

- Developed a custom **ModifiedMLP** in PyTorch with **sine + tanh activations** and Xavier initialization.
- Implemented **exact boundary-condition enforcement** with a smooth corner-taper treatment for the sharp-lid configuration.
- Formulated **continuity and momentum PDE residuals** using PyTorch autograd for first- and second-order derivatives.
- Implemented **Reynolds-number curriculum training** with staged Adam optimization followed by L-BFGS refinement.
- Developed **flow-field evaluation and visualization** for velocity, pressure, speed, vorticity, streamlines, and centerline profiles.
- Built **quantitative L₂/L∞ error analysis and unit tests** to verify boundary conditions, pressure gauge, and collocation sampling.

- ## 📊 Results & Conclusion

- Reproduced the **primary and corner-vortex structures** at Re = 1000, with centerline velocity profiles closely matching the **Botella & Peyret (1998)** benchmark away from corner singularities.
- Quantified solution accuracy using **L₂/L∞ errors, velocity profiles, and flow-field/vorticity visualization** against the reference solution.
- Demonstrated the importance of **physics-constrained training, collocation design, and corner-singularity treatment** for developing reliable PINN-based CFD models with potential for **mesh-free flow prediction and surrogate modeling**.

- ## 🛠️ Tools & Technologies

- **Programming:** Python 3
- **PINN Framework:** PyTorch, Autograd
- **Optimization:** Adam, L-BFGS
- **Data & Analysis:** NumPy
- **Visualization:** Matplotlib — loss, velocity profiles, contours, streamlines & vorticity
- **Compute:** Google Colab with NVIDIA T4 GPU
