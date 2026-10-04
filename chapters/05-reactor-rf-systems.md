# Chapter 5: Reactor & RF Systems for Extreme-Aspect-Ratio Dielectric Etch

## Overview

The reactor for ON-stack etch has to do two things that pull against each other. It must accelerate ions to several kiloelectronvolts with a very narrow angular spread, and it must produce a dense, uniform, chemically controlled plasma that does not depend on that acceleration. The industry answer is a capacitively coupled plasma (CCP) with a very-high-frequency (VHF) source and a high-power low-frequency (LF) bias, pushed to bias powers of 10 kW and beyond. This chapter explains the choice, estimates the sheath that a multi-kilovolt bias creates, shows what limits uniformity, and covers the practical problems of delivering that much power to a wafer: matching, arcing, heat, and parts wear.

**Learning Objectives:**
- Explain why HAR dielectric etch uses dual- or multi-frequency CCP rather than inductively coupled plasma
- Estimate sheath thickness, ion transit time, and the collisionality of a multi-kV sheath
- Relate bias power, ion energy, and ion current at the wafer
- Estimate the VHF standing-wave non-uniformity and its dependence on source frequency
- Compute gas residence time in the reactor
- Describe arcing mechanisms at high bias and how they are detected and prevented

---

## 5.1 Why Capacitively Coupled Plasma

### 5.1.1 The Requirements

```
Requirement                           Reason
──────────────────────────────────────────────────────────────────────────────
Ion energy 2–10 keV at the wafer      Narrow angle; ion pass fraction (Ch. 3, 6)
Ion flux ~10¹⁵–10¹⁶ cm⁻² s⁻¹          Rate
Independent control of flux and       Tune chemistry without changing energy
 energy
Fluorocarbon-rich, low-dissociation   Polymer for mask and sidewall protection
 chemistry                            (C₄F₆ fragments, not just F)
Uniform within ~2% across 300 mm      Front uniformity (Ch. 3.7, 13)
Low pressure (10–40 mTorr)            Low collisionality in the sheath
```

### 5.1.2 CCP vs. ICP

```
                         Dual-frequency CCP              ICP with RF bias
─────────────────────────────────────────────────────────────────────────────────
Plasma density           10¹⁰–10¹¹ cm⁻³                  10¹¹–10¹² cm⁻³
Dissociation             Lower (VHF, small gap)          Higher (more F, fewer
                                                         large CF_x fragments)
Ion energy at kV bias    Natural: large-area wafer       Possible, but bias power
                         electrode, small gap            couples into a dense plasma
                                                         and heats the dielectric window
Polymer control          Good (large fragments)          Weaker for dielectric
Typical use              HAR dielectric, contacts        Silicon, metal, gate etch
```

HAR dielectric etch is dominated by CCP because fluorocarbon chemistry needs low dissociation, and multi-kV bias couples efficiently across a narrow gap to a large electrode.

---

## 5.2 The Frequency Stack

### 5.2.1 Roles of Each Frequency

```
Generator      Frequency (typical)    Power (ref.)   Role
───────────────────────────────────────────────────────────────────────────────
Source         40–100 MHz (ref. 60)   1–5 kW (3)     Plasma density, dissociation;
                                                     little ion energy
Bias           100 kHz–2 MHz          5–40 kW (12)   Ion energy; sheath voltage
               (ref. 400 kHz)
Second bias    2–13.56 MHz            0–5 kW         Shapes the ion energy
(optional)                                           distribution (Ch. 6)
```

At VHF, displacement current through the sheath is large and the sheath voltage stays small, so source power goes into electron heating, not into ion energy. At low frequency, the sheath voltage follows the applied voltage and ions are accelerated by most of it.

### 5.2.2 Why Low Bias Frequency

