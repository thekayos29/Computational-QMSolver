# Computational 1-D Schrödinger Equation Solver

 This project builds a 1-D Schrödinger Equation solver from first principles in Python, bypassing black-box packages to solve the equation directly using calculus and linear algebra.

---

## Technical Overview & Core Methods

We solve the time-independent Schrödinger equation for an arbitrary potential $V(x)$:

$$-\frac{\hbar^2}{2m}\frac{d^2\psi}{dx^2} + V(x)\psi = E\psi$$

The project approaches this boundary value problem using two distinct strategies:

### 1. Finite Difference Method (FDM)
* **Core Principle:** Converts continuous differential calculus into discrete linear matrix algebra.
* **How it works:** The spatial domain is split into $N$ grid points. The second derivative is replaced with a three-point central difference fraction:

$$\frac{d^2\psi}{dx^2} \approx \frac{\psi_{i+1} - 2\psi_i + \psi_{i-1}}{\Delta x^2}$$

This turns the calculus problem into a large tridiagonal spreadsheet matrix. Diagonalizing this matrix solves the entire energy spectrum at once.

### 2. The Shooting Method
* **Core Principle:** Replaces global matrix math with a target-shooting trajectory guessing game.
* **How it works:** It treats the boundary problem as an initial value problem. It picks a trial energy $E$ and integrates the wavefunction across the grid step-by-step using a manual **4th-Order Runge-Kutta (RK4)** engine. If the energy guess is wrong, the wave blows up to infinity at the far boundary. A **bisection root-finder** monitors this error, adjusting the energy until the wave lands perfectly at zero.

---

## Project Architecture & Deliverables

The code is broken down cell-by-cell to handle specific project milestones:

* **1 (Setup):** Discretizes continuous spatial domain into uniform coordinate vector.
* **2 (Potentials):** Defines potential energy functions as vectorized spatial profile arrays.
* **3 (FDM Solver):** Approximates second-derivative operator as symmetric tridiagonal matrix.
* **4 (Shooting Solver):** Solves ODE boundary problem using RK4 and bisection tracking.
* **5 (Validation):** Computes eigenvalue accuracy by comparing numerical results to exact solutions.
* **6 (Exploration):** Diagonalizes Hamiltonian matrix finding system eigenvectors and eigenvalues.
* **7 (Playground):** Re-computes Hamiltonian eigenvalues dynamically via interactive UI slider callbacks.

---

## Verification Benchmarks

To prove the code tracks real physics rather than ungrounded approximations, it must meet three quantitative accuracy checks:

* **Ground State Error ($< 0.01\%$):** Verified against the analytical harmonic oscillator energy ($E_0 = 0.5$).
* **Excited State Accuracy ($\le 0.1\%$):** Proves grid precision holds for the first 5 oscillating states.
* **Solver Generality (Piecewise Smooth):** Code handles smooth curves and sharp step-barriers without crashing.

---

## Getting Started
(NOTE : DOWNLOAD THE IPYNB FILE AND RUN THE BLOCKS ONE BY ONE )
### Prerequisites
Install the standard Python scientific stack:
```bash
pip install numpy scipy matplotlib ipywidgets
