# Chapter 4: ON Etch Chemistry — Fluorocarbons, Hydrogen & Rate Matching

## Overview

Most dielectric etch chemistries are designed for selectivity: etch oxide and stop on nitride, or the reverse. An ON-stack etch has to do the opposite. It must remove oxide and nitride at nearly the same rate, protect the sidewall of both with the same polymer, erode the carbon mask as little as possible, and then switch to high selectivity when it reaches the landing layer. This chapter explains how fluorocarbon plasmas etch oxide and nitride, why hydrogen and oxygen act so differently on the two films, how the gas mixture is used to match their rates, and what cryogenic and hydrogen-fluoride-based chemistries change. It ends with the oxide/polysilicon stacks used in gate-first designs.

**Learning Objectives:**
- Describe the ion-enhanced etch mechanisms of SiO₂ and Si₃N₄ under fluorocarbon plasma
- Explain why oxygen in the film keeps the polymer thin on oxide, and how nitrogen and hydrogen act on nitride
- Use a linear rate-matching matrix to choose gas changes that restore a target rate ratio
- Compute mask selectivity at the top and bottom of a feature and over a whole etch
- Estimate how adsorption of HF or fluorocarbon species changes with wafer temperature
- Describe the chemistry changes needed for oxide/polysilicon stacks

---

## 4.1 Etching Oxide in a Fluorocarbon Plasma

### 4.1.1 Mechanism

Silicon dioxide is etched by fluorine and fluorocarbon species with the help of energetic ions. The net reactions are of the form:

```
SiO₂ + CF_x (adsorbed) + ion energy → SiF₄ + CO / CO₂ / COF₂
```

The ion breaks Si–O bonds in a damaged surface layer, fluorine bonds to silicon, and carbon from the fluorocarbon leaves with the oxygen. **Oxygen in the film removes carbon.** This is the key to oxide etch: the oxide burns off part of the polymer that the plasma deposits on it. The steady-state fluorocarbon film on oxide is therefore thin, often 1–2 nm under HAR conditions.

### 4.1.2 Consequences

```
Property                         Consequence for ON etch
─────────────────────────────────────────────────────────────────────────
Thin polymer on oxide            Oxide etch is robust to polymerizing
                                 gases (C₄F₆, C₄F₈)
Rate set mostly by ion flux ×    Oxide rate follows bias power closely
 yield                           and depends little on F-atom density
Carbon consumed at the front     Oxide tolerates high C/F ratios that
                                 would stop nitride
```

---

## 4.2 Etching Nitride in a Fluorocarbon Plasma

### 4.2.1 Mechanism

Silicon nitride contains no oxygen to consume carbon. Nitrogen must leave as volatile species:

```
Si₃N₄ + CF_x + H + ion energy → SiF₄ + HCN / FCN / C₂N₂ / N₂ / NF_x
```

Carbon from the polymer can combine with nitrogen to form CN-containing products, which helps, but less effectively than oxygen removes carbon from oxide. The steady-state polymer on nitride is therefore thicker than on oxide, and the nitride rate is more sensitive to the polymer balance.

### 4.2.2 The Role of Hydrogen

Hydrogen is the most important lever on the nitride rate:

```
Source of hydrogen          How it helps nitride
───────────────────────────────────────────────────────────────────────────
Hydrogen in the film        Si–H and N–H weaken the network and leave as
(12–25 at%, Ch. 2)          HCN and HF
Hydrofluorocarbon gases     Supply H at the surface → HCN formation;
(CH₂F₂, CHF₃, CH₃F)         H scavenges F in the gas, raising C/F and polymer,
                            which reduces oxide rate slightly
H₂, HBr, HF                 H supply; HF also an etchant at low temperature
                            (Section 4.6)
```

