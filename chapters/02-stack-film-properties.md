# Chapter 2: Stack Films — PECVD Oxide & Nitride, Thickness Ratio & Stress

## Overview

The etch engineer does not choose the material being etched, but a great deal of the etch is decided by it. The density, hydrogen content, and stoichiometry of the stack films set their etch rates. The thickness ratio of oxide to nitride sets the effective rate and the endpoint time. The radial thickness profile of the deposition sets the depth uniformity before the etch has any say. The stress of the films bends the wafer by hundreds of micrometres. This chapter describes how the ON stack is deposited, which film properties matter to the etch and by how much, and how to monitor a stack so that a deposition change does not arrive at the etch chamber unannounced.

**Learning Objectives:**
- Describe PECVD deposition of stack oxide and nitride and the film properties that result
- Compute atom and silicon densities and explain why nitride needs more ion work per nanometre
- Estimate the effect of hydrogen content and density on oxide and nitride etch rates
- Separate random and systematic contributions to stack-height variation
- Compute wafer bow from layer stresses using Stoney's equation, and design a stress-balanced stack
- Identify the non-periodic layers (cap, inter-deck, source stack) and their effect on the etch

---

## 2.1 Depositing the Stack

### 2.1.1 Alternating PECVD

The stack is deposited by plasma-enhanced chemical vapour deposition (PECVD), typically in a multi-station chamber that switches gases between oxide and nitride without breaking vacuum:

```
Film     Precursors                 Temperature   Rate (illustrative)   Notes
───────────────────────────────────────────────────────────────────────────────────────
SiO₂     TEOS + O₂ (or SiH₄ + N₂O)  400–550 °C    150–300 nm/min        TEOS gives better
                                                                         conformality, some C
Si₃N₄    SiH₄ + NH₃ + N₂            400–550 °C    100–200 nm/min        H bonded as Si–H
                                                                         and N–H
```

```
Reference deck deposition time (illustrative):
  160 × 22 nm oxide at 200 nm/min  = 17.6 min
  160 × 28 nm nitride at 150 nm/min= 29.9 min
  Gas switch + stabilize 8 s × 320 = 42.7 min
  Cap and overhead                 ≈ 10 min
  Total ≈ 100 min per deck in one station (multi-station tools split the work)
```

The gas switch time is a large fraction of the total. Short switches reduce cost but leave a graded transition at each interface. A graded interface 1–2 nm thick is normal and matters for striation (Chapter 10).

### 2.1.2 Why PECVD Films Are Not Bulk Materials

PECVD films are deposited far below their equilibrium formation temperature. They contain hydrogen, are less dense than thermal or LPCVD films, and their composition depends on gas ratios, RF power, and temperature. Two nitride recipes that both read "Si₃N₄" on a process flow can differ by 10 at% in hydrogen and by 15% in etch rate.

---

## 2.2 Film Properties That Matter to the Etch

### 2.2.1 Property Table

```
Property                    Stack SiO₂ (PECVD)     Stack Si₃N₄ (PECVD)    Thermal/LPCVD
                                                                          reference
─────────────────────────────────────────────────────────────────────────────────────────
Density (g/cm³)             2.15–2.25              2.5–2.85               2.27 / 3.1
Refractive index (633 nm)   1.45–1.47              1.90–2.05              1.46 / 2.01
Hydrogen (at%)              1–5 (Si–OH, H₂O)       12–25 (Si–H, N–H)      ~0 / 2–5
Si/N ratio                  —                      0.75–0.90              0.75
Dielectric constant         4.0–4.2                6.5–7.5                3.9 / 7.5
Stress (MPa)                −100 to −300 (comp.)   −300 to +400 (tunable) —
Wet etch rate, 100:1 HF     3–6× thermal oxide     1–3× LPCVD nitride     1 / 1
```

*(Ranges are representative. Reference stack values are in Appendix A.)*

### 2.2.2 Atom and Silicon Density

The number of atoms that must be removed per nanometre of depth differs between the two films:

```
SiO₂, ρ = 2.20 g/cm³, M = 60.08 g/mol, 3 atoms per unit
  Units/cm³ = 2.20 / 60.08 × 6.022×10²³ = 2.21×10²² → 6.6×10²² atoms/cm³
  Si/cm³    = 2.21×10²²

Si₃N₄, ρ = 2.80 g/cm³, M = 140.28 g/mol, 7 atoms per unit
  Units/cm³ = 2.80 / 140.28 × 6.022×10²³ = 1.20×10²² → 8.4×10²² atoms/cm³
  Si/cm³    = 3.60×10²²
```

Per nanometre of depth, nitride has **27% more atoms and 63% more silicon** than oxide. Every silicon atom must leave as SiF₄ (or SiF_x), so nitride needs more fluorine and more ion work per nanometre. Its rate is lower unless something else, usually hydrogen and the lack of oxygen in the film, makes up the difference (Chapter 4).

### 2.2.3 Hydrogen

Hydrogen enters nitride as Si–H and N–H bonds. It affects the etch in three ways:

1. **Lower density.** H-rich nitride is less dense, so fewer Si atoms per nanometre.
2. **Weaker network.** Si–H and N–H terminate the network and lower the energy needed to break it up.
3. **Chemistry.** Hydrogen released at the surface scavenges fluorine as HF and helps carry nitrogen away as HCN. Chapter 4 shows that the net effect raises the nitride rate in typical fluorocarbon chemistries.

```
Illustrative sensitivity of the nitride etch rate (HAR fluorocarbon chemistry):
  ∂R_N / ∂[H]   ≈ +1.5% per at% H
  ∂R_N / ∂ρ     ≈ −1.2% per 0.01 g/cm³

Example: nitride hydrogen lowered from 20 to 14 at% to improve cell retention,
density rises from 2.70 to 2.78 g/cm³
  ΔR_N/R_N ≈ (−6 × 1.5%) + (−8 × 1.2%) = −9% − 9.6% ≈ −19%
```

A change of that size moves the rate ratio from 0.91 to about 0.74, enough to change striation, bottom shape, and endpoint (Chapters 3 and 10). The sensitivities are illustrative and must be measured for each chemistry. The direction is consistent across the literature: **denser, lower-hydrogen nitride etches more slowly**.

### 2.2.4 Oxide Variants

Stack oxide is less variable than nitride but not uniform:

```
Oxide variation               Effect on etch (illustrative)
───────────────────────────────────────────────────────────────────────
TEOS vs. silane oxide          TEOS: some residual C and OH; rate +3–8%
Lower deposition temperature   More OH, lower density; rate +5–10%
Higher RF power (denser film)  Rate −3–5%
Boron or phosphorus doping     Rate +10–30% (used in some cap layers)
```

---

## 2.3 Thickness Ratio and Pair Pitch

### 2.3.1 Definitions

```
p     = d_ox + d_N            (pair pitch)
φ_ox  = d_ox / p               (oxide thickness fraction)
φ_N   = d_N / p = 1 − φ_ox

Reference: d_ox = 22 nm, d_N = 28 nm, p = 50 nm, φ_ox = 0.44, φ_N = 0.56
```

### 2.3.2 Effect on Effective Rate

As Chapter 3 derives, the effective vertical rate through a pair is

```
R_eff = p / (d_ox/R_ox + d_N/R_N) = 1 / (φ_ox/R_ox + φ_N/R_N)

Reference: 1 / (0.44/330 + 0.56/300) = 1 / (0.001333 + 0.001867) = 312.5 nm/min
```

The device team may change the thickness ratio, for example thinning the oxide to 20 nm and thickening the nitride to 30 nm to lower word-line resistance. The pair pitch is unchanged, but:

```
φ_ox = 0.40, φ_N = 0.60:
  R_eff = 1 / (0.40/330 + 0.60/300) = 1 / (0.001212 + 0.002000) = 311.3 nm/min
```

The change is only 0.4%, because the reference rates are close. With a poorly matched pair (R_N = 200 nm/min), the same change would take R_eff from 241.9 to 237.4 nm/min, −1.9%, nearly five times larger. **The thickness ratio matters in proportion to the rate mismatch.**

### 2.3.3 Layer Thickness Control

Each layer is controlled by deposition time. Rate drift in the deposition chamber changes every layer in the deck by the same fraction, so it is systematic. Random layer-to-layer variation also exists but averages out over many layers:

