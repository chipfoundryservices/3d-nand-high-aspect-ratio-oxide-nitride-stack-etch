# Chapter 3: Etching Alternating Layers — Effective Rate, Rate Alternation & Interface Physics

## Overview

A feature etched into an ON stack has a front that crosses an interface every few seconds. On each side of that interface the surface chemistry, the polymer layer, the etch yield, and the products are different. This chapter builds the physics of etching a periodic stack. It starts with the series model, which gives an effective rate that is a harmonic mean of the two film rates. It then looks inside a single pair, where the polymer layer lags behind each change in material, and at the curved etch front, which usually spans both materials at once. Finally it joins the layer picture to high-aspect-ratio transport: ion acceptance, neutral transmission in holes and slots, and aspect-ratio-dependent etching (ARDE), including the important case in which oxide and nitride slow down at different rates with depth.

**Learning Objectives:**
- Derive the effective rate of a two-layer periodic stack and explain why it is a harmonic mean
- Compute the time spent in each layer and the front's speed oscillation at the top and bottom of a feature
- Model the polymer transient at an interface and show why stack rates differ from blanket-film rates
- Estimate how many layers a curved front spans and what that means for rate averaging
- Compute ion pass fractions and neutral transmission for holes and slots
- Integrate ARDE for etch time and show how the rate ratio drifts with depth

---

## 3.1 The Series Model

### 3.1.1 Time Per Pair

If the front moves through oxide at rate R_ox and through nitride at R_N, and each layer is etched independently, the time to etch one pair is the sum of the two layer times:

```
t_pair = d_ox / R_ox + d_N / R_N

Effective rate:
  R_eff = p / t_pair = 1 / (φ_ox/R_ox + φ_N/R_N)

This is the thickness-weighted HARMONIC mean of the two rates.
```

```
Reference (open area, A → 0):
  t_ox   = 22 / 330 = 0.0667 min = 4.0 s
  t_N    = 28 / 300 = 0.0933 min = 5.6 s
  t_pair = 0.1600 min = 9.6 s
  R_eff  = 50 / 0.16 = 312.5 nm/min

Fraction of time in nitride = 5.6 / 9.6 = 58%   (nitride is 56% of the thickness)
```

### 3.1.2 Why Not the Arithmetic Mean

The arithmetic mean φ_ox·R_ox + φ_N·R_N treats each film as if it were etched for a time proportional to its thickness. In reality the front spends longer in the slower film. The arithmetic mean always overestimates:

```
R_ox = 330 nm/min, φ_ox = 0.44

ρ = R_N/R_ox   R_N    Harmonic R_eff   Arithmetic   Arithmetic error
──────────────────────────────────────────────────────────────────────
 1.00          330      330.0           330.0          0%
 0.91 (ref.)   300      312.5           313.2         +0.2%
 0.80          264      289.5           293.0         +1.2%
 0.70          231      266.1           274.6         +3.2%
 0.50          165      211.5           237.6        +12.3%
```

**The slower film dominates.** A nitride rate that falls by 20% costs the stack about 7% of its rate in the reference ratio (from 312.5 to 289.5 when ρ goes from 0.91 to 0.80). If the oxide falls by 20% instead, R_eff drops to 1/(0.44/264 + 0.56/300) = 1/(0.001667 + 0.001867) = 283.0 nm/min, a 9.4% loss. In the reference stack the two films are nearly matched and each matters roughly in proportion to its share of the time.

### 3.1.3 Sensitivity

```
∂ ln R_eff / ∂ ln R_N = (φ_N/R_N) / (φ_ox/R_ox + φ_N/R_N) = time fraction in nitride
∂ ln R_eff / ∂ ln R_ox = time fraction in oxide

Reference: 1% change in R_N → 0.58% change in R_eff
           1% change in R_ox → 0.42% change in R_eff
```

This is a useful rule: **the sensitivity of the stack rate to each film's rate equals the fraction of time the front spends in that film.**

---

## 3.2 The Front's Speed Oscillation

### 3.2.1 Layer Times at the Top and Bottom

