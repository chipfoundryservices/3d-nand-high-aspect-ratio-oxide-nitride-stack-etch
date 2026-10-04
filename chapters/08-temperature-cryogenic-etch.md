# Chapter 8: Wafer Temperature, Cryogenic Etch & Heat Flow

## Overview

A HAR stack etch delivers several kilowatts of ion power to the wafer, and the wafer temperature that results controls polymer deposition, lateral etch, adsorption, and the oxide/nitride rate ratio. In cryogenic processes it also controls the supply of etchant to the bottom of the feature. This chapter follows the heat from the plasma to the coolant and shows where the temperature drops occur. It then examines how temperature changes the etch of each film, what cryogenic operation requires of the chuck, and why bowed wafers make all of this harder.

**Learning Objectives:**
- Compute the heat flux to the wafer and the temperature drop across each layer of the thermal path
- Estimate the wafer's thermal time constant and its response to recipe steps and pulsing
- Describe how wafer temperature changes polymer, lateral etch, and the rate ratio
- Quantify the temperature sensitivity of adsorption in cryogenic etch and the uniformity it demands
- Estimate the electrostatic clamping pressure needed to flatten a bowed wafer, and the bow at which chucking fails
- Describe the hardware and handling requirements of cryogenic chucks

---

## 8.1 The Heat Load

### 8.1.1 Sources

```
Source                                  Reference (W/cm²)
──────────────────────────────────────────────────────────
Ion kinetic energy (4.0 kW / 707 cm²)   5.7
Ion neutralization, radical             0.3
 recombination at the surface
Radiation and hot neutrals              0.3
─────────────────────────────────────────────────────────
Total                                   6.3 W/cm² = 63 kW/m²
```

This is several times the heat flux of a conventional etch. It changes with each recipe step, because bias power changes (Chapter 7: 6 kW in CAP to 15 kW in ME-3).

### 8.1.2 The Thermal Path

Heat flows from the wafer surface through the stack, the silicon, the helium-filled gap at the back of the wafer, the electrostatic chuck (ESC) ceramic, and into the cooled base:

```
Layer                          Thickness   k or h (illustrative)   ΔT at 63 kW/m²
──────────────────────────────────────────────────────────────────────────────────
ON stack                        8.4 µm     k ≈ 1.2 W/m·K           0.4 K
Silicon wafer                   775 µm     k ≈ 130 W/m·K           0.4 K
Backside He gap (20 Torr)       ~5–10 µm   h ≈ 2,500 W/m²·K        25 K
ESC ceramic (Al₂O₃, AlN)        ~1 mm      k ≈ 30 W/m·K            2.1 K
Bond and base to coolant        —          —                        2–5 K
──────────────────────────────────────────────────────────────────────────────────
Wafer surface above coolant                                         ≈ 30 K
```

**The helium gap dominates.** The stack and the wafer conduct heat well enough that the wafer is nearly isothermal through its thickness. The wafer temperature is set by the heat flux divided by the backside conductance, plus the chuck setpoint.

```
Reference: chuck surface 20 °C, ΔT_He ≈ 25 K → wafer ≈ 45–50 °C during ME-3
```

### 8.1.3 Backside Conductance

The He conductance depends on the gas pressure (in the transition regime between molecular and continuum flow), the surface roughness of the chuck, and the contact fraction. Raising He pressure raises h, but the clamping pressure must exceed the He pressure, or the wafer lifts and leaks:

```
He pressure 20 Torr = 2.7 kPa
Required clamping pressure > 2.7 kPa with margin (typically 2–5×)
```

---

## 8.2 How Fast the Wafer Responds

### 8.2.1 Thermal Time Constant

```
τ = ρ c t / h

Silicon: ρ = 2330 kg/m³, c = 700 J/kg·K, t = 775 µm
  ρ c t = 1264 J/m²·K
  τ = 1264 / 2500 = 0.5 s
```

The wafer follows each step change in bias power within a few seconds. The ESC body has a much longer time constant (tens of seconds to minutes), so the chuck surface temperature drifts during long high-power steps unless the coolant loop is controlled tightly.

### 8.2.2 Steps and Pulses

```
Recipe step change (ME-2 → ME-3, bias 12 → 15 kW):
  Ion heat flux rises by about 25% → ΔT_He rises from ~20 K to ~25 K
  Wafer warms by ~5 K within ~2 s

Bias pulsing at 5 kHz:
  Period 0.2 ms ≪ τ → wafer sees the average power; no thermal ripple
  (the surface of the feature bottom does see transient heating, but over
   nanometres, not the wafer)
```

Recipes that change bias between steps can also change the chuck setpoint to hold the wafer temperature, or accept the change and tune chemistry around it.

