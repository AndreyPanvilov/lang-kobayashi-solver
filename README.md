# Lang-Kobayashi Solver

Numerical exploration of semiconductor laser dynamics with delayed optical feedback using the Lang–Kobayashi model.

This repository brings together notebooks for:

- time-domain simulation of the reduced Lang–Kobayashi system;
- tracking of characteristic roots;
- construction of D-partitions for selected external-cavity modes (ECMs);
- computation of ECM existence boundaries;
- numerical search for all ECM solutions for a given parameter set.

---

## Main idea

The project studies the nonlinear dynamics of a semiconductor laser with delayed optical feedback.  
The model is written in terms of the field amplitude, phase, and feedback-induced delay. In polar form, the field is represented as

$$
E(t)=R(t)e^{i\theta(t)},
$$

where $R(t)$ is the field amplitude and $\theta(t)$ is the optical phase.

The notebooks cover both the dynamical simulation itself and the analysis of stationary modes, their stability, and the movement of characteristic roots as parameters change.

---

## What is inside the repository

### `Solve_Lang_Koboyashi_reduced.ipynb`

Numerical solution of the reduced Lang–Kobayashi system in polar coordinates.

What this notebook does:

- integrates the delay differential equations;
- reconstructs the time series of intensity and phase;
- plots the intensity
  $I(t)=R^2(t),$
  and the instantaneous frequency;
- extracts local maxima and builds return maps;
- estimates the largest Lyapunov exponent with the Rosenstein method.

This notebook is the main entry point for studying time-domain dynamics, periodicity, quasi-periodicity, and chaos.

### `Characteristic_Root_Tracking.ipynb`

High-precision computation and visualization of characteristic roots of the linearized system.

What this notebook does:

- solves the characteristic equation in the complex plane;
- tracks how roots move when the delay $h$ changes;
- illustrates root trajectories in the $(\Re\lambda,\Im\lambda)$ plane;
- helps identify stability changes and spectral rearrangements.

The implementation uses `mpmath` with increased precision, which is useful when the roots are close to each other or when the spectrum is stiff.

### `D-patrition_for_esm.ipynb`

Construction of a D-partition for a fixed ECM branch.

What this notebook does:

- selects one ECM mode by tracking a chosen phase branch $\eta$;
- finds points where the characteristic equation admits purely imaginary roots$\lambda=i\omega;$
- traces the D-partition curves in the $(\gamma,h)$ plane;
- keeps the branch consistent by continuation in $\eta$.

This notebook is used to identify stability boundaries for a chosen ECM.

### `ESM.ipynb`

Search for all ECM/ESM solutions for a given set of parameters.

What this notebook does:

- scans the parameter space for stationary modes;
- finds all admissible solutions for the chosen parameters;
- helps identify which ECM branches are present at a given point in parameter space.

---

## Mathematical objects used in the project

The notebooks use several core equations of the Lang–Kobayashi framework.

### ECM equation

A stationary external-cavity mode is found from

$$
\eta-\omega_0 h+
\gamma h\sqrt{1+\alpha^2}
\sin\!\left(\eta+\arctan\alpha\right)=0.
$$

### Characteristic equation

Stability of a selected mode is studied through the corresponding characteristic equation.  
On the stability boundary, the roots satisfy

$$
\lambda=i\omega.
$$

This is used in the D-partition notebook and in the root-tracking notebook.

### Saddle-node boundary of existence

For the ECM existence boundary, the notebook derives the saddle-node condition and produces the dashed boundary curve in the $(\gamma,h)$ plane.

---

## Recommended workflow

A typical workflow is:

1. Solve the reduced Lang–Kobayashi system in `Solve_Lang_Kobayashi_reduced.ipynb`.
2. Extract and analyze the relevant steady or transient regime.
3. Study the characteristic roots in `Characteristic_Root_Tracking.ipynb`.
4. Build the D-partition for a chosen mode in `D-patrition_for_esm.ipynb`.
5. Search for all modes at a given parameter set in `ESM.ipynb` when needed.

---

## Requirements

Recommended environment:

- Python 3.10+
- `numpy`
- `scipy`
- `matplotlib`
- `mpmath`
- `jupyter`

Install dependencies with:

```bash
pip install -r requirements.txt
```

If you prefer, you can also install packages manually:

```bash
pip install numpy scipy matplotlib mpmath jupyter
```

---

## How to run locally

1. Clone the repository:

```bash
git clone https://github.com/AndreyPanvilov/lang-kobayashi-solver.git
cd lang-kobayashi-solver
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On Linux or macOS:

```bash
source .venv/bin/activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Launch Jupyter:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

5. Open the notebook you need and run the cells from top to bottom.

---

## How to run on a server or JupyterHub

The notebooks can also be used on a server through JupyterHub.

Typical usage:

1. Open your JupyterHub session in the browser.
2. Upload the repository files, or open the repository from the mounted project directory.
3. Open the required notebook.
4. Run the cells in order.

If the JupyterHub environment already provides the required packages, no additional installation is needed.  
If not, install them inside the notebook environment or in the server environment with:

```bash
pip install -r requirements.txt
```

This makes the project convenient for shared lab environments and remote workstations where users do not want to set up Python manually.

---

## Outputs you can expect

The notebooks generate:

- time series of field intensity and phase;
- return maps of maxima;
- phase portraits;
- delay-embedding reconstructions;
- largest Lyapunov exponent estimates;
- characteristic root trajectories;
- D-partition diagrams;
- ECM existence boundaries.

---

## Repository structure

A compact project layout may look like this:

```text
.
├── Characteristic_Root_Tracking.ipynb
├── Solve_Lang_Koboyashi_reduced.ipynb
├── D-patrition_for_esm.ipynb
├── ESM.ipynb
├── requirements.txt
├── README.md
```

---

## Notes for users

- The notebooks are written as research notebooks, so some cells may use hard-coded parameter values for reproducibility.
- For reliable results, run the notebooks sequentially and avoid skipping initialization cells.
- Some procedures, such as root tracking and branch continuation, are sensitive to initial guesses and parameter ranges.
- If a notebook uses a large amount of computation time, consider running it on a machine with enough memory and a stable Python environment.

---

## Author

Andrey Panvilov

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
