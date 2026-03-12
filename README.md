### Objectives

- Model a multi-storey building using the **lumped mass method**
- Construct the **mass matrix [M]** and **stiffness matrix [K]**
- Solve the **eigenvalue problem** for natural frequencies
- Compute and visualize **mode shapes** of each floor

##  Theory
### Lumped Mass Model

In structural dynamics, buildings are simplified by assuming:

- Each floor has a **concentrated (lumped) mass**
- Each storey behaves like a **linear spring** with stiffness
- Motion occurs only in the **horizontal direction**

```
        ● m₃        ← Floor 3 (roof)
        │
       [k₃]         ← 3rd storey spring
        │
        ● m₂        ← Floor 2
        │
       [k₂]         ← 2nd storey spring
        │
        ● m₁        ← Floor 1
        │
       [k₁]         ← 1st storey spring
        │
   ▓▓▓▓▓▓▓▓▓▓▓     ← Ground (fixed base)
```

### Equation of Motion

For a system with `n` floors, undamped free vibration is governed by:
```
M·ẍ + K·x = 0
```

| Symbol | Description |
|--------|-------------|
| `M`  | Mass matrix |
| `K`  | Stiffness matrix |
| `x`  | Displacement vector |
| `ẍ` | Acceleration vector |

### Generalized Eigenvalue Problem

To find vibration characteristics, we solve:
```
[K]{φ} = λ[M]{φ}
```

| Symbol | Description |
|--------|-------------|
| `λ = ω²`        | Eigenvalues → squared natural frequencies |
| `{φ}`           | Eigenvectors → mode shapes |
| `ω = √λ`        | Natural frequency (rad/s) |
| `f = ω / 2π`    | Natural frequency (Hz) |


##  System Description

This project models a **3-floor building** with the following assumptions:

| Assumption | Detail |
|------------|--------|
| Floor behavior | Rigid mass (no deformation) |
| Storey behavior | Linear spring |
| Damping | Not considered |
| Direction of motion | Horizontal (lateral) only |

### System Parameters

| Parameter | Value |
|-----------|-------|
| Number of Floors | 3 |
| Mass per Floor (m₁, m₂, m₃) | 1000 kg each |
| Storey Stiffness (k₁, k₂, k₃) | 20000 N/m each |


##  Mathematical Model

### Mass Matrix `[M]`

Diagonal matrix with floor masses:
```
    | m₁   0    0  |       | 1000    0      0  |
M = |  0   m₂   0  |   =   |    0  1000      0  |
    |  0    0   m₃ |       |    0     0   1000  |
```

### Stiffness Matrix `[K]`

Tridiagonal matrix assembled from storey stiffnesses:
```
    | k₁+k₂   -k₂      0   |       | 40000  -20000       0 |
K = |  -k₂   k₂+k₃   -k₃  |   =   |-20000   40000  -20000 |
    |   0      -k₃     k₃  |       |     0  -20000   20000 |
```

> Each floor only interacts with the floors directly above and below — hence the tridiagonal structure.

##  Applications

This type of analysis is widely used in:

-  Earthquake engineering and seismic design
-  Structural health monitoring
-  Building design and code compliance
-  Mechanical vibration analysis
-  Aerospace and mechanical structures
-  Finite element structural modeling
