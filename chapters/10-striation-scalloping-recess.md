# Chapter 10: Sidewall Striation, Scalloping & Layer-Selective Recess

## Overview

The sidewall of a feature etched through an ON stack keeps a record of the stack. Look at a high-magnification cross-section of a memory hole and the wall is not smooth: it carries a faint periodic ridge at every oxide/nitride interface. It also carries vertical streaks running down the wall from the mask. After the wet clean that follows etch, the ridges can grow into steps several nanometres deep. This chapter separates the two kinds of wall roughness, builds a model of layer modulation from the lateral-rate difference and the exposure time at each depth, and adds the contributions from the front shape, the interfaces, and post-etch cleaning. It then estimates what modulation costs the device and lists the levers that keep the wall smooth. It closes with designs in which a layer-selective recess is made on purpose.

**Learning Objectives:**
- Distinguish layer modulation (horizontal, at the pair period) from vertical striation (azimuthal, from the mask)
- Compute modulation amplitude versus depth from a lateral-rate difference and the wall exposure time
- Estimate front-shape and interface contributions to modulation
- Calculate the layer-selective recess added by a dilute-HF clean and compare it with the etch contribution
- Relate wall modulation to cell variation and other downstream effects
- Choose etch, deposition, and clean levers to control modulation, and describe intentional recess schemes

---

## 10.1 Two Kinds of Wall Roughness

```
                       Layer modulation                  Vertical striation
                       ("scalloping", "wall steps")
─────────────────────────────────────────────────────────────────────────────────────
Orientation            Horizontal rings / lines at       Vertical streaks along the
                       each ON interface                 wall, around the hole
Period                 Pair pitch p (50 nm) in depth     Azimuthal; tens of nm
                                                         around the circumference
Origin                 Different lateral behaviour of    Mask edge roughness (LER)
                       oxide and nitride; front shape;   transferred and propagated
                       interfaces; post-etch clean       down the wall
Amplitude (typical)    0.5–3 nm after etch; up to        1–5 nm; hole non-
                       5–10 nm after aggressive clean    circularity
Grows with             Exposure time, ρ mismatch,        Mask roughness, mask
                       lateral etch, HF clean            facet, low polymer
Measured by            TEM; CD-SAXS superlattice peaks   Top-down SEM of the
                       at q_z = 2π/p                     opening; plan-view TEM at
                                                         depth
```

Both matter for a memory hole, where the wall becomes part of the cell. For slits and contacts, layer modulation matters mainly through the post-etch clean and fill.

---

## 10.2 Layer Modulation From Lateral Etch

### 10.2.1 The Model

After the front passes a given depth, the wall there remains exposed to the plasma for the rest of the etch. Under passivation, the wall etches laterally at a small rate r_lat, which differs between the two films. The step between adjacent layers grows as:

```
δ(z) = |r_lat,ox − r_lat,N| · t_exp(z)

t_exp(z) = t_total − t(z)      (time from when the front passed z to the end)
```

### 10.2.2 Reference Calculation

Use t(A) = 0.288(A + A²/180) min, a total of 45.1 min including overetch, and an illustrative lateral-rate difference of Δr_lat = 0.05 nm/min:

```
Depth (µm)   t(z) (min)   t_exp (min)   δ (nm)
──────────────────────────────────────────────
 0.5           1.7          43.5         2.2
 1.0           3.4          41.7         2.1
 2.0           7.2          37.9         1.9
 4.0          16.0          29.1         1.5
 6.0          26.3          18.8         0.9
 8.0          38.2           6.9         0.3
 8.4          40.8           4.3         0.2
```

**Modulation is largest at the top and fades toward the bottom**, because the top wall is exposed for the whole etch. A lateral-rate difference of only 0.05 nm/min produces 2 nm steps near the top, the size of the specification in Chapter 1.

### 10.2.3 Where the Lateral Rate Is Highest

The lateral rate is not uniform with depth. It rises where ions strike the wall, which is at the bow depth (Chapter 11, typically 1–3 µm), and where the polymer is thinnest. So the actual amplitude profile is the exposure time multiplied by a lateral rate that peaks near the bow:

```
δ(z) = Δr_lat(z) · t_exp(z)

If Δr_lat at the bow depth (2 µm) is 2× the value elsewhere:
  δ(2 µm) ≈ 2 × 0.05 × 37.9 = 3.8 nm   (peak of the modulation profile)
```

**The worst modulation usually sits at the bow depth**, not at the very top. Bow and modulation share a cause (wall ion flux) and are best treated together.

### 10.2.4 Which Film Recesses

Under fluorocarbon passivation, oxide tends to keep a thinner wall polymer, as at the front (Chapter 4). It therefore often etches laterally slightly faster than nitride, and the oxide layers end up recessed. When the chemistry is rich in hydrogen or in O₂ (late steps supporting the nitride rate, Chapter 7), the nitride lateral rate can rise and the sign can reverse. The sign matters for the cell (Section 10.5), and it is determined by depth-series TEM, not by assumption.