```
Random: σ_d = 0.5 nm per layer (≈ 2%), N = 320 layers per deck
  σ_H,random = 0.5 × √320 = 8.9 nm  (0.1% of 8.4 µm, negligible)

Systematic: deposition rate +1.0% at the wafer centre vs. the mean
  ΔH = 1.0% × 8.4 µm = 84 nm
```

**Systematic radial profiles dominate stack-height variation.** A typical PECVD stack is ±1–2% from centre to edge. That variation passes directly into the time each region needs to reach the landing layer and is the first term in the landing budget (Chapter 13).

---

## 2.4 Stack Stress and Wafer Bow

### 2.4.1 Net Stack Stress

The stress of the stack is the thickness-weighted average of the layer stresses:

```
σ_stack = φ_ox·σ_ox + φ_N·σ_N

Reference: σ_ox = −200 MPa (compressive), σ_N = +100 MPa (tensile)
  σ_stack = 0.44 × (−200) + 0.56 × (+100) = −88 + 56 = −32 MPa
```

### 2.4.2 Stoney's Equation

For a film of thickness t_f and stress σ_f on a substrate of thickness t_s and biaxial modulus M_s:

```
κ = 6 σ_f t_f / (M_s t_s²)            (curvature, 1/m)
δ = κ r² / 2                          (centre-to-edge bow at radius r)

Si (100) wafer: M_s = 180 GPa, t_s = 775 µm, r = 150 mm

One reference deck (t_f = 8.4 µm, σ = −32 MPa):
  κ = 6 × 32×10⁶ × 8.4×10⁻⁶ / (180×10⁹ × (775×10⁻⁶)²)
    = 1613 / 1.081×10⁵ = 0.0149 m⁻¹
  δ = 0.0149 × 0.0225 / 2 = 168 µm

Two decks (t_f ≈ 16.8 µm of ON):
  δ ≈ 336 µm
```

A bow of 300 µm or more is far outside what lithography, chucking, and wafer handling tolerate (often < 100–150 µm). Fabs therefore:

1. **Tune nitride stress** toward more tensile values to offset the compressive oxide
2. **Deposit a backside compensation film** (often nitride or oxide on the back of the wafer)
3. **Anneal**, which drives hydrogen out of nitride and makes it more tensile

### 2.4.3 Stress-Balanced Stack Design

The condition for zero net stress is φ_ox·σ_ox + φ_N·σ_N = 0:

```
σ_N,balance = −φ_ox·σ_ox / φ_N = 0.44 × 200 / 0.56 = +157 MPa
```

A nitride tuned to about +160 MPa would balance the reference oxide. But tensile nitride is typically deposited with less hydrogen and higher density, which lowers its etch rate (Section 2.2.3). **Stress balance and rate matching pull the nitride in opposite directions.** This is one of the most important stack-etch trade-offs. It is often resolved by balancing stress mostly with the backside film and keeping the nitride closer to the etch-friendly composition.

### 2.4.4 Stress Changes After Etch

The etch removes material and changes the bow:

- **Holes** remove about 25% of the area at the top (Chapter 1) in an isotropic pattern. Biaxial stress in the deck relaxes roughly in proportion to the removed fraction, and the bow changes by tens of micrometres.
- **Slits** cut the stack into long blocks. Stress relaxes across the slit but not along it, so the wafer becomes **saddle-shaped** (anisotropic bow). Blocks may lean (Chapter 12).

The second deck is etched on a wafer that already carries the stress of the first, so the chucking and edge behaviour of deck 2 is not the same as deck 1 (Chapter 8).

---

## 2.5 Non-Periodic Layers

### 2.5.1 The Layers Around the Pairs

```
Position        Layer                       Typical thickness   Etch effect
────────────────────────────────────────────────────────────────────────────────────────
Top             Cap oxide                   100–300 nm          Fast oxide etch; sets
                                                                initial profile
Top             Select-gate pairs           Normal or thicker   Normal
                (sometimes different        pairs
                thickness ratio)
Middle          Inter-deck layer (IDL)      100–400 nm oxide    Rate jump; joint step
                                            or oxide/poly       (Chapter 7)
Bottom          Bottom select / dummy       Normal pairs        Normal
Bottom          Buffer oxide                30–100 nm           —
Landing         Source stack: poly-Si /     50–300 nm           Etch stop; overetch
                oxide / nitride / poly-Si                       (Chapter 13)
                (replacement source) or
                doped poly / W
```

