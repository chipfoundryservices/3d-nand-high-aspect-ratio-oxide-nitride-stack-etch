# Chapter 6: Ion Energy, Angular Spread & Bias Waveform Engineering

## Overview

Ion energy is the most expensive parameter in ON-stack etch. It buys a narrow angular spread, which lets ions reach the bottom of a deep feature. It also costs mask, heat, parts life, and arcing margin, and the ion energy distribution under a real bias waveform is much wider than its mean suggests. This chapter derives the energy a feature needs from its aspect ratio, compares the energy distributions produced by sinusoidal and tailored bias waveforms, and shows what pulsing changes. It closes with how energy is ramped through a recipe and what that does and does not save.

**Learning Objectives:**
- Derive the required ion energy for a target pass fraction and show that it scales as A²
- Compare the energy needs of holes and slots
- Compute the ion energy distribution under low-frequency sinusoidal bias and its effect on the pass fraction
- Explain how tailored (non-sinusoidal) waveforms narrow the distribution
- Evaluate high-energy, low-duty pulsed bias against continuous bias at the same average power
- Explain why ion energy is ramped with depth and what the ramp buys

---

## 6.1 How Much Energy a Feature Needs

### 6.1.1 Round Holes

From Chapter 3, with σ_θ² = T_⊥/E and θ_c = 1/A, the pass fraction into a round hole is f = 1 − exp(−E/(2T_⊥A²)). Solving for E:

```
E_req = 2 T_⊥ A² · ln[1 / (1 − f)]

T_⊥ = 0.5 eV:

  A       f = 0.44    f = 0.50    f = 0.70
──────────────────────────────────────────────
  56      1.8 keV     2.2 keV     3.8 keV
  93      5.0 keV     6.0 keV    10.4 keV
 120      8.4 keV    10.0 keV    17.3 keV
 150     13.0 keV    15.6 keV    27.1 keV
```

**Required energy scales as A².** Raising the aspect ratio from 93 to 120 (a 29% taller deck at the same width) needs 67% more energy for the same pass fraction. This is a hard physical wall. It explains why each generation has moved to higher bias power and why stacks are split into decks (Chapter 14).

### 6.1.2 Slots

A slot constrains only one axis: f = erf(θ_c/(σ_θ√2)), so

```
E_req = 2 T_⊥ A² · [erf⁻¹(f)]²

Slit at A = 56, f = 0.50: erf⁻¹(0.5) = 0.477
  E_req = 2 × 0.5 × 3136 × 0.2275 = 0.71 keV
```

A slit needs much less energy than a hole for the same pass fraction. In practice slits are still etched at multi-keV energies, because the higher pass fraction at those energies raises the bottom rate and lowers taper. The slit is run with energy to spare, while the hole is energy-limited.

### 6.1.3 What T_⊥ Really Is

T_⊥ is not just the ion temperature in the bulk plasma. It includes the transverse energy that ions gain from collisions in the sheath and from the curvature of the sheath edge over the feature. In a collisional multi-kV sheath (Chapter 5), the effective T_⊥ can be 0.5–1 eV or more. Lower pressure, a thinner sheath, and flat sheath edges reduce it. A recipe change that halves T_⊥ has the same effect on the pass fraction as doubling the energy, with none of the energy's costs.

---

## 6.2 Ion Energy Distributions

### 6.2.1 Low-Frequency Sinusoidal Bias

When ions cross the sheath in a small fraction of the bias period (Chapter 5, Section 5.3.3), each ion gains an energy close to the sheath voltage at the moment it enters. For a sinusoidal sheath voltage V(t) = V̄ + V₁ sin ωt, the ion energy distribution (IED) takes the arcsine form:

```
f(E) ∝ 1 / √(V₁² − (E − V̄)²),    V̄ − V₁ < E < V̄ + V₁

Bimodal, with peaks at the minimum and maximum sheath voltage.

Reference: V̄ = 5.0 kV, V₁ = 4.5 kV → E from 0.5 to 9.5 keV

Fraction below 2.5 keV:
  F(E) = 1/2 + (1/π) arcsin[(E − V̄)/V₁]
  F(2.5) = 0.5 + (1/π) arcsin(−0.556) = 0.5 − 0.1875 = 0.31
```

Nearly a third of the ions arrive below 2.5 keV, where their pass fraction into the reference hole is only 25%.

### 6.2.2 Effect on the Pass Fraction

The pass fraction is a concave function of energy, so a spread of energies with the same mean delivers fewer ions to the bottom than a single energy:

```
Reference hole (A = 93, T_⊥ = 0.5 eV):

IED                                   Mean E    Pass fraction (ion-weighted)
───────────────────────────────────────────────────────────────────────────
Monoenergetic                          5.0 keV   0.44
Arcsine 0.5–9.5 keV (LF sinusoid)      5.0 keV   0.40
```

