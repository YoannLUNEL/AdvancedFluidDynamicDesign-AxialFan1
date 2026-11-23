<div align="center">

<!-- Logo de l'école ESEIAAT (UPC) -->
![Logo UPC](https://github.com/MiguelAndriano/Team-3_Advanced-Fluid-Dynamic-Design/blob/main/UPC_logos/LOGO_UPC.png)
***

# **PC Fans for heating down the tower**
### *Advanced Fluid Dynamics Design*

<br>

<!-- Image du ventilateur d'ordinateur -->
<img src="https://images.unsplash.com/photo-1587202372775-e229f172b9d7?w=600" alt="Ventilateur d'ordinateur" width="400"/>

<br>
<br>

### **Team members**

| Name| Role| Github username |
| :--- | :--- | :--- | 
| **Yoann Lunel** | Design / Leader | YoannLUNEL|
| **Erwann Penin** | CFD|ErwannPenin|
| **ANDRIANO GRANADOS MIGUEL ANGEL** | Experimentation |	MiguelAndriano|


<br>

---

**University :** ESEIAAT - Universitat Politècnica de Catalunya (UPC)  
**Course :** Advanced Fluid Dynamics Design         
**School year :** 2026 – 2027  
**Date :** [13/10/26]


</div>




# Project Report — Release 1: Design

## 1. Specifications and Dimensionless Parameters

The objective of this project is to design an axial cooling fan for a standard 110 mm PC case, achieving an optimal balance between airflow, moderate static pressure, and low acoustic noise.

### 1.1 Design Specifications (Nominal Operating Point)

The nominal operating point is calibrated with a benchmark of commercial fans (such as the Noctua NF-A12x25 operating at 1800 rpm, one of the three references).

| Parameter | Symbol | Value | Unit |
| :--- | :---: | :---: | :---: |
| Rotor Outer Diameter (Tip) | $D$ | 110.0 | mm |
| Hub Diameter | $D_h$ | 50.0 | mm |
| Number of Blades | $Z$ | 8 | — |
| Nominal Rotational Speed | $N$ ($\omega$) | 1800 /188.50 | rpm / rad/s |
|  Flow Rate | $Q$ | 95 / 0.02638 | m³/h / m³/s |
| Target Total Pressure Rise | $\Delta P_0$ | 13.0 | Pa |
| Air Density at 20 °C | $\rho$ | 1.22 | kg/m³ |
| Air Dynamic Viscosity | $\mu$ | $1.8 \times 10^{-5}$ | Pa·s |

Total Pressure rise is found using the following formula  ($\Delta P_0 = \Delta P_{\text{stat}} + \frac{1}{2}\rho c_x^2$). Using the values of the Noctua, we found that for 95m³/h, $P_dyn=0.5mmH20$ (4,9Pa) and $P_stat = 8 Pa$.

### 1.2 Mean-Radius Kinematic Analysis (RMS)

To accurately represent the average flow across the span while dividing the annulus into two equal-area regions between hub and tip, the preliminary analysis is performed at the **Root-Mean-Square (RMS) radius**:

$$
r_m = \sqrt{\frac{r_t^2 + r_h^2}{2}} = \sqrt{\frac{0.060^2 + 0.025^2}{2}} = 0.0460\text{ m} \quad (45.96\text{ mm})
$$

From the annular flow area $A = \pi (r_t^2 - r_h^2) = 9.346 \times 10^{-3}\text{ m}^2$ and Euler's turbomachinery equation (assuming purely axial inlet flow, $c_{\theta 1} = 0$, and ideal hydraulic efficiency $\eta = 1$ for preliminary sizing):

* **Mean blade tangential velocity:** $U = \omega \cdot r_m = \mathbf{8.66\text{ m/s}}$
* **Mean axial velocity:** $c_x = \frac{Q}{A} = \mathbf{2.82\text{ m/s}}$
* **Outlet tangential air velocity (swirl):** $c_{\theta 2} = \frac{\Delta P_0}{\rho \cdot U} = \mathbf{1.25\text{ m/s}}$

### 1.3 Dimensionless Parameters and Cordier Diagram

Dimensional analysis characterizes the aerodynamic similarity of the fan and validates the choice of an axial architecture:

* **Flow Coefficient ($\phi$):**
  $$\phi = \frac{Q}{\omega D^3} = \mathbf{0.0810}$$
  *Interpretation:* Moderate flow coefficient well suited for a compact PC cooling fan.

* **Head (Pressure) Coefficient ($\psi$):**
  $$\psi = \frac{\Delta P_0}{\rho \omega^2 D^2} = \mathbf{0.0212}$$
  *Interpretation:* Low aerodynamic loading typical of low-pressure axial fans.

* **Ideal Power Coefficient ($\hat{P}$):**
  $$\hat{P} = \phi \cdot \psi = \mathbf{0.001715}$$
  *Interpretation:* Corresponds to an ideal aerodynamic power output of approximately $0.34\text{ W}$.

* **Machine Reynolds Number ($Re_D$):**
  $$Re_D = \frac{\rho c_x D}{\mu} = \mathbf{2.26 \times 10^4}$$
  *Interpretation:* Low-Reynolds / transitional regime, meaning the blades are sensitive to laminar boundary layer separation.

* **Specific Diameter ($D_s$):**
  $$D_s = \frac{D (\Delta P_0 / \rho)^{1/4}}{Q^{1/2}} = \mathbf{1.3402}$$
  *Interpretation:* Falls directly within the optimal Cordier band for axial turbomachines.

* **Specific Speed ($\Omega_s$):**
  $$\Omega_s = \frac{\omega Q^{1/2}}{(\Delta P_0 / \rho)^{3/4}} = \mathbf{5.1279}$$
  *Interpretation:* Since $\Omega_s > 2.5$, this confirms that an **axial fan** architecture is the optimal choice for these high-flow, low-pressure specifications.

---

## 2. Geometric Description of the Axial Fan Components

The fan assembly consists of four main mechanical and aerodynamic sub-components designed to fit a standard $120 \times 120 \times 25\text{ mm}$ PC mounting envelope (105 mm mounting hole spacing with four $\varnothing 4.3\text{ mm}$ holes):

1. **Hub:** Central cylindrical core with an outer diameter of $D_h = 50\text{ mm}$ (hub-to-tip ratio $\nu = D_h / D = 0.417$). It houses the brushless DC motor (12 V), permanent magnets, and bearing assembly, while providing structural support for the blade roots.
2. **Impeller Blades:** A set of $Z = 8$ twisted airfoil blades extending from the hub ($r_h = 25\text{ mm}$) to the tip ($r_t = 60\text{ mm}$), giving a blade span of $h = 35\text{ mm}$. Their cambered profile transfers mechanical energy from the shaft to the airflow.
3. **Frame / Shroud:** Outer square housing ($120 \times 120\text{ mm}$) incorporating an internal cylindrical duct. A minimal **radial tip clearance** ($\approx 0.5\text{ to }1.0\text{ mm}$) is maintained between the blade tips and the shroud to prevent mechanical contact while minimizing tip leakage vortices, which cause pressure losses and acoustic noise.
4. **Support Struts:** Four thin stator struts connecting the rear motor mount to the outer frame. Their cross-section is streamlined to minimize wake drag and tonal noise from rotor–stator interaction.

---

## 3. Materials and Characteristics — Justification

Material selection is driven by three core requirements: **high stiffness under centrifugal loading** (to maintain tight tip clearances and prevent creep), **low rotational inertia**, and **vibration damping**.

| Component | Recommended Industrial Material | Prototyping Alternative (Lab) | Technical Justification |
| :--- | :--- | :--- | :--- |
| **Impeller (Hub + Blades)** | **LCP-GF30** (Liquid Crystal Polymer, 30% glass-fiber reinforced) or **PBT-GF30** | **PLA+ / PETG** or **Rigid SLA Resin** | High Young's modulus minimizes radial elongation under centrifugal force; excellent dimensional stability and fatigue resistance. |
| **Frame (Shroud)** | **PBT / ABS-GF30** (30% glass-fiber reinforced) | **PLA / ABS** (FDM 3D printing) | Optimal stiffness-to-cost ratio, good structural rigidity for case mounting, and flame-retardant compliance (UL 94 V-0). |
| **Bearings** | **Fluid Dynamic Bearing (FDB / SSO2)** or miniature ball bearings | Standard 608ZZ / 623ZZ ball bearings | Low friction, long service life ($> 150,000\text{ h}$ industrially), and quiet operation at 1800 rpm. |

---

## 4. Mean-Line Analysis (2D Cascade Analysis)

The two-dimensional cascade analysis at the mean radius ($r_m = 45.96\text{ mm}$) follows the methodology established by Dixon & Hall and Lewis (1996), using relative velocities ($\mathbf{w}$) and relative flow angles ($\beta$) measured from the axial direction.

### 4.1 Relative Velocity Triangles

In the rotor's relative frame of reference ($w_{\theta 1} = U$ and $w_{\theta 2} = U - c_{\theta 2}$):

* **Relative inlet flow angle:** $\beta_1 = \arctan\left(\frac{U}{c_x}\right) = \mathbf{71.95^\circ}$ (relative velocity $w_1 = \sqrt{c_x^2 + U^2} = \mathbf{9.11\text{ m/s}}$)
* **Relative outlet flow angle:** $\beta_2 = \arctan\left(\frac{U - c_{\theta 2}}{c_x}\right) = \mathbf{69.15^\circ}$ (relative velocity $w_2 = \mathbf{7.93\text{ m/s}}$)
* **Nominal flow deflection:** $\epsilon^* = \beta_1 - \beta_2 = \mathbf{2.80^\circ}$
* **Mean relative flow angle:** $\beta_\infty = \arctan\left(\frac{\tan\beta_1 + \tan\beta_2}{2}\right) = \mathbf{70.66^\circ}$

### 4.2 Initial Sizing via the Diffusion Factor ($DF = 0.50$)

To prevent boundary layer separation on the suction side of the blades, Lieblein's Diffusion Factor is initially constrained to $DF = 0.50$:

$$
DF = \left(1 - \frac{\cos\beta_1}{\cos\beta_2}\right) + \frac{1}{2}\left(\frac{s}{l}\right)\cos\beta_1\big(\tan\beta_1 - \tan\beta_2\big)
$$

For $Z = 8$ blades, the circumferential pitch at the mean radius is $s = \frac{2\pi r_m}{Z} = \mathbf{36.10\text{ mm}}$. Assuming a typical profile drag coefficient $C_D = 0.02$, the initial cascade yields:

* **Maximum pitch-to-chord ratio:** $s/l = \mathbf{5.400}$ (solidity $\sigma = l/s = 0.185$)
* **Minimum chord length:** $l_{\min} = \mathbf{6.68\text{ mm}}$
* **Ideal lift coefficient ($C_D = 0$):** $C_{L,0} = 2\left(\frac{s}{l}\right)\cos\beta_\infty(\tan\beta_1 - \tan\beta_2) = \mathbf{1.585}$
* **Actual lift coefficient ($C_D = 0.02$):** $C_L = C_{L,0} - C_D\tan\beta_\infty = \mathbf{1.528}$

**Critical Assessment:** Although $DF = 0.50$ satisfies the diffusion limit, the resulting lift coefficient ($C_L = 1.528$) is **too high** compared to the recommended limit ($C_L \le 1.0$). At low Reynolds numbers ($Re_D \approx 2.26 \times 10^4$), such excessive aerodynamic loading would trigger premature stall and severe efficiency drops.

### 4.3 Solidity Optimization for $C_L = 1.0$ and Blade Geometry (Howell's Rule)

To bring the lift coefficient down to **$C_L = 1.00$**, the pitch-to-chord ratio $s/l$ is reduced (increasing the chord length $l$ and solidity $\sigma$) by inverting the lift equation:

$$
\left(\frac{s}{l}\right)_{\text{opt}} = \frac{C_{L,\text{target}} + C_D \tan\beta_\infty}{2 \cos\beta_\infty (\tan\beta_1 - \tan\beta_2)} = \mathbf{3.601} \quad (\sigma = 0.278)
$$

Using **Howell's correlation** for a circular-arc camber line ($a/l = 0.5$, rotor exponent $n = 0.5$) and assuming zero incidence ($i = 0^\circ \implies \beta'_1 = \beta_1$), the camber angle ($\theta$), nominal deviation ($\delta^*$), blade angles ($\beta'_1, \beta'_2$), and stagger angle ($\xi$) are computed as:

$$
m = 0.23\left(\frac{2a}{l}\right)^2 + \frac{\beta_2}{500} = 0.3683 \quad ; \quad \theta = \frac{\epsilon^*}{1 - m(s/l)^n} \quad ; \quad \delta^* = m\theta\left(\frac{s}{l}\right)^n
$$

The table below compares the initial cascade ($DF = 0.50$) and the optimized design ($C_L = 1.00$) for **$Z = 8$ blades**:

| Cascade Parameter | Initial ($DF = 0.50$, $Z = 8$) | Optimized ($C_L = 1.00$, $Z = 8$) |
| :--- | :---: | :---: |
| Pitch-to-chord ratio ($s/l$) | 5.400 | **3.601** |
| Solidity ($\sigma = l/s$) | 0.185 | **0.278** |
| Circumferential pitch ($s$) | 36.10 mm | **36.10 mm** |
| Chord length ($l$) | 6.68 mm | **10.03 mm** |
| Diffusion Factor ($DF$) | 0.500 | **0.3765** |
| Lift coefficient ($C_L$, $C_D = 0.02$) | 1.528 | **1.000** |
| Camber angle ($\theta$) | 19.42° | **9.29°** |
| Deviation angle ($\delta^*$) | 16.63° | **6.50°** |
| Blade inlet angle ($\beta'_1$) | 71.95° | **71.95°** |
| Blade outlet angle ($\beta'_2 = \beta_2 - \delta^*$) | 52.53° | **62.66°** |
| Stagger angle ($\xi = \frac{\beta'_1 + \beta'_2}{2}$) | 62.24° | **67.31°** |

Optimizing the chord to $l = 10.03\text{ mm}$ lowers the Diffusion Factor to **$DF = 0.3765$**—providing a wide safety margin against flow separation—and reduces the required camber to **$9.29^\circ$**. This produces a clean, gently cambered airfoil section ready for the preliminary 2D CFD simulation and the upcoming 3D radial equilibrium design (Release 2).