The ion transit time through the sheath, compared with the RF period, decides how the ion energy distribution looks (Chapter 6). At low bias frequency, ions cross the sheath in a small fraction of a period and gain energy close to the instantaneous sheath voltage. The peak of the distribution then reaches nearly the full sheath voltage. That maximizes the energy obtained per volt of RF and per watt.

---

## 5.3 The Multi-Kilovolt Sheath

### 5.3.1 Sheath Thickness

The Child-law sheath thickness:

```
s ≈ (√2/3) λ_D (2V_s / T_e)^(3/4)

λ_D = 7430 √(T_e[eV] / n_e[m⁻³])  m

Reference: n_e at sheath edge = 5×10¹⁶ m⁻³, T_e = 3 eV, mean sheath voltage V_s = 4 kV
  λ_D = 7430 × √(3 / 5×10¹⁶) = 7430 × 7.75×10⁻⁹ = 57.6 µm
  (2 × 4000 / 3)^(3/4) = 2667^(0.75) = 371
  s = 0.471 × 57.6 µm × 371 ≈ 10 mm
```

A multi-kilovolt sheath is about a centimetre thick. In a 25–35 mm gap, the wafer sheath takes up a third of the space.

### 5.3.2 Collisions in the Sheath

```
Gas density at 20 mTorr, 300 K: n_g = p/(k_B T) = 2.67 / (1.38×10⁻²³ × 300) = 6.4×10²⁰ m⁻³
Ion–neutral (charge-exchange + elastic) cross-section ~ 5×10⁻¹⁹ m² (illustrative)
Mean free path λ_i = 1/(n_g σ) = 3.1 mm

Collisions per ion across the sheath ≈ s/λ_i = 10/3.1 ≈ 3
```

Most ions undergo one or more collisions in the sheath. Each charge exchange creates a slow ion that is re-accelerated by only part of the sheath. The result is a low-energy, wide-angle tail in the ion distribution, which contributes little to the bottom and much to the upper wall (bow; Chapter 11). Lower pressure and denser plasma (thinner sheath) reduce collisions. This is one reason HAR etch runs at 10–30 mTorr rather than higher.

### 5.3.3 Ion Transit Time

```
Fast ion velocity (Ar⁺, 4 keV): v = √(2E/m) = √(2 × 4000 × 1.60×10⁻¹⁹ / 6.64×10⁻²⁶)
                                = 1.39×10⁵ m/s
Transit time across the sheath: τ_i ≈ 3s / v ≈ 3 × 0.010 / 1.39×10⁵ = 0.22 µs

400 kHz period: 2.5 µs → τ_i / T_RF ≈ 0.09
  → ions see a nearly instantaneous voltage: broad, bimodal IED

13.56 MHz period: 0.074 µs → τ_i / T_RF ≈ 3
  → ions average over cycles: narrow IED near the mean voltage
```

Heavier ions (CF₃⁺, 69 amu; C₂F₄⁺, 100 amu) are slower and average more. The ion energy distribution is therefore a mixture of shapes. Chapter 6 develops this into IED design.

---

## 5.4 Power, Voltage, and Current at the Wafer

### 5.4.1 Where Bias Power Goes

```
Reference: 12 kW bias at 400 kHz

Into ions accelerated to the wafer   ≈ 4.0 kW  (33%)
Into ions at the grounded/upper      ≈ 1.5 kW
 surfaces and the ring
Electron heating, sheath dissipation ≈ 3.5 kW
Losses in match, cables, electrode   ≈ 3.0 kW
 and ESC (capacitive, resistive)
```

*(Illustrative split; it varies with geometry and frequency.)*

### 5.4.2 Ion Current and Energy

```
Ion power to the wafer P_i = 4.0 kW, mean ion energy 5 keV
  Ion current I_i = P_i / E_i = 4000 / 5000 = 0.80 A
  Current density = 0.80 / 707 cm² = 1.13 mA/cm²
  Ion flux Γ_i = 1.13×10⁻³ / 1.60×10⁻¹⁹ = 7.1×10¹⁵ cm⁻² s⁻¹
  Heat flux to the wafer from ions = 4000 / 707 = 5.7 W/cm²
```

