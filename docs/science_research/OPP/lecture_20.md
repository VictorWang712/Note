---
comments: true
---

# Lecture 20 - Battery Modelling

- Speaker: Prof. Charles Monroe

## The Importance of Electrochemical Storage Devices

Electrochemical devices facilitate the efficient storage and conversion of energy, rendering portable electronics feasible.

Prior to the widespread adoption of electrical generators, the *voltaic pile* (a copper-zinc battery) served as the sole available source of electricity.

All electrochemical devices are underpinned by a common set of physical principles, resulting in models with analogous structures across different device types.

## Ragone Plot

### Storage Applications Range from mW to MW

Electrochemical devices are ubiquitous today, spanning a broad spectrum of energy and power scales.

They are increasingly integral to the *green revolution*, including electric and hybrid vehicles, hydrogen-powered cars, and grid energy storage systems.

### Demand for Battery Models

- Design
  - Predicting the **behaviour** of new chemical compositions
  - Designing **electrodes**
  - Estimating the **heat** generation of a cell
  - Designing a **balancing** system
  - **Matching** cells within a pack
- Estimation
  - State of **charge**
  - **Temperature**
  - State of **health**
  - Power capability
- System integration and control
  - Determining the **efficiency** map
  - Identifying the **optimal (dis)charge profile**
  - Estimating the **lifespan** of batteries
  - Determining the **voltages** encountered by the inverter

### The Ragone Plot: Comparing Performance Across Devices

It facilitates the matching of a **device** to a specific **application**.

Ragone plots illustrate the relationship between **energy density** and **power density** for devices; in the context of a car, this corresponds to **range** versus **acceleration**.

Density can be expressed as **gravimetric** (per kilogram) or **volumetric** (per litre); in automotive applications, low volume may be prioritised over low weight.

The primary objective of energy storage research is to advance devices towards the upper right quadrant of the Ragone plot.

### A Simplified Perspective on the Ragone Plot

Assume that the device operates at a constant maximum voltage $V_{0}$, determined by its chemical composition.

When a current $I$ is drawn from the device, the delivered voltage $V$ is given by

$$V(I) = V_{0} - IR_{\text{internal}}$$

The power $P$ delivered by the device can be expressed as

$$P(I) = IV(I) = I(V_{0} - IR_{\text{internal}})$$

If the device holds a charge $Q$, it can deliver power for a duration $t = \frac{Q}{I}$.

The energy $E$ delivered by the device is given by $E = Pt = Q(V_{0} - IR_{\text{internal}})$.

The Ragone plot expresses energy as a function of power, i.e., $E(P)$. From the equations $E(I) = Q(V_{0} - IR_{\text{internal}})$ and $P(I) = I(V_{0} - IR_{\text{internal}})$, we can derive

$$P(E) = \frac{(QV_{0} - E)E}{Q^{2}R_{\text{internal}}}$$

By solving for $E$ using the quadratic formula, we can qualitatively explain the characteristic shapes of Ragone plots.

$$\frac{E}{m}(\frac{P}{m}) = \frac{QV_{0}}{2m} \left( 1 + \sqrt{1 - \frac{4PR_{\text{internal}}}{V_{0}^{2}}} \right)$$

To enhance battery performance, the following objectives are pursued:

- Raise **specific capacity** $\frac{Q}{m}$
- Raise **open-circuit voltage** $V_{0}$
- Raise **specific internal conductance** $\frac{1}{mR_{\text{internal}}}$

## Introduction to Batteries: Chemistries and Physical Mechanisms

### Batteries Come in a Wide Variety of Chemistries

Chemistry determines **specific capacity** and **open-circuit voltage**.

**Primary cells** are designed for single use, offering high energy density and extended **shelf life**.

- $\ce{Zn}$-$\ce{C}$/$\ce{MnO2}$ dry cell (*Leclanché*)
- $\ce{Zn}$-$\ce{MnO2}$ wet cell (*Alkaline*)
- $\ce{Zn}$-$\ce{Ag2O}$
- $\ce{Li}$-$\ce{SO2}$

**Secondary cells** are rechargeable and are chosen for their energy/power density as well as their **cycle life**.

- $\ce{Pb}$-$\ce{PbSO4}$ (*lead-acid*)
- $\ce{Li}$-$\ce{LiCoO2}$ (*lithium-ion*)
- $\ce{Ni}$-MH (*nickel-metal hydride*)
- $\ce{Ni}$-$\ce{Cd}$ (*nickel-cadmium*)

