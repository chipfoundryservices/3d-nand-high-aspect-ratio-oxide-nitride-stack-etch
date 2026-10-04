# Chapter 13: Mask Selectivity, Landing & Loading Between Features

## Overview

The ON-stack etch is a race against two clocks. The mask clock runs at a steady rate from the first second: the carbon mask erodes whether the front is fast or slow. The landing clock starts when the first feature reaches the bottom: from then on, every second of overetch digs that feature into its landing layer while the slowest features catch up. This chapter builds the mask budget and the landing budget for the reference process. It then shows how co-etching features of different widths and depths stresses both, and how the uniformity of the etch and of the stack combine across the wafer.

**Learning Objectives:**
- Build a mask budget from erosion rates, stage times, edge excess, and the minimum remaining mask
- Explain the feedback between mask thickness and effective aspect ratio
- Compute the overetch needed to land a population of 10¹² features, including systematic and random terms
- Compute landing-layer recess from overetch and selectivity, and the selectivity a given recess limit requires
- Estimate the landing problem when features of different widths are etched together
- Combine deposition and etch radial profiles into a front-uniformity budget

---

## 13.1 The Mask Budget

### 13.1.1 Required Thickness

```
T_mask ≥ (Σ r_m,i · t_i) · (1 + e_edge) + T_facet + T_min

r_m,i   = mask erosion rate in stage i
t_i     = stage time
e_edge  = extra erosion at the wafer edge (5–15%)
T_facet = allowance so the facet does not reach the stack top (≈ 0–100 nm)
T_min   = minimum remaining mask for profile protection at the end (≈ 300 nm)
```

```
Reference (Chapter 7, simplified to 45 nm/min over 45.1 min):
  Consumed at centre:        45 × 45.1 = 2030 nm
  With 10% edge excess:      2233 nm
  Plus T_min = 300 nm:       2533 nm
  Available:                 2400 nm a-C       → short by ~130 nm at the edge
```

The detailed stage budget (Chapter 7, Section 7.2.3) is slightly more favourable, but the conclusion is the same. **The reference process has no mask margin at the wafer edge.** The fixes are a thicker or harder mask, less erosion in the deep steps, or less overetch.

### 13.1.2 Mask Thickness Feeds Back on Aspect Ratio

The mask is part of the feature. At the start, the opening in a 2.4 µm mask over a 105 nm hole is itself 23:1. The neutral flux that reaches the stack must first pass through it. As the etch proceeds, the mask thins, and the total height (remaining mask + etched depth) grows more slowly than the depth:

```
Point in etch       Mask left    Depth     Total height   A_total (w̄ = 90 nm)
──────────────────────────────────────────────────────────────────────────────
Start               2.40 µm      0         2.40 µm         27
Mid (t ≈ 20 min)    1.50 µm      4.8 µm    6.3 µm          70
End (t ≈ 41 min)    0.55 µm      8.4 µm    8.95 µm         99
```

A thicker mask raises the effective aspect ratio throughout, which slows the etch, which costs more mask. Adding 500 nm of mask costs about 5% of rate in the middle of the etch (illustrative). **Mask thickness cannot be increased freely; mask selectivity must improve instead.**

### 13.1.3 Improving the Mask

```
Option                              Gain                         Cost
───────────────────────────────────────────────────────────────────────────────
Denser a-C (higher sp³ fraction)    Erosion −10–25%              Stress; harder mask
                                                                 open; opacity
Boron- or metal-doped carbon        Erosion −30–50%              Mask open and strip
                                                                 chemistry; residues;
                                                                 contamination control
Thicker a-C                         Linear in thickness          Higher A_total; mask
                                                                 open AR; stress
Polymer-protective chemistry        Erosion −5–20%               Taper, clogging, ρ
High-peak pulsed bias (Ch. 6)       Erosion per µm at depth ↓    Hardware; top rate ↓
Less overetch (better uniformity)   Directly reduces OE term     Requires feed-forward
                                                                 and uniform rate
```

Book #19 (Carbon Hard Mask Etch) covers mask materials and mask open.