---

## 8.3 How Temperature Changes the Etch

### 8.3.1 Effects on Each Mechanism

```
Mechanism                        Lower wafer temperature →
────────────────────────────────────────────────────────────────────────────
Fluorocarbon sticking            Higher; more polymer on walls and mask
Lateral etch of the wall         Lower; less bow
Neutral adsorption               Higher (exponential in 1/T); more etchant
                                 delivered by surface transport at depth
Product desorption               Lower; risk of redeposition and salt
                                 formation (nitride + HF)
Mask erosion                     Lower (more polymer protection)
Rate ratio ρ                     Usually falls: nitride is more polymer-
                                 limited (Ch. 4), so extra polymer hurts it
                                 more
```

### 8.3.2 Illustrative Sensitivities (Conventional Process, 20–60 °C)

```
Quantity                     Sensitivity per +1 K at the wafer
───────────────────────────────────────────────────────────────
R_ox                         +0.10%
R_N                          +0.25%
ρ                            +0.15% (≈ +0.0014)
Top CD (bow)                 +0.3 nm
Mask erosion                 +0.2%
```

A 10 K radial temperature difference from centre to edge would change ρ by 0.014, bow by 3 nm, and mask erosion by 2%. Multi-zone ESCs (from 2–4 radial zones up to many dozens of independently controlled zones) are used to flatten the wafer temperature and to tune CD radially on purpose (Chapter 15).

---

## 8.4 Cryogenic ON-Stack Etch

### 8.4.1 Operating Window

```
                         Conventional         Cryogenic
─────────────────────────────────────────────────────────────────────
Chuck setpoint           0 to +40 °C          −40 to −80 °C
Wafer during etch        +30 to +70 °C        −20 to −60 °C
Chemistry                Fluorocarbon/HFC     HF-based (HF or H₂ + F
                         with O₂, NF₃         sources) with fluorocarbon
                                              and additives
Etchant supply at depth  Ion-driven; gas-     Adsorbed layer, surface
                         phase radicals       transport
                         mostly lost
Published rate at depth  Reference            2–3× (reported)
```

### 8.4.2 Why Uniformity Must Be Tighter

The adsorption constant K ∝ exp(E_ads/k_BT) changes much faster with temperature at low temperature:

```
d ln K / dT = −E_ads / (k_B T²)

E_ads = 0.35 eV:
  T = 293 K (+20 °C):  −4.7% per K
  T = 243 K (−30 °C):  −6.9% per K
  T = 213 K (−60 °C):  −9.0% per K

At 213 K, a 5 K warm spot lowers K by a factor of exp(0.35/k_B × (1/208 − 1/213)) = 1/1.58
```

At low coverage, the etchant supply at depth falls in proportion. **A cryogenic process needs the wafer temperature controlled to about ±1 K** where a warm process tolerates several kelvin. The heat load of Section 8.1 therefore has to be removed more effectively. Options include higher He pressure, which needs stronger clamping, better chuck surface contact, and recipes that hold the heat flux constant across steps.

### 8.4.3 Cryogenic Hardware

```
Item                          Requirement
──────────────────────────────────────────────────────────────────────────
Chiller                       −70 to −80 °C capacity at several kW of load
ESC materials and bonds       Thermal cycling over 100 K without cracking
                              or debonding; matched expansion
Seals and feedthroughs        Elastomers rated for low temperature, or
                              metal seals
Condensation control          Dry purge around the chuck base; no moisture
                              in the transfer path
Wafer exit                    Warm the wafer above the dew point (in the
                              chamber or the load lock) before it meets
                              ambient air; adds 1–3 min unless overlapped
Temperature metrology         Sensor wafers calibrated at cryogenic
                              temperature; per-zone calibration
```

### 8.4.4 Cryogenic Trade-Offs for the Stack

- **Rate matching.** Nitride forms ammonium fluorosilicate at low temperature (Chapter 4, Section 4.6.3), and ion energy must keep it clear. The ρ window is narrower than in a warm process.
- **Sidewall protection.** With less fluorocarbon polymer, the wall is protected partly by condensed or adsorbed species. Their coverage depends on temperature, so bow becomes temperature-sensitive.
- **Throughput.** The faster etch is partly offset by wafer cool-down and warm-up time. The net gain must be computed per wafer, not per minute of etch (Chapter 16).

---

## 8.5 Chucking a Bowed Wafer

### 8.5.1 The Problem

A wafer with a two-deck stack can bow by 150–350 µm before backside compensation (Chapter 2). Even after compensation, residual bow of 50–150 µm is common, and slits leave a saddle shape. The chuck must pull the wafer flat to establish the He seal and the thermal contact.