### 2.5.2 Why They Matter

Each non-periodic layer is a step change in material at a known depth. The etch rate, polymer state, and products change at each one:

- The **cap oxide** is etched first, at shallow depth and high rate. It sets the initial wall angle and the top CD (Chapter 11).
- An **inter-deck oxide** etches faster than the stack (no nitride), so the deck-2 front accelerates as it reaches it. If the recipe is not matched there, a ledge forms (Chapter 7).
- The **landing layer** must have high selectivity to the stack chemistry. Its thickness sets how much overetch can be spent (Chapter 13).

---

## 2.6 Monitoring the Stack for the Etch

### 2.6.1 What to Measure

```
Measurement                   Method                          Frequency (illustrative)
──────────────────────────────────────────────────────────────────────────────────────
Total stack thickness, map    Spectral reflectometry with     Every wafer (or every lot)
                              multilayer model; X-ray
                              reflectometry on monitors
Individual layer thickness    Monitor-wafer ellipsometry      Daily per chamber
                              of single films; TEM on product Weekly
Nitride H content             FTIR (Si–H ~2170 cm⁻¹,          Daily monitor
                              N–H ~3350 cm⁻¹)
Refractive index              Ellipsometry                    Daily monitor
Stress / bow                  Wafer curvature (laser          Every wafer before etch
                              scanning or interferometry)
Particles                     Laser scattering                Every lot
```

### 2.6.2 Feed-Forward to the Etch

The two stack measurements that most directly help the etch are **total thickness map** and **bow**:

```
Thickness map → etch time (or landing-step time) per wafer and radial tuning
Bow → chucking recipe, He pressure, edge setting (Chapter 15)
```

A fab that does not pass these to the etch module is relying on the etch overetch margin to absorb deposition variation. Chapter 15 shows how much margin that costs.

---

## 2.7 Summary & Key Takeaways

1. **The stack is PECVD material, not bulk material.** Composition, density, and hydrogen vary with deposition conditions and directly change etch rates.

2. **Nitride needs more work per nanometre.** It has 27% more atoms and 63% more silicon per unit volume than oxide.

3. **Hydrogen raises the nitride rate.** Dense, low-hydrogen nitride for retention or tensile stress can cut the nitride rate by 15–20%.

4. **The thickness ratio matters in proportion to the mismatch.** With matched rates, changing φ_ox barely changes R_eff. With mismatched rates it does.

5. **Systematic deposition profiles dominate height variation.** Random layer variation averages away; radial profiles of ±1–2% do not.

6. **The stack bows the wafer by hundreds of micrometres.** Stress balance and rate matching pull the nitride in opposite directions.

7. **Non-periodic layers are step changes for the etch.** Cap, inter-deck, and landing layers each need their own recipe treatment.

---

## Study Questions

1. Compute the Si atom density of a PECVD nitride with density 2.65 g/cm³ and Si/N = 0.80 (ignore hydrogen mass). Compare with the reference nitride.

2. A deck uses oxide at −180 MPa and nitride at +60 MPa with d_ox = 24 nm and d_N = 26 nm. Compute the net stress and the bow for a 7.6 µm deck. What nitride stress would balance it?

3. Deposition rate in one chamber is 1.5% high at the centre and 1.0% low at the edge. For an 8.4 µm deck, compute the difference in time to the landing layer between the centre and the edge, using the reference bottom rate of 154 nm/min.

4. Using the sensitivities in Section 2.2.3, compute the new nitride rate and R_eff if the nitride hydrogen rises from 18 to 22 at% and the density falls by 0.04 g/cm³. Start from the reference rates.

5. Explain why random layer thickness variation contributes so little to height variation. Under what condition would layer-to-layer variation be correlated, and what would its contribution then be?

---

**Previous Chapter:** [Chapter 1: The ON Stack in 3D NAND](./01-on-stack-architecture.md)  
**Next Chapter:** [Chapter 3: Etching Alternating Layers — Effective Rate, Rate Alternation & Interface Physics](./03-alternating-layer-etch-physics.md)

---

**Chapter 2 Development Status:** Complete  
**Version:** 1.0