### Lead-Acid Battery Chemistry

> Negative electrode, $U^{\ominus} = -0.36 \text{V}$
>
> $$\ce{Pb + HSO4- <=> PbSO4 + H+ + 2e-}$$
>
> Positive electrode, $U^{\ominus} = 1.39 \text{V}$
>
> $$\ce{PbO2 + HSO4- + 3H+ + 2e- <=> PbSO4 + 2H2O}$$
>
> Full cell, $U^{\ominus} = 2.05 \text{V}$
>
> $$\ce{Pb + PbO2 + 2H2SO4 <=> 2PbSO4 + 2H2O}$$

Approximately 60% of the world's storage batteries are lead-acid, utilised in vehicle starting systems, off-grid energy solutions, and uninterruptible power supply (UPS) applications.

A cell contains porous **lead** negative and **lead dioxide** positive electrodes.

The electrolyte, which participates in the reaction, consists of aqueous sulfuric acid.

During discharge, **lead sulfate** deposits form on both electrodes, and the acidity of the electrolyte decreases.

## The Open-Circuit Potential

### Lead-Acid Battery Thermodynamics: The Nernst Equation

In our simplified model for deriving the Ragone plot, we assumed $V_{0}$ to be constant. However, in practice, the **open-circuit voltage** varies with the battery's **state of charge**.

For simple electrochemical reactions, the *Nernst Equation* describes the variation of the open-circuit voltage $U$ with composition at an absolute temperature $T$.

$$U = U^{\ominus} - \frac{RT}{nF} \ln \left( \frac{\prod(\text{product activities})}{\prod(\text{reactant activities})} \right)$$

The Nernst Equation can be applied to analyse the lead-acid battery

$$U = 2.05 \text{V} - \frac{RT}{2F} \ln \left( \frac{a_{\ce{H2SO4}}^{2} a_{\ce{H2O}}^{2}}{a_{\ce{Pb}} a_{\ce{PbO2}} a_{\ce{H2SO4}}^{2}} \right)$$

Here, the acid concentration can be utilised to determine the state of charge, denoted as $X$.

$$X = \frac{c}{c_{\max}}$$

### Open-Circuit Voltage Curve for Lead-Acid Batteries

For a lead-acid battery, the open-circuit voltage $U$ varies with the state of charge $X$ at $298 \text{K}$ according to

$$U = 2.05 \text{V} + 0.0257 \text{V} \cdot \ln X$$

To determine the maximum remaining energy at a given $X$, this curve can be integrated as follows:

$$E_{\text{remaining}}(X) = \int_{0}^{Q_{\max}X} U(Q)\text{d}Q = 2Fc_{\max} \int_{0}^{X} U(X)\text{d}X = 2Fc_{\max}U_{0}X + 2c_{\max}RT(X \ln X - X)$$

### Lithium-ion Chemistry: Host Electrodes

Lithium-ion chemistry operates uniquely, with solid electrodes undergoing compositional changes via **intercalation** processes, wherein $\ce{Li}$ atoms are inserted between the layers of crystal structures within the electrodes.

$\ce{Li+}$ ions are transported through the electrolyte, ideally without the involvement of solvent in the reactions.

> Negative electrode, $U^{\ominus} = 0.1$-$1.3 \text{V}$ vs. $\ce{Li}$
>
> $$\ce{y Li+ + C +} y \ce{e- <=> Li_{y}C}$$
>
> Positive electrode, $U^{\ominus} = 3.5$-$4.5 \text{V}$ vs. $\ce{Li}$
>
> $$\ce{LiCoO2 <=> Li_{1 - x}CoO2 + x Li+ +} x \ce{e-}$$
>
> Full cell, $U^{\ominus} = 2.7$-$4.2 \text{V}$ vs. $\ce{Li}$
>
> $$\ce{LiCoO2 +} x/y \ce{C <=>} x/y \ce{CLi_{y} + Li_{1 - x}CoO2}$$

### Many Useful $\ce{Li}$ Intercalation Materials

The dominant **negative** electrode material is **graphite** ($\ce{TiO3}$ and $\ce{Si}$ are also used).

A variety of **lithium-metal-oxide positive** electrode materials are utilised, including $\ce{LiCoO2}, \ce{LiMn2O4}, \ce{LiNiCoAlO2}, \ce{LiNiMnCoO2},$ and $\ce{LiFePO4}$.