Under ARDE (Section 3.6) both rates fall with depth. If they fall by the same factor, the layer times grow by that factor:

```
Rate factor at the bottom of the reference hole: 1/(1 + 93/90) = 0.492

                 Top (A → 0)     Bottom (A = 93)
───────────────────────────────────────────────────
Oxide layer       4.0 s            8.1 s
Nitride layer     5.6 s           11.4 s
Pair              9.6 s           19.5 s
Pairs per minute  6.3              3.1
```

The front never moves at a constant speed. It alternates between 5.5 and 5.0 nm/s near the top, and between 2.7 and 2.5 nm/s at the bottom. The oscillation is only ±5% because the reference films are well matched. With ρ = 0.7 it would be ±18%.

### 3.2.2 Why the Oscillation Matters

1. **Endpoint and OES.** Each change of material changes the products (CO and CO₂ from oxide; HCN, CN, and N₂ from nitride). The emission oscillates at the pair frequency, which is the basis of layer counting at low aspect ratio (Chapter 15).
2. **Sidewall marks.** Each interface leaves a mark on the wall if the lateral rate or polymer differs between films (Chapter 10).
3. **Interface transients.** If the surface takes time to adjust after each change, part of every layer is etched in a transient state (Section 3.3).

---

## 3.3 Interface Transients

### 3.3.1 The Polymer Layer

In fluorocarbon etching the surface carries a steady-state fluorocarbon film a few nanometres thick. Ions and radicals reach the substrate through it, and its thickness controls the etch yield. A widely used empirical form is

```
R = R_bare · exp(−T_p / λ_p)

T_p = steady-state polymer thickness
λ_p = attenuation length for the energy and reactants passing through it (~1–2 nm)
```

The polymer is thinner on oxide than on nitride. Oxygen released from the oxide consumes carbon as CO and CO₂, while nitride releases nitrogen, which removes carbon less efficiently (Chapter 4). So the steady-state polymer is a few tenths of a nanometre to about a nanometre thicker on nitride.

### 3.3.2 Lag at the Interface

When the front passes from oxide into nitride, the polymer starts at the thin oxide value and grows to the nitride value with a time constant τ_p. During that time nitride is etched under a thinner film than its steady state, so it etches **faster** than its steady-state rate. Passing from nitride into oxide, the oxide starts under a thicker film and etches **slower** than its steady state.

Model the rate in a layer as relaxing exponentially to its steady state:

```
R(t) = R_ss · [1 + (k − 1) e^(−t/τ_p)]

k = initial rate / steady-state rate (k > 1 entering nitride; k < 1 entering oxide)

Depth gained, for t ≫ τ_p:  z(t) = R_ss · t + (k − 1) · τ_p · R_ss
                                             └── extra depth from the transient ──┘
```

### 3.3.3 Worked Example: Stack Rate vs. Blanket Rates

Illustrative values near the top of the feature: τ_p = 1.5 s, k_N = 1.15 entering nitride, k_ox = 0.90 entering oxide.

```
Nitride layer:  R_ss = 300 nm/min = 5.00 nm/s
  Extra depth = 0.15 × 1.5 × 5.00 = 1.13 nm
  Time = (28 − 1.13) / 5.00 = 5.38 s   (steady-state value: 5.60 s)
  Apparent rate = 28 / 5.38 = 5.21 nm/s = 312.6 nm/min

Oxide layer:    R_ss = 330 nm/min = 5.50 nm/s
  Extra depth = −0.10 × 1.5 × 5.50 = −0.83 nm
  Time = (22 + 0.83) / 5.50 = 4.15 s   (steady-state value: 4.00 s)
  Apparent rate = 22 / 4.15 = 5.30 nm/s = 318.1 nm/min

Pair time = 9.53 s   →   R_eff = 50 / 9.53 = 5.25 nm/s = 315.0 nm/min
Apparent ratio ρ_stack = 312.6 / 318.1 = 0.98   (blanket ρ = 0.91)
```

Two conclusions follow:

