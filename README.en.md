<p align="center">
  <a href="README.md">Русский</a> | <b>English</b> | <a href="README.de.md">Deutsch</a>
</p>

# Rectangular Waveguide on $H_{10}$ ($TE_{10}$) Mode (4.2 GHz, C-Band)

This repository contains engineering design files, analytical calculations, and 3D electromagnetic numerical simulations for a hollow rectangular waveguide operating in the fundamental $H_{10}$ ($TE_{10}$) mode at a center frequency of $f_0 = 4.2\text{ GHz}$ (C-band).

The project includes analytical mathematical derivations in PTC Mathcad, parametric 3D CAD models with a standard mounting flange (SolidWorks / STEP), and full-wave electromagnetic verification in CST Studio Suite.

---

## Project Structure

```text
rectangular-waveguide-4.2ghz/
├── cad/                  # 3D CAD models (SolidWorks SLDPRT, STEP format)
├── calculations/         # Analytical calculation worksheets in PTC Mathcad (.xmcd)
├── docs/images/          # Engineering calculation sheets, 3D model renders, and simulation plots
└── simulation/           # Electromagnetic simulation project in CST Studio Suite (.cst)
```

---

## Analytical Calculations

Analytical calculation of the waveguide channel was performed in PTC Mathcad using Maxwell's electrodynamic equations for hollow metallic waveguides.

![Parameters and Constants](docs/images/calc_waveguide_parameters.png)

### 1. Input Parameters and Physical Constants
- **Center Frequency**: $f_0 = 4.2\cdot 10^9\text{ Hz}$ ($4.2\text{ GHz}$)
- **Speed of Light in Vacuum**: $c \approx 2.998\cdot 10^8\text{ m/s}$
- **Free-Space Wave Impedance**: $Z_0 = 120\pi \approx 376.73\ \Omega$
- **Permittivity of Free Space**: $\varepsilon_0 \approx 8.854\cdot 10^{-12}\text{ F/m}$
- **Conductor Material**: Aluminum alloy with electrical conductivity $\sigma = 35.7\cdot 10^6\text{ S/m}$

### 2. Geometry Dimensions and Single-Mode Bandwidth
Free-space wavelength:
$$\lambda_0 = \frac{c}{f_0} = 71.379\text{ mm}$$

To ensure single-mode propagation ($TE_{10}$) and prevent higher-order modes ($TE_{20}$, $TE_{01}$), the broad wall dimension $a$ was calculated:
- Minimum broad wall dimension: $a_{min} = \frac{\lambda_0}{2} = 35.69\text{ mm}$
- Selected broad wall dimension: $a_{eff} = 53.534\text{ mm}$
- Narrow wall dimension ($b = 0.5 \cdot a_{eff}$): $b = 26.767\text{ mm}$

![Cutoff Parameters and Wave Impedance](docs/images/calc_waveguide_cutoff_impedance.png)

### 3. Electrodynamic Properties
- **Cutoff Wavelength ($TE_{10}$)**: $\lambda_{crit} = 2 \cdot a_{eff} = 107.069\text{ mm}$
- **Cutoff Frequency ($TE_{10}$)**: $f_{crit} = \frac{c}{\lambda_{crit}} = 2.80\text{ GHz}$
- **Higher-Order Mode Threshold**: $f_{high} = 2 \cdot f_{crit} = 5.60\text{ GHz}$
- **Characteristic Wave Impedance ($TE_{10}$)**:
  $$W_h = \frac{Z_0}{\sqrt{1 - \left(\frac{\lambda_0}{\lambda_{crit}}\right)^2}} = 505.787\ \Omega$$
- **Guide Wavelength**:
  $$\lambda_B = \frac{\lambda_0}{\sqrt{1 - \left(\frac{\lambda_0}{\lambda_{crit}}\right)^2}} = 95.765\text{ mm}$$

![Attenuation and Power Capacity](docs/images/calc_waveguide_attenuation_power.png)

- **Attenuation Constant (Conductor Loss)**: $\alpha_R = 35.974\cdot 10^{-3}\text{ dB/m}$ ($0.036\text{ dB/m}$)
- **Breakdown Power Handling (in air)**: $P_{max} = 605.595\text{ kW}$

---

## 3D CAD Modeling

The waveguide section was modeled in SolidWorks and verified in CST Studio Suite. The assembly features an internal rectangular duct of $53.534 \times 26.767\text{ mm}$ and an interface flange with 4 mounting holes and an alignment shoulder.

![Waveguide 3D Model in CST Studio Suite](docs/images/model_3d_waveguide_flange.png)

- **Boundary Conditions**: Open add space along the propagation axis, lossy metal wall boundaries corresponding to aluminum conductivity.
- **Excitation Ports**: Waveguide ports (Port 1 and Port 2) positioned at the waveguide terminals supporting the fundamental $TE_{10}$ mode.

---

## Simulation Results

Electromagnetic numerical analysis was performed across the $3.0\text{--}5.0\text{ GHz}$ frequency spectrum.

### 1. Voltage Standing Wave Ratio (VSWR)
![VSWR Plot](docs/images/simulation_vswr.png)

At the design center frequency of $4.2\text{ GHz}$:
- $\text{VSWR}_1 = 1.00183$
- $\text{VSWR}_2 = 1.00183$

Across the entire $3.0\text{--}5.0\text{ GHz}$ sweep, the VSWR remains below $1.004$, confirming impedance matching within nominal tolerances.

### 2. Scattering Parameters (S-Parameters)
![S-Parameters Plot](docs/images/simulation_s_parameters.png)

At the design center frequency of $4.2\text{ GHz}$:
- **Reflection Coefficient ($S_{11}, S_{22}$)**: $-60.77\text{ dB}$ / $-60.79\text{ dB}$ (return loss $> 60\text{ dB}$).
- **Transmission Coefficient ($S_{21}, S_{12}$)**: $-0.067\text{ dB}$ (minimal insertion loss over the component length).

### 3. Impedance Parameters (Z-Parameters)
![Z-Parameters Plot](docs/images/simulation_z_parameters.png)

At $4.2\text{ GHz}$:
- **Mutual Transfer Impedance ($Z_{21}, Z_{12}$)**: $509.47\ \Omega$.

The simulated mutual impedance $Z_{21} \approx 509.5\ \Omega$ demonstrates high convergence with the analytical wave impedance $W_h = 505.79\ \Omega$ (deviation below $0.73\%$, attributed to line length transformation and port boundary discretization).

---

## License

Copyright (c) 2026 Ilya Kornilov

This source describes Open Hardware and is licensed under the CERN-OHL-P v2. 
You may redistribute and modify this source and make products using it under 
the terms of the CERN-OHL-P v2 (https://cern.ch/cern-ohl).

This source is distributed WITHOUT ANY EXPRESS OR IMPLIED WARRANTY, 
INCLUDING OF MERCHANTABILITY, SATISFACTORY QUALITY AND FITNESS FOR A 
PARTICULAR PURPOSE. Please see the CERN-OHL-P v2 for applicable conditions.