### Cell Constituents Need to be Stable

The electrolyte in a $\ce{Li}$-ion cell comprises

- **Solvent**, typically a non-aqueous organic liquid or polymer, as water is unstable at high voltages
- **Lithium salt**, composed of lithium and a counterion, such as $\ce{LiPF6}, \ce{LiBF4},$ or $\ce{LiClO4}$

One reason for the upper voltage limit is to prevent the oxidation of the electrolyte.

The current collectors include:

- **Aluminium** is employed at the positive electrode due to its stability at high potentials, despite reacting with lithium below $0.6 \text{V}$.
- **Copper** is utilised at the negative electrode.

### The Nernst Equation as the Basis for Open-Circuit Voltage (OCV)

Host materials exhibit multiple stable stages of lithiation, indicating that several half-reactions occur during the intercalation process.

Beginning with the Nernst Equation, for the $i$th stable voltage (*stage*), the activity of reactants is proportional to $1 - x_{i}$ (the fractional occupancy of lattice sites available for that stage), while the activity of products is proportional to $x_{i}$.

$$U_{i} = U_{i}^{\ominus} - \frac{RT}{nF} \ln \left( \frac{x_{i}}{1 - x_{i}} \right)$$

This can be extended to incorporate the interaction energy $\gamma$ between other stages

$$U_{i} = U_{i}^{\ominus} - \frac{\gamma U_{i}}{F} (1 - 2x_{i}) - \frac{RT}{nF} \ln \left( \frac{x_{i}}{1 - x_{i}} \right)$$

At equilibrium, $U_{i} = U$ for all stages; solving for $x_{i}$ and summing over $i$ yields

$$x(U) = \sum_{i} \frac{\delta x_{i}}{1 + e^{\frac{F(U_{i}^{\ominus} - U_{i}) a_{i}}{RT}}}$$

### The *Stairstep* Potentials of Lithium-Intercalation Electrodes

The full open-circuit voltage model is therefore given by:

$$x_{PE}(E_{PE}^{OC}) = \sum_{i = 1}^{4} \frac{\Delta x_{PE, i}}{1 + e^{\frac{(E_{PE}^{OC} - E_{0, PE, i}) a_{PE, i} e}{kT}}}$$

$$x_{NE}(E_{NE}^{OC}) = \sum_{i = 1}^{4} \frac{\Delta x_{NE, i}}{1 + e^{\frac{(E_{NE}^{OC} - E_{0, NE, i}) a_{NE, i} e}{kT}}}$$

$$E_{\text{cell}}^{OC} = E_{PE}^{OC} - E_{NE}^{OC}$$

The diagram demonstrates the combination of four distinct Nernst-style terms, summed in the $x$-direction, to achieve a close fit to the measured positive electrode OCV.

## Physics-Based Lithium-Ion Modeling: The Single-Particle Model

To rationalise the Ragone plot, we conceptualised a battery system in a highly simplified manner, as a **voltage source** with internal **losses**.

We have observed that the voltage supplied by the source varies with the state of charge, and several models have been proposed to explain this phenomenon.

The internal resistance can also be explained by physical processes occurring at the molecular scale.

$$R_{\text{internal}} = R_{\text{ohmic}} + R_{\text{reaction}}^{+} + R_{\text{reaction}}^{-} + R_{\text{diffusion}}$$

### Measuring Impedance Spectra to Isolate Scales

Electrochemical impedance spectroscopy (EIS) applied to a battery yields a typical frequency response, as illustrated opposite.

For engineering applications, such as battery management systems (BMS), the focus is typically on dynamics below $1 \text{Hz}$.

A model that captures the sub-$1 \text{Hz}$ **solid diffusion** dynamics is desirable, as it is valuable for control and estimation purposes.

### Single-Particle Model (SPM) for Impedance

We aim to develop a more principled model that accounts for the internal processes within the cell.

The simplest confined shape for an electrode particle is a sphere.

Therefore, we model the following:

- Diffusion in spheres
- Nonlinear reaction kinetics
- Open circuit potential

This approach is termed the single-particle model (SPM).

#### The Butler-Volmer Equation Governs Reactions

The Butler-Volmer (BV) kinetic equation is given by

$$j_{i} = \frac{2 j_{0, i}}{F} \sinh \left( \frac{F \eta_{i}}{2RT} \right)$$

