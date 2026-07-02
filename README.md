# 3-Body Gravitational Dynamics with Leapfrog Integration

This repository contains a Python implementation to simulate and plot the orbital trajectories of 3-body gravitational systems. The project focuses on tracking chaotic motion and verifying energy conservation using a symplectic integrator.

---

## Mathematical Framework

The gravitational acceleration $\mathbf{a}_i$ acting on a body $i$ due to other bodies $j$ is calculated using Newton's Law of Universal Gravitation:

$$\mathbf{a}_i = -G \sum_{j \neq i}^{N} \frac{m_j}{|\mathbf{r}_i - \mathbf{r}_j|^3} (\mathbf{r}_i - \mathbf{r}_j)$$

Where:
* $G$ is the gravitational constant (normalized to $GM = 1$ in our simulation units).
* $\mathbf{r}$ represents the position vector.
* $m$ represents the mass of the bodies.

---

## Leapfrog Integration Method

To ensure stable orbits over long time periods, we use the **Symplectic Leapfrog (Kick-Drift-Kick)** integration method instead of the standard Euler method. This maintains the energy balance of the system without introducing artificial computational drift.

The position and velocity updates for each time step $\Delta t$ are computed as follows:

1. **Velocity Half-Step (Kick):**
   $$\mathbf{v}_{i}\left(t + \frac{\Delta t}{2}\right) = \mathbf{v}_i(t) + \mathbf{a}_i(t) \frac{\Delta t}{2}$$

2. **Position Update (Drift):**
   $$\mathbf{r}_i(t + \Delta t) = \mathbf{r}_i(t) + \mathbf{v}_i\left(t + \frac{\Delta t}{2}\right) \Delta t$$

3. **Velocity Final Half-Step (Kick):**
   $$\mathbf{v}_i(t + \Delta t) = \mathbf{v}_i\left(t + \frac{\Delta t}{2}\right) + \mathbf{a}_i(t + \Delta t) \frac{\Delta t}{2}$$

---

## Features & Implementation

* **Vectorized Computations:** Implemented using `NumPy` to efficiently update coordinates across multiple arrays simultaneously.
* **Energy Diagnostics:** Calculates and plots Kinetic Energy (KE) and Potential Energy (PE) at every step to verify total energy conservation ($E_{\text{total}} = T + V$).
* **Batch Testing:** Automatically simulates and records **10 different initial configurations (Cases 1–10)**, saving the resulting trajectory and energy plots as `.png` files.

---

## Setup & Execution

### Prerequisites
Make sure you have Python installed along with `numpy` and `matplotlib`.

### Running the Code
1. Clone the repository:
   ```bash
  git clone https://github.com/abrium-tech/3-body-gravitational-dynamics.git