The ion heat flux is several times larger than in a conventional etch. Chapter 8 shows how it sets the wafer temperature.

### 5.4.3 Scaling Bias Power

To raise mean ion energy at constant ion current, bias power must rise in proportion. The ion current is set mostly by the source (plasma density). Raising energy from 5 to 8 keV at the same current needs 60% more ion power, about 19 kW of bias in the reference split. Raising energy also thickens the sheath (s ∝ V^(3/4)), which raises collisionality unless pressure is reduced.

---

## 5.5 Uniformity

### 5.5.1 Standing Waves at VHF

At VHF, the electrode dimensions approach a significant fraction of the effective wavelength in the plasma-loaded gap. The RF voltage across the electrode then varies roughly as J₀(kr), peaking at the centre:

```
V(r)/V(0) ≈ J₀(2π r / λ_eff)

λ_eff is the free-space wavelength reduced by the plasma loading (illustrative:
λ₀/2 at 60 MHz)

60 MHz:   λ₀ = 5.0 m, λ_eff ≈ 2.5 m; at r = 150 mm, kr = 0.377 → J₀ = 0.965  (−3.5%)
120 MHz:  λ₀ = 2.5 m, λ_eff ≈ 1.25 m; kr = 0.754 → J₀ = 0.863  (−14%)
```

Higher source frequency gives denser plasma at lower dissociation but worsens the centre-high profile. Reactors compensate with shaped (lens) electrodes, segmented power feeds, and radial gas and temperature zones.

### 5.5.2 The Wafer Edge

At the wafer edge, the sheath must bend from the wafer to the edge ring. Any step in sheath thickness tilts the ion trajectories. The edge ring's height and material are chosen to make the sheath flat, and ring wear changes it over time. Edge tilt is treated in Chapter 9 (hardware) and Chapter 12 (effect on the feature).

---

## 5.6 Gas Flow and Residence Time

```
Reference: gap 30 mm, electrode diameter 340 mm
  Plasma volume V ≈ π × 0.17² × 0.030 = 2.7×10⁻³ m³ (2.7 L)
  Total flow Q = 300 sccm = 300 × 1.69×10⁻³ = 0.51 Pa·m³/s
  Pressure p = 20 mTorr = 2.67 Pa

  Residence time τ = pV / Q = 2.67 × 2.7×10⁻³ / 0.51 = 14 ms
```

A short residence time limits the build-up of etch products in the gas phase and keeps the chemistry close to the feed. The feature's own product build-up (Chapter 3, Section 3.8) is a separate, local problem that the chamber residence time does not solve.

Confinement rings around the electrode gap keep the plasma off the chamber walls and reduce wall-related drift (Chapter 9). They must pass gas freely enough to hold the residence time at high flow.

---

## 5.7 Arcing at High Bias

### 5.7.1 Where Arcs Happen

At kilovolt bias, any weak point in the electrical path can break down:

```
Location                          Mechanism                           Consequence
──────────────────────────────────────────────────────────────────────────────────────
Wafer backside / He holes         Gas breakdown in He passages        ESC damage,
                                  (Paschen minimum at Torr·mm)        particles, wafer
                                                                      scrap
Wafer bevel / edge                Field concentration at the bevel;   Bevel damage,
                                  film flakes                         particles
Through the wafer (micro-arcs)    Charge build-up on thick dielectric Local craters in
                                  stack; breakdown at defects         the array
ESC dielectric                    Ageing, contamination               ESC failure
Edge ring / coupling ring gaps    Field in gaps                       Ring damage,
                                                                      tilt shift
```

### 5.7.2 The Stack Makes It Worse

The wafer carries 8–17 µm of dielectric. During etch, charge accumulates on the surface and in the features, and the potential across the stack can approach its breakdown strength at defects (particles, voids, thin spots). A local discharge through the stack leaves a crater that kills the die and can spray particles.