The sinusoid loses about 9% of the bottom flux. Worse, the low-energy ions are the widest in angle and hit the upper wall, where they drive bow (Chapter 11). The high-energy ions, up to 9.5 keV, sputter the mask edge and parts more than their share.

### 6.2.3 Tailored Waveforms

A tailored bias waveform holds the wafer at a nearly constant negative voltage for most of the period. A short positive excursion then lets electrons reach the surface and neutralize the charge collected from the ions. Examples include pulsed-DC-like waveforms, ramp-compensated waveforms, and the sum of a fundamental and its harmonics.

```
Waveform                     IED shape                      Notes
───────────────────────────────────────────────────────────────────────────────
LF sinusoid                  Broad, bimodal                 Simple, mature, high power
LF + harmonic(s)             Narrower, skewed to high E     Moderate complexity
Tailored / pulsed-DC-like    Narrow peak (±5–10% of E)      Needs specialized
 (voltage ramp compensates                                  generators and matching;
 charging during the flat                                   wafer surface charging sets
 phase)                                                     the ramp
```

With a narrow IED, the whole ion flux is near the design energy. For the same mean energy, the bottom flux is higher, the upper-wall flux from low-energy ions is lower, and the high-energy tail that facets the mask is gone. The cost is generator complexity and a waveform that must be tuned to the wafer's dielectric charging, which changes with stack thickness and feature density.

---

## 6.3 Pulsed Bias

### 6.3.1 What Pulsing Does

In pulsed bias, the LF bias is switched on and off at 1–20 kHz with a duty cycle d (fraction of time on), often synchronized with source pulsing. During the off-time:

1. **Charge relaxes.** The sheath collapses, and electrons (and negative ions in electronegative fluorocarbon plasma) reach the wafer and the feature bottoms. They neutralize the positive charge built up during the on-time (Chapter 12).
2. **Polymer deposits.** Without ion bombardment, fluorocarbon deposits on the mask and walls. The off-time is a passivation step.
3. **Heat is lower** for the same peak power.

### 6.3.2 High Energy at Low Duty

The main use of pulsing in ON-stack etch is to reach **higher peak energy** at the same average power and heat load:

```
Case A (CW):     5 keV, 0.8 A, 100% duty → 4.0 kW average ion power
Case B (pulsed): 10 keV, 0.8 A during on, 50% duty → 8.0 kW peak, 4.0 kW average

Ion-enhanced yield scaling: Y ∝ √E (above a low threshold)

                              Case A          Case B
─────────────────────────────────────────────────────────────────
Pass fraction (A = 93)        0.44            0.69
Bottom ion flux (relative)    0.44            0.5 × 0.69 = 0.34
Yield per ion (relative)      1.00            √2 = 1.41
Bottom etch (flux × yield)    0.44            0.48   (+9%)
Top etch (A → 0, f ≈ 1)       1.00            0.5 × 1.41 = 0.71
Heat to the wafer             4.0 kW          4.0 kW
```

Case B etches 9% faster at the bottom and 29% slower at the top. **The ratio of bottom to top rate rises from 0.44 to 0.68.** In ARDE terms, A₀ grows: high-energy pulsing flattens ARDE. It also adds charge relief and off-time passivation. The cost is a longer etch through the upper part of the feature. Mask erosion depends on how the a-C sputter yield scales above a few keV, where it rises more slowly than √E, so pulsed high-energy operation usually reduces mask loss per micrometre at depth.

*(The √E yield scaling and the pass-fraction model are idealizations. The trend matches published HAR results, but the magnitude must be measured.)*

### 6.3.3 Choosing the Pulse Frequency

```
Off-time requirement           Typical value          Sets
───────────────────────────────────────────────────────────────────────
Charge relaxation              10–50 µs               Minimum off-time
Polymer deposition per cycle   ~0.01–0.05 nm per      Duty and frequency
                               off-period
Sheath re-formation transient  5–20 µs                Maximum frequency
                                                      (transients waste power)

Typical choice: 2–10 kHz, duty 30–60%
  5 kHz, d = 0.5 → 100 µs on, 100 µs off
```

---

## 6.4 The Costs of Energy

### 6.4.1 Where the Energy Goes

```
Cost                     Scaling with mean energy (fixed flux)     Chapter
────────────────────────────────────────────────────────────────────────────
Bias power               ∝ E                                       5
Wafer heat load          ∝ E                                       8
Mask sputtering          ∝ E^(0.3–0.5) at multi-keV                13
Mask facet → bow         Rises with E and with high-E tail         11
Edge ring and electrode  ∝ E^(0.5–1)                               9
 wear
Arcing risk              Rises steeply with V                      5
Sidewall damage at bow   Reflected ions carry more energy          11
```