---

## 13.2 Landing

### 13.2.1 Why Overetch Is Needed

Features arrive at the landing layer at different times. The etch must continue until the last feature has arrived. The arrival-time spread has systematic and random parts:

```
Source                                     Type          Size (reference)
─────────────────────────────────────────────────────────────────────────────
Stack thickness radial profile (Ch. 2)     Systematic    ±1.5% of H
Etch rate radial profile                   Systematic    ±1.5% of t
Local loading (array edge, density)        Systematic    ±0.5%
Feature-to-feature rate (CD, local         Random        σ = 1.0% of t
 polymer, charging)
```

### 13.2.2 Overetch for 10¹² Features

The random part must be covered out to the tail of 10¹² features per wafer. For a normal distribution, a miss probability of 10⁻¹² per feature needs about 7σ:

```
Systematic (worst-case region, after partial cancellation): ~3% of 40.6 min = 1.2 min
Random tail: 7 × 1.0% × 40.6 min                                           = 2.8 min
───────────────────────────────────────────────────────────────────────────────────
Overetch                                                                    ≈ 4.0 min (10%)
```

This matches the reference OE of Chapter 7. The tail term is the larger one, and it can only be reduced by reducing the random variation itself, not by measurement (Chapter 15).

*(The Gaussian assumption is optimistic for clogging-type failures, which produce non-Gaussian tails; Chapter 11, Section 11.5.)*

### 13.2.3 Recess Into the Landing Layer

The earliest features spend the whole overetch in the landing layer. At the bottom rate R_b and stack-to-landing selectivity S:

```
Recess_max = t_OE · R_b / S

Reference: t_OE = 4.0 min, R_b = 153.7 nm/min
  S = 15 → 41 nm
  S = 20 → 31 nm
  S = 25 → 25 nm

Specification (Chapter 1): recess ≤ 30 nm → S ≥ 20.5
```

The landing chemistry must provide a selectivity of about 20 or more **at the bottom of a 93:1 hole**, where the selective polymer-rich chemistry also risks clogging (Chapter 11). The landing step is therefore a balance of selectivity against bottom-CD closure.

### 13.2.4 Landing-Layer Thickness

```
Required landing-layer thickness ≥ Recess_max + margin for downstream steps

Doped poly-Si landing: 31 nm recess at S = 20 + 30 nm margin → ≥ 61 nm
```

A thinner landing layer reduces stack height and cost but requires better uniformity or higher selectivity.

---

## 13.3 Loading Between Features

### 13.3.1 Co-Etched Features of Different Widths

Some flows etch features of different widths in the same step: for example, support holes in the staircase together with memory holes, or holes of two sizes at the edge of the array. ARDE makes the wider feature faster:

```
Same stack, same recipe (A₀ = 90):

Memory hole: w̄ = 90 nm,  A = 93  → t = 40.6 min
Support hole: w̄ = 200 nm, A = 42 → t = (200/312.5)(42 + 42²/180) = 33.2 min

The support hole lands 7.4 min before the memory hole.
Its bottom rate at landing: 312.5 / (1 + 42/90) = 213 nm/min

Recess in the support hole during the extra 7.4 min (S = 20):
  7.4 × 213 / 20 = 79 nm (plus its share of the regular overetch)
```

**Co-etching features of different widths multiplies the landing problem.** Remedies include a thicker or more selective stop under the wide feature, separate etches, or layout rules that keep co-etched features within a narrow width range.

### 13.3.2 Features Through Different Stacks

Support holes in the staircase pass through staircase fill oxide (which etches faster than ON) above a partial stack. The amount of ON stack under each tread is different. Their arrival times vary systematically across the staircase. The landing chemistry and stop layer must absorb the whole range, or the staircase support holes must be etched separately.

### 13.3.3 Macroloading

The total open area on the wafer changes the consumption of etchant:

```
Feature layer          Open area (illustrative)   Effect
──────────────────────────────────────────────────────────────────────
Memory holes            ~25% of the wafer         High etchant consumption;
                                                  high product load
Slits                   ~5–10%                    Lower consumption
TACs                    ~1%                       Little loading; rate close
                                                  to blanket
```