1. **The stack behaves as if its films were better matched than their blanket rates suggest.** The transient pulls the two apparent rates toward each other. R_eff changes very little (+0.8%), but the mismatch that drives striation and bottom roughness is much smaller.
2. **Thinner layers converge more.** The extra depth (k − 1)τ_p R_ss is fixed per interface, so its share of each layer grows as the layers get thinner. At a 40 nm pair pitch the transient is about 25% larger relative to each layer than at 50 nm (Chapter 14).

*These values are illustrative. τ_p and k depend on chemistry, ion flux, and temperature, and are best extracted by fitting stack rates and blanket rates measured in the same chamber (Appendix C).*

**Practical rule:** measure etch rates on stacks, not only on blanket films. A blanket-film ratio is an upper bound on the mismatch the stack feels.

### 3.3.4 Graded Interfaces

PECVD interfaces are graded over 1–2 nm (Chapter 2). A graded interface spreads the change in surface chemistry over a few tenths of a second, which reduces any overshoot. It also changes the lateral etch at the wall: the graded zone has an intermediate composition and its own lateral rate. Chapter 10 returns to this.

---

## 3.4 The Curved Etch Front

### 3.4.1 How Many Layers the Front Spans

The bottom of a hole or slit is not flat. It is a rounded bowl whose sag (the depth from the rim to the centre of the bottom) is typically a third to a half of the bottom width:

```
Reference hole bottom: CD_b = 75 nm, sag h_s ≈ 30 nm (illustrative)
Pair pitch p = 50 nm

Front span / pitch = 30 / 50 = 0.6 pairs
```

At most moments, the centre of the front is in one film while the rim is in the other. With a sag of 0.6 pairs, part of the front is in oxide and part in nitride most of the time. The fraction of the front area in each film varies around φ_ox and φ_N but rarely reaches 0 or 1.

### 3.4.2 Consequences

1. **The front averages.** The polymer, products, and charging at the bottom see a mixture of the two films. Interface transients are partly smoothed out.
2. **The shape breathes.** If the rates differ, the faster film advances faster at the part of the front that is in it. The front's sag oscillates by roughly d·(1 − ρ):

```
Nitride layer, ρ = 0.91:  28 × 0.09 = 2.5 nm oscillation of the sag
Nitride layer, ρ = 0.70:  28 × 0.30 = 8.4 nm
```

A breathing front is harmless in itself, but it is also how a large mismatch writes a rough wall near the bottom, where the wall is formed (Chapter 10).

3. **Across the wafer the phase is random.** Different features reach a given interface at different times because of front-depth variation (Section 3.7). The sum over the wafer of all fronts is a smooth average of the two films after the first few pairs. This is why layer-count endpoint fails at depth (Chapter 15).

---

## 3.5 Transport in Holes and Slits

The layer physics above concerns the surface. Transport decides what reaches it. Book #24 and the slit-etch companion treat transport in feature-specific depth; this section summarizes what applies to every through-stack feature.

### 3.5.1 Ion Acceptance

```
σ_θ ≈ √(T_⊥ / E_i)     (per-axis angular spread)
θ_c ≈ 1/A               (acceptance half-angle)

Round hole (2D cone):   f_pass = 1 − exp(−θ_c² / (2σ_θ²))
Slot (1D):              f_pass = erf(θ_c / (σ_θ √2))
```

```
Reference ions: E_i = 5 keV, T_⊥ = 0.5 eV → σ_θ = 10.0 mrad

Feature            A     θ_c (mrad)   f_pass
───────────────────────────────────────────────
Hole (ref.)        93    10.8         0.44
Slit (ref.)        56    17.9         0.93 (slot)
Hole at A = 56     56    17.9         0.80
Slot at A = 93     93    10.8         0.72
```

A slot accepts more ions than a hole of the same aspect ratio, because only one axis is constrained.

### 3.5.2 Neutral Transmission

For a neutral with cosine entry and diffuse wall reflection that never sticks, the probability of reaching the bottom (Clausing factor) is:

```
Round hole, long tube:  W_hole ≈ 1 / (1 + 3A/4)
Slot (fit to Monte Carlo, A = 20–93):  W_slot ≈ (ln A + 0.1) / A
```