Hydrofluorocarbons are used in nitride-selective etches (Book #22) precisely because they raise the nitride rate relative to oxide. In an ON-stack etch they are used in small amounts to **bring the nitride rate up to the oxide rate**.

### 4.2.3 The Role of Oxygen

Added O₂ removes polymer from both films. On oxide, where the polymer is already thin, the rate rises little. On nitride, where the polymer is thicker and limits the rate, it rises more. So O₂ raises ρ = R_N/R_ox, but it also erodes the carbon mask and thins sidewall protection, which increases bow (Chapter 11).

---

## 4.3 Matching the Rates

### 4.3.1 The Knob Table

```
Knob (increase)       R_ox     R_N      ρ        Mask        Profile side effect
                                                  erosion
─────────────────────────────────────────────────────────────────────────────────────────
C₄F₆                  ≈ / −    −        −        −           More polymer: bow ↓,
                                                             taper ↑, clogging risk
C₄F₈                  ≈        − (less) −        − (less)    Weaker polymerizer
CH₂F₂                 ≈        + +      + +      −           Polymer ↑ → taper ↑
CHF₃                  +        +        ≈ / +    ≈           Higher F, less polymer
O₂                    +        + +      +        + +         Bow ↑, mask ↓
NF₃                   +        +        ≈        +           Declogging, mask ↓
Ar dilution           ≈ / +    ≈ / +    ≈        +           Ion flux ↑, more
                                                             physical sputtering
Bias power / energy   +        +        ≈ / +    +           Narrower angles,
                                                             more heat
Wafer temperature ↓   −        − −      −        −           More polymer, less
                                                             lateral etch
```

### 4.3.2 A Linear Rate-Matching Matrix

Around a qualified recipe, small changes act roughly linearly. Illustrative coefficients, per +10% of each gas's reference flow (or of bias power):

```
Knob (+10%)       ΔR_ox     ΔR_N     ΔR_mask
────────────────────────────────────────────
C₄F₆               −1%       −3%      −4%
CH₂F₂               0%       +4%      −1%
O₂                 +1%       +4%      +6%
NF₃                +2%       +3%      +3%
Bias power         +4%       +4%      +5%
```

*(Coefficients are illustrative. Each fab must measure its own, on stacks, using the procedure in Appendix C.)*

### 4.3.3 Worked Example: Recovering From a Nitride Change

The deposition team lowers nitride hydrogen and densifies the film. The nitride rate falls 19% (Chapter 2, Section 2.2.3):

```
Before:  R_ox = 330, R_N = 300,  ρ = 0.91, R_eff = 312.5
After:   R_ox = 330, R_N = 243,  ρ = 0.74, R_eff = 1/(0.44/330 + 0.56/243) = 274.9
```

To restore ρ, the ratio R_N/R_ox must rise by 0.91/0.74 = 1.23.

```
Option A: CH₂F₂ alone
  Each +10% step: R_N +4%, R_ox 0% → ratio +4% per step
  Steps needed ≈ 23/4 ≈ 5.7 → +57% CH₂F₂
  Outside the linear range; polymer and taper would grow considerably.

Option B: O₂ alone
  Each +10% step: ratio ≈ +3%
  Steps needed ≈ 7.7 → +77% O₂, mask erosion +46%
  Mask budget fails (Chapter 13).

Option C: CH₂F₂ +40% and O₂ +25%
  R_N:  +16% + 10% = +26%   → 243 × 1.26 = 306.2 nm/min
  R_ox:   0% + 2.5% = +2.5% → 330 × 1.025 = 338.3 nm/min
  ρ = 0.905
  R_eff = 1 / (0.44/338.3 + 0.56/306.2) = 319.5 nm/min
  Mask erosion: −4% + 15% = +11% → 45 × 1.11 = 50 nm/min
```

Option C restores the ratio and the rate. It costs 11% more mask erosion, about 200 nm of mask over a 40-minute etch, and it pushes CH₂F₂ to the edge of its linear range. **Chemistry can compensate a film change, but every compensation spends mask or profile margin.** Where the cell allows, the cheaper fix is to keep the nitride composition in its etch-friendly window (Chapter 2, Section 2.4.3).

### 4.3.4 Why Exact Matching Is Not the Goal

ρ = 1.00 at the top does not guarantee matching at the bottom (Chapter 3, Section 3.6.3). Interface transients make the stack better matched than blanket rates suggest (Chapter 3, Section 3.3). And the profile, the mask, and the wall all have their own optima. Production recipes typically target ρ between 0.85 and 1.05 at each stage, measured on stacks, and accept the mismatch that the wall can tolerate (Chapter 10).

---

## 4.4 Mask Selectivity

### 4.4.1 How the Carbon Mask Erodes

The amorphous-carbon (a-C) mask is eroded by:

```
Mechanism                      Driven by                    Lever
────────────────────────────────────────────────────────────────────────────
Physical sputtering            Ion energy and flux          Bias, pulsing
Chemical erosion by O and F    O₂, NF₃, oxide-released O    Gas mix
Faceting at the mask edge      Angle-dependent sputtering   Polymer on mask,
                               (peak at 50–70°)             mask density
Ion-assisted H/F reactions     Hydrofluorocarbons (minor)   —
```

Fluorocarbon polymer deposits on the mask top and protects it. Highly polymerizing gases (C₄F₆) are favoured for mask selectivity.

### 4.4.2 Selectivity Through the Etch

The mask erodes at a roughly constant rate, because the mask top always sees the full plasma. The front slows with depth. So selectivity falls through the etch:

```
Reference: mask erosion 45 nm/min, constant

At the top:     S = 312.5 / 45 = 6.9
At the bottom:  S = 153.7 / 45 = 3.4
Whole etch:     S = 8400 / (45 × 40.6) = 8400 / 1827 = 4.6
```

The **bottom selectivity** sets how much mask the last micrometre costs. In the reference, the last micrometre of a hole takes 6.3 min and uses about 285 nm of mask. The first micrometre takes 3.4 min and uses 153 nm. Chapter 13 builds the full mask budget.

---

## 4.5 Landing Selectivity

At the bottom of the stack the etch must stop in a landing layer with enough selectivity to absorb the front variation (Chapter 13):

```
Landing layer                 Chemistry change for landing       Selectivity
                                                                 (ON : landing, illustrative)
──────────────────────────────────────────────────────────────────────────────────────
Doped poly-Si (source plate)  More C₄F₆, less O₂ and NF₃,         10–25
                              lower bias
Oxide/nitride buffer over     Timed; relies on rate and          ~1 (no stop)
 poly                         uniformity
W or other metal pad (TAC)    Polymerizing chemistry, no O₂;     20–50
                              avoid F-rich mixes (WF₆ volatile)
Al₂O₃ or other high-k stop    Fluorocarbon without Cl/BCl₃       > 50
(some designs)                (AlF₃ involatile)
```

The landing chemistry is more polymerizing than the main etch. In a deep feature, the extra polymer must not close the bottom before the front reaches the stop (Chapter 11, Section 11.4).

---

## 4.6 Cryogenic and HF-Based Chemistry

### 4.6.1 Why Lower Temperature

At low wafer temperature, more of the etchant arrives at the bottom of the feature as **adsorbed** species instead of gas-phase radicals. Adsorbed species can move along the wall and do not need a line of sight to the bottom. The supply problem of Chapter 3 (Section 3.5.3) is partly solved.

Langmuir coverage:

```
θ = K p / (1 + K p),     K ∝ exp(E_ads / k_B T)

For E_ads = 0.35 eV (illustrative physisorption energy):
  K(213 K) / K(293 K) = exp[(0.35 / 8.617×10⁻⁵) × (1/213 − 1/293)]
                      = exp[4062 × 0.001282] = exp(5.21) ≈ 180
```

Going from +20 °C to −60 °C raises the adsorption constant by more than two orders of magnitude. A species that barely covers the surface at room temperature can approach full coverage at cryogenic temperature.

### 4.6.2 HF as an Etchant

Hydrogen fluoride, either fed directly or formed in the plasma from H₂ with CF₄ or NF₃, etches oxide when adsorbed and activated by ions. It sticks weakly to polymer-covered walls and survives many wall collisions, so it reaches deep bottoms. Published reports of cryogenic HF-based HAR etch describe etch rates two to three times those of conventional fluorocarbon processes at similar depth. The same reports describe adequate profile control with less fluorocarbon polymer.

### 4.6.3 Nitride at Low Temperature

Nitride reacts with HF to form ammonium fluorosilicate, (NH₄)₂SiF₆, a solid salt that sublimes at around 100 °C or above. At cryogenic temperature the salt does not sublime on its own; ion bombardment must remove it. If ion flux is too low, the salt builds up and the nitride rate falls. Cryogenic ON recipes therefore balance HF supply with ion energy to keep the nitride surface clear, and rate matching at cryogenic temperature behaves differently from warm fluorocarbon processes (Chapter 8).

### 4.6.4 Trade-Offs

```
Gain                                     Cost
──────────────────────────────────────────────────────────────────────
Higher rate at depth (larger A₀)          Chiller and chuck hardware;
                                          longer temperature stabilization
Less fluorocarbon polymer; less clogging  Different sidewall protection; bow
                                          control relies on temperature
Lower mask erosion relative to rate       Salt formation on nitride;
                                          rate-matching window narrower
Lower ion energy may suffice              Wafer temperature sensitive to heat
                                          load and bow (Chapter 8)
```

---

## 4.7 Oxide/Polysilicon (OPOP) Stacks

Gate-first designs replace the nitride with doped polysilicon. The poly layers are etched by fluorine much faster and more isotropically than oxide, and by chlorine or bromine, which barely etch oxide:

```
Issue                               Response
─────────────────────────────────────────────────────────────────────────
Poly etched laterally by F atoms     More polymer; lower temperature;
 (notching at each poly layer)       HBr addition to passivate poly walls
Rate matching: F-rich etches poly    Balance with fluorocarbon for oxide;
 fast, oxide slowly                  higher bias for oxide
Poly doping changes rate             Monitor dopant level like nitride H
Landing on poly impossible           Landing in a different material
 (same as stack)                     (oxide stop or metal)
```

Most of the physics in this book applies to OP stacks. The chemistry is different, and notching at the poly layers is usually more severe than striation in ON stacks.

---

## 4.8 Summary & Key Takeaways

1. **Oxide burns its own polymer.** Oxygen in the film removes carbon, so oxide keeps a thin polymer and etches robustly in polymerizing gases.

2. **Nitride needs help.** Without oxygen, nitride carries thicker polymer. Hydrogen (from the film or hydrofluorocarbons) and O₂ raise its rate.

3. **Rate matching is a balance of knobs.** CH₂F₂ raises ρ with little mask cost but adds polymer. O₂ raises ρ but erodes the mask and increases bow.

4. **Every compensation spends margin.** Recovering a 19% nitride rate loss by chemistry costs about 11% more mask erosion in the worked example.

5. **Selectivity falls with depth.** A constant mask erosion against a slowing front: 6.9 at the top, 3.4 at the bottom, 4.6 overall.

6. **Cold surfaces hold etchant.** A 0.35 eV adsorbate is covered 180 times more strongly at −60 °C than at +20 °C, which is the basis of cryogenic HF etch.

7. **Nitride forms a salt at low temperature.** Ammonium fluorosilicate must be removed by ions, which narrows the cryogenic rate-matching window.

---

## Study Questions

1. A nitride change raises R_N from 300 to 330 nm/min (ρ = 1.0). Using the matrix in Section 4.3.2, find a combination of C₄F₆ and O₂ changes that brings ρ back to 0.92 while lowering mask erosion. What happens to R_eff?

2. Mask erosion is 50 nm/min. Compute the selectivity at the top, at A = 50, and at the bottom of the reference hole, and the overall selectivity for an etch of 40.6 min.

3. For an adsorbate with E_ads = 0.25 eV, compute the ratio of adsorption constants between −40 °C and +20 °C. If θ = 0.05 at +20 °C, what is θ at −40 °C at the same pressure?

4. Explain why O₂ raises the nitride rate more than the oxide rate, and why that makes O₂ an expensive way to fix ρ.

5. A TAC lands on tungsten. The ON-to-W selectivity is 30 and the required overetch is 12% of the main-etch time at a bottom rate of 180 nm/min. How much W is lost? How does the answer change if a fluorine-rich declogging step with selectivity 8 is used for the last 3 minutes?

---

**Previous Chapter:** [Chapter 3: Etching Alternating Layers](./03-alternating-layer-etch-physics.md)  
**Next Chapter:** [Chapter 5: Reactor & RF Systems for Extreme-Aspect-Ratio Dielectric Etch](./05-reactor-rf-systems.md)

---

**Chapter 4 Development Status:** Complete  
**Version:** 1.0
