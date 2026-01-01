# Hydrodynamics and Cooling in Enzo

## What Enzo is actually solving (physics first)

### 1. Fluid Equations (conceptual, not math-heavy)

Enzo treats gas as a fluid and solves:

1. Mass conservation -> Gas doesn't disappear.
2. Momentum concervation -> Gas accelerates due to pressure & gravity.
3. Energy conservation -> Gas heats and cools.

This is **Euler Hydrodynamics** (no viscosity)

### 2. Why hydrodynamics matter for galaxies

Hydro determines:

- Gas collapse into halos
- Shock heating during mergers
- Disk vs clumpy structure
- Star formation sites

*No hydro = no galaxy*

## How Enzo does hydrodynamics (numericals)

### 3. Grid-based AMR (key difference from Gadget)

Enzo:

- Uses **Eulerian grids**
- Space is divided into **cells**
- Uses **Adaptive Mesh Refinement (AMR)**

Meaning:

- High resolution where gas collapses
- Low resolution elsewhere

This is perfect for high-z galaxies with dense star-forming regions.

### 4. Hydro solvers in Enzo 

Enzo offers solvers like:

- PPM (Piecewise Parabolic Method)
- MUSCL
- ZEUS (older)

For early galaxies:

- PPM is standard
- Good shock capturing
- low numerical diffusion

**PPM = accurate shocks**

## Cooling Physics (this is where galaxies form)

### 5. Why cooling is essential

Without cooling:

- Gas heats to ~10^6 K
- Pressure stops collapse
- No stars, no galaxies

Cooling lets gas:

- Lose thermal energy
- Collapse further
- Fragment --> Star formation

### 6. Cooling channels in early universe (high-z)

At z > 8.5, main cooling mechanisms:

|Temperature|Cooling|
|-----------|-------|
| > 10^6 K  | Bremsstrahlung|
| 10^4 - 10^6 K | Atomic H, He |
| < 10^4 K | Molecular H2 |
| Metal-rich gas | Metal-line cooling |

Early galaxies:

- Initially metal-poor
- H & He dominate
- H2 critical for first stars

## How Enzo implements cooling

### Cooling modules (conceptual)

Enzo uses:

- Tabulated cooling rates
- depends on:
- - Temperature
  - Density
  - Metallicity
  - UV background

 Cooling is applied as:
 Energy_new = Energy_old - Cooling_rate x dt