---

## 10.3 Other Sources of Layer Modulation

### 10.3.1 Front Shape

At the moving front, the curved bottom crosses each interface at a slightly different time at the centre and at the rim (Chapter 3, Section 3.4). If the films' vertical rates differ, the slower layer can leave a small ledge at the corner where the wall is formed:

```
Ledge size ≈ g · d · (1 − ρ)       (g ≈ 0.1–0.3: geometry factor, illustrative)

Nitride layer 28 nm, g = 0.2:
  ρ = 0.91:  0.2 × 28 × 0.09 = 0.5 nm
  ρ = 0.70:  0.2 × 28 × 0.30 = 1.7 nm
```

The front-shape term is small in a matched stack. It becomes visible near the bottom when ρ drifts down with depth (Chapter 3, Section 3.6.3), where the exposure-time term of Section 10.2 is small. **Modulation near the bottom is a sign of ρ drift.**

### 10.3.2 Interfaces

The graded transition between films (1–2 nm) has an intermediate composition and its own etch behaviour. Silicon-rich or hydrogen-rich transition zones can etch laterally faster than either film, leaving a thin groove at each interface (interface notching). This is a deposition property: the gas-switching sequence in the PECVD tool decides it (Chapter 2, Section 2.1.1).

### 10.3.3 Charging and Permittivity Contrast

Oxide (ε ≈ 4) and nitride (ε ≈ 7) layers carry different surface charge and leak charge at different rates (Chapter 12). Small differences in local wall potential deflect grazing ions into one film more than the other. The effect is second-order but has the same period as the stack.

---

## 10.4 Post-Etch Clean: The Largest Amplifier

### 10.4.1 Dilute HF

After the etch and ash, a wet clean removes residual polymer and fluorinated residue. Dilute HF (DHF) attacks oxide much faster than nitride, and PECVD oxide faster than thermal oxide (Chapter 2):

```
Illustrative 100:1 DHF etch rates:
  Thermal oxide reference:     2.5 nm/min
  Stack PECVD oxide (4×):     10 nm/min
  Stack PECVD nitride:         0.7 nm/min

30 s DHF clean, per side:
  Oxide recess   = 10 × 0.5 = 5.0 nm
  Nitride recess = 0.7 × 0.5 = 0.35 nm
  Added modulation ≈ 4.7 nm
```

**A short DHF clean adds two to five times more modulation than the etch itself.** And because it is isotropic and depth-independent, it adds that modulation everywhere, including the bottom.

### 10.4.2 Clean Choices

```
Clean                           Oxide:nitride   Modulation added   Residue removal
                                selectivity     (illustrative)
──────────────────────────────────────────────────────────────────────────────────
100:1 DHF, 30 s                 ~14:1           ~4.7 nm            Good
Very dilute DHF, short          ~14:1           ~1–2 nm            Moderate
SC1 / APM based                 ~1:1            < 0.5 nm           Polymer: moderate
Organic/solvent-based polymer   ~1:1            ~0                 Polymer: good;
 remover                                                           fluoride: weaker
Vapour HF (controlled)          Tunable         Tunable            Good, needs
                                                                   integration
```

The choice of clean is an integration decision that involves the etch, cleaning, and the device. A smooth etch followed by an aggressive clean gives a rough wall.

---

## 10.5 What Modulation Costs

### 10.5.1 In the Memory Hole

The memory films (blocking oxide, charge-trap nitride, tunnel oxide, channel) are deposited conformally on the hole wall. They follow its modulation:

```
Effect                                  Mechanism
─────────────────────────────────────────────────────────────────────────────
Cell-to-cell Vt shift along the string  Hole radius at each word line changes
                                        gate coupling and field in the tunnel
                                        oxide
Channel and film thickness variation    Conformal ALD over steps leaves thicker
                                        films in recesses
Charge-trap coupling between cells      Continuous trap layer wraps around steps;
                                        lateral charge migration changes
Breakdown / leakage at sharp steps      Field concentration at step corners
```

```
Illustrative sensitivity: dV_t / dr ≈ 15 mV per nm of local hole radius

Modulation 2 nm (systematic, top of the hole):
  ΔV_t between top and bottom cells ≈ 2 × 15 = 30 mV (handled by trimming)
Random layer-to-layer modulation σ = 0.5 nm:
  Adds σ_Vt ≈ 7.5 mV per cell → in quadrature with other sources
```

The systematic part can be corrected by programming conditions per word line. The random part adds to the threshold-voltage distribution width, which costs read margin in TLC and QLC cells.

### 10.5.2 In Slits and Contacts

For slits, oxide recess at the slit wall is later partly filled by the word-line metal and the slit liner. Large steps can trap voids in the slit fill or thin the liner, raising leakage between the word line and the source line. For contacts, modulation mostly affects the barrier and fill. In both, the clean contributes more than the etch.

---

## 10.6 Controlling Modulation