The exchange current density $j_{0}^{i} = k_{i} F \sqrt{c_{e}c_{i}^{\text{surf}}(c_{i}^{\max} - c_{i}^{\text{surf}})}$

The BV equation can be inverted

$$\eta_{i} = \frac{2RT}{F} \text{arcsinh} \left( \frac{F j_{i}}{2j_{0, i}} \right) $$

yielding overpotential as an explicit function of current density.

#### Transport Follows Spherical Diffusion in Particles

Diffusion within each intercalation particle $i$, with radius $R_{i}$, is described by

$$\frac{\partial c_{i}}{\partial t} = \frac{D_{i}}{r_{i}^{2}} \frac{\partial}{\partial r_{i}} \left( r_{i}^{2} \frac{\partial c_{i}}{\partial r_{i}} \right)$$

The surface boundary condition is governed by the reaction rate, while the gradient at the centre is zero due to symmetry; the initial condition is specified by $c_{0}$.

$$\left. \frac{\partial c_{i}}{\partial r_{i}} \right|_{r_{i} = 0} = 0, \left. D_{i} \frac{\partial c_{i}}{\partial r_{i}} \right|_{r = R_{i}} = - j_{i}$$

$$c_{i}(0, r_{i}) = c_{0}$$

The reaction rates are related to the current $I$ flowing through the cell

$$j_{-} = \frac{I}{a_{-} \delta_{-} \mathcal{FA}}, j_{+} = \frac{- I}{a_{+} \delta_{+} \mathcal{FA}}$$

#### Transport is Modelled by Spherical Diffusion

The equation can be simplified by non-dimensionalising certain variables

$$\bar{r} = \frac{r_{i}}{R_{i}}, x_{i} = \frac{c_{i}}{c_{\max}}, \bar{x_{i}} = x_{i} - x_{0}, x_{0} = \frac{c_{0}}{c_{\max}}$$

A change of variable is introduced, $\bar{u_{i}} = \bar{r} \bar{x_{i}}$, yieldingg

$$\frac{\partial \bar{u_{i}}}{\partial t} = \frac{1}{\tau_{i}^{d}} \frac{\partial^{2} \bar{u_{i}}}{\partial \bar{r_{i}}^{2}}$$

Subject to the following boundary and initial conditions:

$$\left. \bar{u_{i}} \right|_{r_{i} = 0} = 0, \left. \frac{\partial \bar{u_{i}}}{\partial \bar{r}} \right|_{\bar{r} = 1}, \left. - u \right|_{\bar{r} = 1} = \frac{- \tau_{i}^{d}}{3Q_{i}^{th}} I$$

Substituting $\bar{u_{i}} = \bar{r} \bar{x_{i}}$ and evaluating at $\bar{r} = 1$ yields

$$H_{i}^{d} = \frac{\bar{X_{i}}^{s}(s)}{I(s)} = \frac{\tau_{i}^{d}}{3Q_{i}^{th}} \frac{\tanh \sqrt{s \tau_{i}^{d}}}{\tanh \sqrt{s \tau_{i}^{d}} - \sqrt{s \tau_{i}^{d}}}$$

We now possess a transfer function that relates the current to the electrode surface concentration, expressed as a ratio of the maximum concentration within the electrode.

The battery **terminal voltage** can be expressed as

$$V = U_{+}(x_{+}^{s}) - U_{-}(x_{i}^{s}) + \eta_{+} - \eta_{-}$$

#### After Linearisation We Get Low-Frequency Impedance

Recall that the impedance is given by

$$\frac{\bar{V}(s)}{I(x)} = \alpha_{+, 0} H_{+}^{d}(s) - \alpha_{-, 0} H_{-}^{d}(s) - R_{ct, 0}$$

It is important to note that:

- the $R_{ct}$ term induces instantaneous voltage changes in response to current variations
- $R_{ct}$ is a function of SOC
- at lower frequencies, the system behaves as a capacitor (linearised OCV)
- the diffusion dynamics are *attenuated* by the OCV slopes, resulting in apparent changes with SOC

#### A Good Explanation of Low-Frequency Behaviour

As evidenced by measured data, behaviour at frequencies below $1 \text{Hz}$ is dominated by **diffusion** and **OCV changes**.

When linearised, the OCV changes manifest as a capacitance.

In many applications, **higher frequency effects** are neglected, although double-layer capacitance must be considered in such cases.

Time-domain results exhibit comparable behaviour.