### 6.4.2 Energy Versus Temperature

The angular-spread benefit of energy can also be obtained, partly, by reducing T_⊥ (lower pressure, flatter sheath) or by changing what reaches the bottom (cryogenic adsorbed etchant, Chapter 8). A recipe that is energy-limited should be checked against all three before more power is added.

---

## 6.5 Ramping Energy With Depth

### 6.5.1 Why Ramp

At shallow depth, A is small and almost every ion passes the cone at any energy. Extra energy there buys no pass fraction. It only sputters the mask edge, creating a facet that later reflects ions into the wall (bow). Deep in the feature, pass fraction rises steeply with energy. So recipes start at lower energy and raise it with depth:

```
Reference stepped bias (illustrative):

Stage    Depth (µm)    A at end    Mean energy    Pass fraction at end
──────────────────────────────────────────────────────────────────────
ME-1     0 – 3.0        33          3.0 keV        0.93
ME-2     3.0 – 6.0      67          4.5 keV        0.63
ME-3     6.0 – 8.4      93          6.0 keV        0.50
```

### 6.5.2 What the Ramp Does Not Save

In an ion-limited etch where both the stack rate and the mask erosion scale as √E, the mask consumed **per micrometre of depth** is set by chemistry, not by energy. Lowering the energy in ME-1 slows ME-1 and saves mask per minute, but not per micrometre. What the ramp saves is:

1. **Facet growth** in the early part of the etch, which reduces later bow
2. **High-energy tail damage** to the mask edge
3. **Heat load** during the long early steps

and what it buys, at depth, is pass fraction. The total etch time usually rises a few percent compared with running the deep-step energy throughout. Chapter 7 builds the full stage recipe.

### 6.5.3 Energy to Hold a Constant Pass Fraction

```
Holding f constant as A grows: E(A) = E_end × (A / A_end)²

To hold f = 0.50 at every depth of the reference hole:
  A = 33: E = 6.0 × (33/93)² = 0.76 keV
  A = 67: E = 6.0 × (67/93)² = 3.1 keV
  A = 93: E = 6.0 keV
```

A continuous quadratic ramp is the logical end point. Production recipes approximate it with three to six steps, because each change of bias is also a change in sheath, heat, and chemistry that must be stabilized (Chapter 7).

---

## 6.6 Summary & Key Takeaways

1. **Required energy scales as A².** E_req = 2T_⊥A² ln[1/(1 − f)]: 5 keV for 44% into the reference hole, 10 keV at A = 120.

2. **Slots need far less.** At A = 56 a slot needs about 0.7 keV for 50% pass; holes are the energy-limited feature.

3. **T_⊥ matters as much as E.** Collisions and sheath curvature broaden angles; halving T_⊥ is worth doubling E.

4. **Sinusoidal bias wastes ions.** The arcsine IED puts 31% of ions below 2.5 keV and lowers the reference pass fraction from 0.44 to 0.40.

5. **Tailored waveforms narrow the IED.** More bottom flux, less low-energy wall bombardment, less high-energy mask damage.

6. **High-energy, low-duty pulsing flattens ARDE.** At equal average power, 10 keV at 50% duty gives +9% bottom rate, −29% top rate, and charge relief.

7. **Ramp energy with depth for profile, not for mask per micrometre.** Low early energy limits facet and bow; high late energy buys pass fraction.

---

## Study Questions

1. Compute E_req for f = 0.60 into round holes at A = 80, 100, and 130 with T_⊥ = 0.6 eV.

2. An LF sinusoid gives V̄ = 6 kV and V₁ = 5 kV. What fraction of ions arrive below 3 keV? Explain qualitatively how the pass fraction compares with a monoenergetic 6 keV beam.

3. Compare CW 6 keV with pulsed 12 keV at 50% duty for the reference hole (T_⊥ = 0.5 eV), using the Section 6.3.2 method. Compute the relative bottom and top rates.

4. A slit at A = 60 is etched at 5 keV. Compute its pass fraction. What energy would a round hole need at the same A to match it?

5. Explain why lowering the ME-1 energy does not reduce mask consumption per micrometre in an ion-limited etch with √E scaling. What does it reduce, and why does that matter later in the etch?

---

**Previous Chapter:** [Chapter 5: Reactor & RF Systems](./05-reactor-rf-systems.md)  
**Next Chapter:** [Chapter 7: Recipe Architecture — Steps, Ramps & Deck Transitions](./07-recipe-architecture.md)

---

**Chapter 6 Development Status:** Complete  
**Version:** 1.0