```
Monte Carlo, diffuse walls, no sticking (this book, App. E.3):

  A      W_hole (MC)   1/(1+3A/4)   W_slot (MC)   W_slot / W_hole
─────────────────────────────────────────────────────────────────
  20     0.059          0.063        0.156          2.6
  42     0.030          0.031        0.091          3.1
  56     0.023          0.023        0.074          3.2
  93     0.014          0.014        0.050          3.6
```

A slot transmits **about three times** more neutral flux than a hole at the same aspect ratio. Together with the wider ion acceptance, that is why slits etch faster than holes at the same depth and have a larger ARDE constant A₀.

### 3.5.3 Neutrals That Stick

For a neutral with wall-loss probability s, density decays with depth with length λ ≈ w̄/√(3s) in a round hole:

```
w̄ = 90 nm:
  s = 10⁻²:   λ = 520 nm
  s = 10⁻³:   λ = 1.64 µm    → n(8.4 µm)/n₀ = exp(−5.1) = 0.6%
  s = 10⁻⁴:   λ = 5.2 µm     → n(8.4 µm)/n₀ = exp(−1.6) = 20%
```

Radicals with sticking coefficients of 10⁻² or more (F, CF, CF₂ on polymer-covered walls) are gone within the first micrometre. At depth, the etch runs on ion-driven chemistry and on species that stick weakly (HF, O₂) or move along the wall as an adsorbed layer (Chapter 4, Chapter 8).

---

## 3.6 ARDE of a Layered Material

### 3.6.1 The Effective-Rate Form

The empirical ARDE relation applies to the effective rate:

```
R_eff(A) = R_eff,0 / (1 + A/A₀)

Reference: R_eff,0 = 312.5 nm/min; A₀ = 90 (hole), 120 (slit)

Depth (µm)   Hole A   Hole R (nm/min)   Slit A   Slit R (nm/min)
──────────────────────────────────────────────────────────────────
 0             0        312.5              0        312.5
 2.0          22        251.1             13        282.0
 4.0          44        209.9             27        255.1
 6.0          67        179.1             40        234.4
 8.4          93        153.7             56        213.1
```

### 3.6.2 Time to Depth

```
dz/dt = R_eff(A),  z = A·w̄   →   t(A) = (w̄/R_eff,0) · (A + A²/(2A₀))

Hole: t(93) = 0.288 × (93 + 48.1) = 40.6 min
Slit: t(56) = 0.480 × (56 + 13.1) = 33.2 min
```

### 3.6.3 When the Two Films Slow Differently

ARDE need not act equally on oxide and nitride. Nitride needs more fluorine per nanometre (Chapter 2) and depends more on hydrogen chemistry, so when the neutral supply falls with depth, nitride often slows **more**. Give each film its own ARDE constant:

```
R_ox(A) = 330 / (1 + A/100)     R_N(A) = 300 / (1 + A/82)     (illustrative)

ρ(A) = 0.909 × (1 + A/100) / (1 + A/82)

  A       R_ox     R_N     ρ       R_eff (harmonic)
────────────────────────────────────────────────────
  0      330.0    300.0   0.91     312.5
 30      253.8    219.6   0.87     233.5
 60      206.2    173.2   0.84     186.4
 93      171.0    140.6   0.82     152.5
```

The effective rate at the bottom (152.5 nm/min) is close to the single-A₀ value (153.7), so the time model still holds. But **the rate ratio drifts from 0.91 to 0.82** between the top and bottom. A stack that is well matched at the top is mismatched at the bottom. Recipes respond by ramping chemistry with depth, typically adding hydrogen or reducing oxygen in the late steps to support the nitride rate (Chapter 7).

---

## 3.7 Front Variation Across Features

Every feature on the wafer is at a slightly different depth at a given time. The spread has three sources:

```
Source                                   Typical size (1σ, illustrative)
──────────────────────────────────────────────────────────────────────────
Rate non-uniformity across the wafer     1.0–1.5% of depth
Stack thickness variation (Ch. 2)        Enters at landing, not during etch
CD variation → A variation → rate        1 nm CD (1.1%) → ~0.6% depth
Local loading (array edge vs. centre)    0.5–1.0% of depth
```