```
Lever                                  Acts on                       Cost
──────────────────────────────────────────────────────────────────────────────────
Match ρ at every stage (Ch. 4, 7)      Front-shape term              Chemistry margin
More wall polymer in ME-1/ME-2         Lateral rate at the top/bow   Taper, clogging
 (C₄F₆, lower temperature)
Lower lateral F/O at the wall          Δr_lat                        Lower ρ, mask
 (less O₂, less NF₃ early)
Reduce bow (Ch. 11)                    Peak lateral rate             See Ch. 11
Faster etch / shorter overetch         Exposure time                 Mask budget
Sharper, cleaner interfaces in         Interface notching            Deposition time
 deposition
Matched film hydrogen and density      Lateral-rate difference       Stress, cell
Gentle post-etch clean                 Clean amplification           Residue removal
```

The biggest single improvement in most flows comes from the **clean**, followed by **ρ matching in the deep steps**, then **wall polymer at the bow depth**.

---

## 10.7 Intentional Layer-Selective Recess

Some cell designs recess one film on purpose after the etch:

```
Scheme                              Purpose                         Process
─────────────────────────────────────────────────────────────────────────────────
Oxide recess at the hole wall        Separate charge-trap layer     Controlled DHF or
 (cut trap layer between cells)      per cell; reduce lateral       vapour HF; then
                                     charge migration               conformal trap
                                                                    deposition and
                                                                    trim
Nitride recess at the hole wall      Enlarge cell gate area or      Selective nitride
                                     form isolated trap pockets     etch (hot H₃PO₄,
                                                                    or dry isotropic;
                                                                    Book #22)
```

These schemes turn layer-selective recess from a defect into a structure. They also raise the requirements on the etch: the recess must be uniform from the top to the bottom of the hole. So the etch must deliver walls with the same film composition and damage at every depth, including the bow region, where lateral ion damage changes the wet etch rate.

---

## 10.8 Measuring Modulation

```
Method                          What it gives                   Limitation
────────────────────────────────────────────────────────────────────────────────
Cross-section TEM / STEM        Direct step profile per layer   Few holes; sample
                                                                prep artefacts
CD-SAXS (transmission)          Superlattice peaks at           Array average;
                                q_z = 2π/p = 0.126 nm⁻¹; the    model-based
                                peak intensity ratio gives the
                                modulation amplitude
                                averaged over the array
Optical scatterometry (OCD)     Sensitive to strong modulation  Weak sensitivity at
                                in some models                  1–2 nm amplitude
Post-clean vs. pre-clean TEM    Separates etch and clean        Destructive
                                contributions
```

CD-SAXS is well suited to the stack because the modulation is truly periodic: its Fourier component at the pair period stands out clearly from the smooth profile (Chapter 15).

---

## 10.9 Summary & Key Takeaways

1. **Two roughnesses, two causes.** Layer modulation follows the pair period and comes from the stack. Vertical striation comes from the mask.

2. **Exposure time writes the modulation.** δ = Δr_lat × t_exp: 0.05 nm/min gives about 2 nm at the top of the reference hole and 0.2 nm at the bottom.

3. **The bow depth is the hot spot.** Lateral rate peaks where ions strike the wall, so modulation often peaks near the bow.

4. **Bottom modulation signals ρ drift.** The front-shape term g·d·(1 − ρ) grows when nitride slows at depth.

5. **The clean amplifies everything.** A 30 s 100:1 DHF clean adds about 4.7 nm of oxide recess, more than the etch itself.

6. **Modulation costs read margin.** At about 15 mV/nm, random modulation widens the V_t distribution of every cell.

7. **Recess can be a feature.** Intentional oxide or nitride recess makes isolated trap cells and requires uniform walls at every depth.

---

## Study Questions

1. With Δr_lat = 0.08 nm/min and the reference timings, compute δ at 1, 4, and 8 µm. If the bow at 2 µm doubles the lateral rate there, what is the peak?

2. ρ drifts to 0.78 in ME-3. Estimate the front-shape ledge for a 28 nm nitride layer with g = 0.25. Compare it with the exposure-time term at 8 µm from Question 1.

3. A clean uses 200:1 DHF for 20 s (stack oxide 5 nm/min, nitride 0.4 nm/min). Compute the added modulation per side. What clean time would keep it below 1 nm?

4. Using dV_t/dr = 15 mV/nm, compute the V_t spread contributed by random modulation of σ = 0.8 nm. If other sources give σ_Vt = 60 mV, what is the total?

5. Explain why CD-SAXS can measure modulation averaged over an array but cannot distinguish a uniform 1 nm modulation from a mix of 0 and 2 nm modulations in different holes.

---

**Previous Chapter:** [Chapter 9: Chamber Conditioning & Long-Recipe Stability](./09-chamber-conditioning-stability.md)  
**Next Chapter:** [Chapter 11: Profile Control — Bow, Necking, Taper & Bottom CD](./11-profile-bow-taper.md)

---

**Chapter 10 Development Status:** Complete  
**Version:** 1.0