### 8.5.2 Force Needed to Flatten

Treat the wafer as a circular elastic plate. The uniform pressure needed to deflect it by the bow height δ is approximately:

```
q ≈ δ · 64 D (1 + ν) / [a⁴ (5 + ν)]

D = E t³ / [12 (1 − ν²)]    (flexural rigidity)

Si: E = 130 GPa, ν = 0.28, t = 775 µm → D = 5.47 N·m
a = 150 mm

δ = 336 µm (two reference decks, uncompensated): q ≈ 56 Pa
```

Flattening the wafer elastically needs only about 56 Pa. That is small compared with the kilopascals that hold the He seal.

### 8.5.3 Force Available Across a Gap

The difficulty is that electrostatic force falls rapidly with the gap between wafer and chuck. For a Coulomb chuck with dielectric thickness d and permittivity ε_r, at a gap g:

```
P(g) ≈ ε₀ V² / [2 (g + d/ε_r)²]

V = 2000 V, d = 300 µm, ε_r = 10 (d/ε_r = 30 µm):

  Gap g          P (Pa)
──────────────────────────
   5 µm         14,500     (wafer seated)
 168 µm            450
 336 µm            132
 600 µm             45
```

*(Illustrative single-electrode estimate; real chucks are bipolar or Johnsen–Rahbek types with different constants.)*

At a 336 µm gap at the edge, the available pressure (132 Pa) still exceeds the 56 Pa needed, and the wafer pulls down from the centre outward. At 600 µm the available pressure (45 Pa) is below the roughly 100 Pa needed, and the edge never seats. **This chuck fails to clamp at around 450–500 µm of bow.** Real chucks extend the range by staged voltage, mechanical assistance, or Johnsen–Rahbek materials. The practical limit still caps the bow the stack may introduce.

### 8.5.4 Effects of Imperfect Chucking

```
Symptom                           Cause                             Effect on etch
───────────────────────────────────────────────────────────────────────────────────
High He leak at edge zone         Edge not seated                   Edge hotter:
                                                                    less polymer,
                                                                    bow ↑, ρ shift
Wafer-to-wafer edge variation     Bow varies by wafer               Edge tilt and CD
                                                                    vary
Asymmetric temperature            Saddle-shaped wafer seats along   Angular (azimuthal)
                                  one axis first                    CD and tilt pattern
Arcing at the edge                Gap + He + high bias              Bevel damage,
                                                                    particles (Ch. 5)
```

He leak rate per zone is the most useful chucking monitor. It should be logged per wafer and correlated with incoming bow (Chapter 15).

---

## 8.6 Summary & Key Takeaways

1. **The wafer absorbs about 6 W/cm².** Most of it comes from 5 keV ions. The heat load changes with every bias step.

2. **The He gap sets the temperature.** About 25 K of the 30 K rise from coolant to wafer is across the backside gas; the stack and silicon add under 1 K.

3. **The wafer responds in half a second.** It follows step changes almost immediately and averages out kHz pulsing.

4. **Colder means more polymer and lower ρ.** Illustrative sensitivities: ρ +0.0014/K, bow +0.3 nm/K.

5. **Cryogenic etch needs ±1 K.** At −60 °C a 0.35 eV adsorbate changes by 9% per kelvin.

6. **Bow limits chucking.** Flattening needs only ~56 Pa, but the electrostatic force collapses with gap. The illustrative chuck fails near 450–500 µm of bow.

---

## Study Questions

1. Bias power rises from 12 to 18 kW with the same ion fraction. With h = 2500 W/m²·K and a 20 °C chuck, estimate the new wafer temperature. What He conductance would hold the wafer at 45 °C?

2. Using the illustrative sensitivities, compute the change in ρ and bow between centre and edge if the edge zone runs 6 K hotter.

3. For E_ads = 0.30 eV, compute d ln K/dT at 223 K and 293 K. What temperature tolerance at 223 K gives the same relative K variation as ±3 K at 293 K?

4. Compute the flattening pressure for a wafer with 250 µm bow, and the electrostatic pressure at a 250 µm gap for the chuck in Section 8.5.3. Does it clamp?

5. A cryogenic recipe etches the reference hole in 18 min but needs 2.5 min of extra cool-down and warm-up per wafer. The conventional recipe takes 40.6 min with 4 min of overhead. Compute wafers per hour per chamber for each.

---

**Previous Chapter:** [Chapter 7: Recipe Architecture](./07-recipe-architecture.md)  
**Next Chapter:** [Chapter 9: Chamber Conditioning & Long-Recipe Stability](./09-chamber-conditioning-stability.md)

---

**Chapter 8 Development Status:** Complete  
**Version:** 1.0