A recipe developed on one layer cannot be moved to another with a different open area without retuning rate and ρ.

### 13.3.4 Array-Edge Loading

Holes at the edge of an array have open field on one side. They see more etchant, less product, and a different charging environment. They often etch slightly faster and twist toward or away from the field (Chapter 12). Layouts place several rows of dummy holes at array edges to absorb this, so that the first active hole sees the same neighbourhood as the centre of the array.

---

## 13.4 Within-Wafer Uniformity

### 13.4.1 Two Profiles

The time to land at each point on the wafer depends on two radial profiles:

```
t_land(r) ∝ H(r) / R(r)

H(r) = stack height profile (deposition)
R(r) = etch rate profile (etch)

If the stack is +1.5% thick at the centre and the etch is +1.5% fast at the centre:
  t_land(centre) / t_land(mean) ≈ 1.015 / 1.015 = 1.00 → profiles cancel

If the stack is +1.5% thick at the centre and the etch is −1.5% slow there:
  t_land(centre) / t_land(mean) ≈ 1.015 / 0.985 = 1.03 → profiles add (3%)
```

### 13.4.2 Co-Optimization

Etch rate profiles can be tuned with radial gas injection, ESC temperature zones, and source power distribution (Chapters 5 and 8). Deposition profiles are tuned with showerhead design, spacing, and temperature. Because the two modules optimize separately, they often leave profiles that add. A fab that **matches the etch profile to the measured stack profile** removes most of the systematic overetch term:

```
Systematic term in the overetch (Section 13.2.2):
  Profiles adding:     3% → 1.2 min
  Profiles matched:    ~0.5% → 0.2 min
  Saving:              1.0 min of overetch → ~45 nm of mask, ~8 nm less recess
```

The radial ESC zones are often the fastest actuator for this (Chapter 15).

---

## 13.5 Summary & Key Takeaways

1. **The mask clock runs constantly.** At 45 nm/min over 45 min, the reference uses about 2.0 µm of mask, and with edge excess and a 300 nm minimum it is short at the edge.

2. **More mask is not free.** A thicker mask raises the effective aspect ratio and slows the etch. Selectivity must improve instead.

3. **Overetch covers a 7σ tail.** About 2.8 min of the 4.0 min reference overetch covers the random tail of 10¹² features; systematic terms add 1.2 min.

4. **Landing needs selectivity ~20 at the bottom.** A 30 nm recess limit with 4 min of overetch at 154 nm/min requires S ≥ 20.5.

5. **Co-etched widths multiply recess.** A 200 nm support hole lands 7.4 min early and recesses 79 nm more at S = 20.

6. **Profiles should cancel.** Matching the etch rate profile to the stack thickness profile removes most of the systematic overetch.

---

## Study Questions

1. A boron-doped mask lowers erosion by 35%. Recompute the edge mask budget for the reference recipe. How much thinner could the mask be for the same remaining thickness?

2. The random arrival spread is reduced from 1.0% to 0.7% (σ). Compute the new overetch and the new maximum recess at S = 20.

3. A landing layer must hold recess ≤ 20 nm. With the reference overetch and bottom rate, what selectivity is needed? If only S = 15 is achievable, how much must overetch be reduced?

4. Support holes of w̄ = 150 nm are co-etched with memory holes. Compute their arrival time and the extra recess at S = 20.

5. The stack is 1% thicker at the edge and the etch is 2% slower there. Compute the edge landing time relative to the centre, and the change in the systematic overetch term.

---

**Previous Chapter:** [Chapter 12: Charging, Twisting & Stress-Driven Distortion](./12-charging-twisting-distortion.md)  
**Next Chapter:** [Chapter 14: Scaling to 300–1000 Layers — Decks, Thinner Pairs & Next-Generation Etch](./14-scaling-multideck-nextgen.md)

---

**Chapter 13 Development Status:** Complete  
**Version:** 1.0