### 5.7.3 Prevention and Detection

```
Measure                                  Purpose
───────────────────────────────────────────────────────────────────────
Ramped bias turn-on and turn-off         Avoid transient overvoltage
Pulsed bias with off-time discharge      Relieve accumulated charge (Ch. 6)
He hole geometry and ceramic plugs       Keep He passages below Paschen breakdown
Fast arc detection (V/I transients,      Stop or reduce bias within µs;
 reflected-power spikes, optical)        flag wafer for inspection
Bevel film control (bevel etch/clean)    Remove loose film at the edge
Particle control before etch             Remove defects that seed breakdown
```

Arc events are a key fault-detection (FDC) parameter for HAR chambers (Chapter 15).

---

## 5.8 Platforms and Matching

A HAR dielectric etch platform carries four to six chambers around a vacuum transfer module. Because each wafer spends 30–45 minutes in a chamber, transfer time is small and the platform throughput is set almost entirely by chamber count and etch time.

```
Reference: 6 chambers, 40.6 min etch + 4 min overhead per wafer (WAC, transfer,
           stabilization)
  Per chamber: 60 / 44.6 = 1.35 wafers/h
  Per platform: 8.1 wafers/h
```

Matching between chambers is a production requirement: every chamber must produce the same depth, CD, and tilt within the APC correction range. The RF path (cable lengths, match networks, delivered-power calibration at the electrode) is the most common source of mismatch, followed by edge-ring and electrode part variation (Chapter 9).

---

## 5.9 Summary & Key Takeaways

1. **CCP with VHF source and LF bias is the standard.** It separates density from energy, keeps dissociation low for fluorocarbon chemistry, and couples multi-kV bias efficiently.

2. **The sheath is about a centimetre thick.** At 4 kV and 5×10¹⁶ m⁻³, s ≈ 10 mm, with about three ion collisions across it at 20 mTorr.

3. **Low bias frequency gives instantaneous-response ions.** At 400 kHz, transit time is 9% of the period, so the IED is broad and reaches near the full sheath voltage.

4. **Ion power is a third of bias power.** 12 kW of bias delivers about 4 kW to the wafer as ions: 0.8 A at 5 keV, 7.1×10¹⁵ cm⁻² s⁻¹, 5.7 W/cm² of heat.

5. **VHF trades uniformity for density.** The standing-wave dip at the edge grows from about 3.5% at 60 MHz to 14% at 120 MHz in the illustrative model.

6. **Arcing is a stack problem.** Kilovolt bias across a thick dielectric stack needs ramped bias, pulsing, careful He paths, and fast arc detection.

---

## Study Questions

1. Compute the sheath thickness for n_e = 1×10¹⁷ m⁻³, T_e = 3.5 eV, and V_s = 6 kV. How many charge-exchange mean free paths is it at 15 mTorr (σ = 5×10⁻¹⁹ m²)?

2. Compute the transit time of a CF₃⁺ ion (69 amu) at 5 keV across a 10 mm sheath. Compare with the periods at 400 kHz and 2 MHz.

3. A recipe raises mean ion energy from 5 to 7 keV at constant ion current. With the reference power split, estimate the new bias power and ion heat flux.

4. Using λ_eff = λ₀/2, compute the centre-to-edge voltage ratio at r = 150 mm for 40 MHz and 80 MHz sources.

5. A chamber runs 350 sccm at 15 mTorr with a 2.5 L plasma volume. Compute the residence time. How would halving the flow change it?

---

**Previous Chapter:** [Chapter 4: ON Etch Chemistry](./04-on-etch-chemistry.md)  
**Next Chapter:** [Chapter 6: Ion Energy, Angular Spread & Bias Waveform Engineering](./06-ion-energy-waveforms.md)

---

**Chapter 5 Development Status:** Complete  
**Version:** 1.0