Combining to σ_z ≈ 1.5% of depth: at 750 nm depth, σ_z ≈ 11 nm, which is a fifth of a pair. By 3 µm σ_z ≈ 45 nm, nearly a full pair. **After the first micrometre or so, features across the wafer are at random points in the pair cycle.** This sets the limit for layer-resolved endpoint (Chapter 15, Section 15.2).

---

## 3.8 Products of the Stack Etch

```
Film       Main volatile products                     Signature species (OES)
───────────────────────────────────────────────────────────────────────────────
SiO₂       SiF₄, CO, CO₂, COF₂                        CO (Ångström bands, 451, 483,
                                                      520 nm), O (777 nm)
Si₃N₄      SiF₄, HCN, N₂, FCN, NF_x (minor)           CN (388 nm), N₂ (337 nm)
Both       SiF_x, CF_x fragments, HF                  SiF (440 nm), CF₂ (250–320 nm)
```

Per pair at the reference rate, a single hole releases about 1.3×10⁶ silicon atoms per second near the top (Appendix E.4). The products must diffuse out through the same feature, which raises the product density at the bottom of a deep hole to a noticeable fraction of the chamber gas density (Book #24, Chapter 3). In a stack the product composition alternates with the front, adding a small pair-frequency modulation to redeposition along the wall.

---

## 3.9 Summary & Key Takeaways

1. **Stack rate is a harmonic mean.** R_eff = 1/(φ_ox/R_ox + φ_N/R_N) = 312.5 nm/min in the reference. The slower film dominates, and each film's sensitivity equals its share of the etch time.

2. **The front oscillates in speed.** ±5% for the reference films, larger for mismatched pairs. Each change of film changes the products and can mark the wall.

3. **Interface transients reduce the apparent mismatch.** The polymer lags each change of material, so stack rates are closer than blanket rates. Measure on stacks.

4. **The curved front spans both films.** A 30 nm sag over a 50 nm pitch keeps both materials exposed much of the time. The front averages, and its shape breathes by about d·(1 − ρ).

5. **Slots beat holes in transport.** A slot passes about three times the neutral flux of a hole at the same aspect ratio and accepts more ions.

6. **ARDE can unbalance the films.** If nitride slows more with depth, ρ drifts from 0.91 at the top to 0.82 at the bottom, and the recipe must compensate.

7. **Features fall out of phase.** With 1.5% front spread, features across the wafer are at random points of the pair cycle after about a micrometre.

---

## Study Questions

1. A stack has d_ox = 25 nm and d_N = 25 nm, R_ox = 300 nm/min and R_N = 240 nm/min. Compute R_eff, the arithmetic mean, and the fraction of time in nitride. What 1% change in which film rate would change R_eff the most?

2. Using the transient model with τ_p = 2.0 s, k_N = 1.2, and k_ox = 0.85, compute the apparent nitride and oxide rates and R_eff for the reference stack near the top. Compare ρ_stack with the blanket ρ.

3. A slit has w̄ = 140 nm and depth 9.0 µm. Compute A, the ion pass fraction at 5 keV (T_⊥ = 0.5 eV), and W_slot from the fit. Compare with a round hole of the same A.

4. With A₀,ox = 110 and A₀,N = 75, compute ρ and R_eff at A = 0, 50, and 93 for the reference rates. At what aspect ratio does ρ fall below 0.80?

5. The front spread is σ_z = 1.2% of depth. At what depth does σ_z equal one quarter of the pair pitch? Explain what happens to the pair-frequency OES signal beyond that depth.

---

**Previous Chapter:** [Chapter 2: Stack Films — PECVD Oxide & Nitride, Thickness Ratio & Stress](./02-stack-film-properties.md)  
**Next Chapter:** [Chapter 4: ON Etch Chemistry — Fluorocarbons, Hydrogen & Rate Matching](./04-on-etch-chemistry.md)

---

**Chapter 3 Development Status:** Complete  
**Version:** 1.0
