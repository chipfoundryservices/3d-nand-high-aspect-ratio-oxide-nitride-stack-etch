# Chapter 7: Recipe Architecture — Steps, Ramps & Deck Transitions

## Overview

A production ON-stack recipe is not one etch condition held for 40 minutes. It is a sequence of five to ten steps, each tuned to a depth range, with transitions between them and a separate treatment for the non-periodic layers: the cap, the inter-deck layer, and the landing layer. This chapter explains why the recipe is staged, builds a reference recipe for the reference hole with stage times from the ARDE model, shows how chemistry is ramped to keep oxide and nitride matched as the feature deepens, and covers the transitions that leave marks on the wall. It ends with recipe sensitivities and the differences between hole, slit, and contact recipes in the same stack.

**Learning Objectives:**
- Explain the purpose of each recipe stage from breakthrough to overetch
- Compute stage times and mask consumption from the ARDE time model
- Design chemistry ramps that hold the oxide/nitride rate ratio as the feature deepens
- Describe the inter-deck joint and estimate its alignment budget
- Quantify the depth error caused by parameter drifts of 1%
- Adapt the recipe structure to slits and through-array contacts

---

## 7.1 Why the Recipe Is Staged

### 7.1.1 What Changes With Depth

```
Quantity                  Top of the feature        Bottom of the feature
──────────────────────────────────────────────────────────────────────────────
Aspect ratio              0–20                      80–95
Ion pass fraction         ~1 at any energy          0.4–0.5 (energy-limited)
Neutral supply            Plentiful                 ~1% of the opening
Rate ratio ρ              0.91 (matched)            0.82 (nitride slow; Ch. 3)
Risk                      Mask facet, top bow,      Taper, bottom-CD collapse,
                          necking                   clogging, twisting
What the step needs       Polymer, low energy       Energy, nitride support,
                                                    less polymer
```

A single condition cannot satisfy both ends. The recipe is divided at depths where the dominant risk changes.

### 7.1.2 Stage Functions

```
Stage                Purpose
──────────────────────────────────────────────────────────────────────────────
BT (breakthrough)    Remove SiON cap/native residue on the a-C openings
CAP                  Etch cap oxide; set the initial wall angle and top CD
ME-1                 Upper stack: protect mask and top wall; low energy;
                     high polymer
ME-2                 Middle stack: raise energy; balance polymer and rate
ME-3                 Lower stack: high energy; nitride support (more H, less
                     polymer); declogging
LS (landing)         Selective step into the landing layer
OE (overetch)        Bring the slowest features to the landing layer
Flash/declog         Short F- or O-rich steps to clear polymer from the
(optional, inserted) feature necks
```

---

## 7.2 The Reference Recipe

### 7.2.1 Stage Depths and Times

Stage times follow from the ARDE time model of Chapter 3, t(A) = 0.288 × (A + A²/180) min, which describes the staged recipe as a whole:

```
Stage   Depth range (µm)   A at end   Cumulative t (min)   Stage time (min)
──────────────────────────────────────────────────────────────────────────
CAP     0 – 0.3             3.3         1.0                  1.0
ME-1    0.3 – 3.0          33.3        11.4                 10.4
ME-2    3.0 – 6.0          66.7        26.3                 14.9
ME-3    6.0 – 8.2          91.1        39.5                 13.2
LS      8.2 – 8.4 (+stop)  93.3        41.1                  1.6 (slower,
                                                                  selective)
OE      —                   —          45.1                  4.0 (≈10%)
───────────────────────────────────────────────────────────────────────────
Total                                                       45.1 min
```

### 7.2.2 Conditions

```
Parameter          CAP     ME-1    ME-2    ME-3    LS      OE
─────────────────────────────────────────────────────────────────────────
Pressure (mTorr)   25      20      20      15      20      20
Source 60 MHz (kW) 2.5     3.0     3.0     3.0     2.5     2.5
Bias 400 kHz (kW)  6       8       12      15      8       8
Mean energy (keV)  2.5     3.0     4.5     6.0     3.5     3.5
Bias pulsing       CW      CW      5 kHz,  5 kHz,  CW      CW
                                   70%     50%
C₄F₆ (sccm)        30      45      40      30      50      45
C₄F₈ (sccm)        20      20      20      15      10      10
CH₂F₂ (sccm)       10      20      25      35      0       0
O₂ (sccm)          30      30      35      30      15      20
NF₃ (sccm)         0       0       5       10      0       0
Ar (sccm)          150     150     150     150     200     200
Chuck (°C)         20      20      20      20      20      20
```

*(Illustrative values for a conventional, non-cryogenic process. They are starting points for a DOE, not qualified conditions.)*

Trends to notice:

- **Energy rises** from 2.5 to 6.0 keV with depth (Chapter 6, Section 6.5).
- **C₄F₆ falls** in ME-3 to reduce polymer at the bottom and limit clogging.
- **CH₂F₂ rises** in ME-3 to support the nitride rate as ρ drifts down (Section 7.3).
- **NF₃ appears** in ME-2 and ME-3 to clear polymer at the neck.
- **Pressure falls** in ME-3 to narrow the ion angle.
- **LS removes CH₂F₂ and NF₃** and raises C₄F₆ for selectivity to poly-Si.

### 7.2.3 Mask Budget of the Recipe

```
Stage   Time (min)   Mask erosion (nm/min, illustrative)   Mask used (nm)
─────────────────────────────────────────────────────────────────────────
BT      0.3          60                                      18
CAP     1.0          40                                      40
ME-1    10.4         38                                     395
ME-2    14.9         45                                     671
ME-3    13.2         52                                     686
LS      1.6          35                                      56
OE      4.0          38                                     152
─────────────────────────────────────────────────────────────────────────
Total   45.4                                               2018 nm

Starting mask: 2400 nm a-C + 50 nm SiON (the SiON takes 50 of the 58 nm
  used in BT and CAP)
a-C consumed: 2018 − 50 = 1968 nm
Remaining a-C at centre: 2400 − 1968 ≈ 430 nm
```

The edge typically loses 5–10% more mask than the centre, which leaves about 230–330 nm there. That straddles the 300 nm specification (Chapter 1), so the reference recipe has essentially no mask margin at the edge. Chapter 13 handles this budget in detail.

---

## 7.3 Ramping Chemistry to Hold the Rate Ratio

### 7.3.1 The Drift to Correct

Chapter 3 showed that if nitride slows more with depth than oxide, ρ falls from 0.91 at the top to about 0.82 at the bottom. Left alone, the lower stack would develop larger striation and a rougher bottom (Chapters 3 and 10).

### 7.3.2 The Correction

Using the illustrative matrix of Chapter 4 (CH₂F₂ +10% → R_N +4%, R_ox 0%):

```
Target: keep ρ ≈ 0.90 in ME-3 (A ≈ 67–91, uncorrected ρ ≈ 0.83)
Required change in R_N/R_ox: 0.90 / 0.83 = 1.084 → +8.4%

CH₂F₂ steps (+10% each): 8.4 / 4 ≈ 2.1 → +21% CH₂F₂
  From the ME-2 value of 25 sccm: 25 × 1.21 ≈ 30 sccm

The reference ME-3 uses 35 sccm (+40%). The extra beyond 30 sccm offsets
the lower C₄F₆ (less polymer helps oxide slightly more than nitride at
this point) and keeps a small margin at the very bottom (A ≈ 91).
```

### 7.3.3 Checking the Ramp

The ramp is verified on a **depth series** (Appendix C.1): wafers stopped at the end of each stage and cross-sectioned. Striation amplitude and bottom shape at each depth show whether ρ is held. Measuring blanket-film rates in ME-3 conditions is not enough, because the transport at depth is part of the drift.

---

## 7.4 Transitions Between Steps

### 7.4.1 Step Marks

When conditions change between steps, the wall formed during the transition has a different polymer state and lateral etch than the walls above and below it. The result is a **step mark**: a ring or line on the wall at the depth where the transition happened.

```
Transition duration and the depth it occupies:

Transition at 6.0 µm (ME-2 → ME-3), local rate ≈ 179 nm/min = 3.0 nm/s
  Abrupt change, 3 s settling:       9 nm of wall affected
  Ramped change over 15 s:          45 nm, but smaller amplitude
```

### 7.4.2 Good Transition Practice

```
Practice                                 Reason
────────────────────────────────────────────────────────────────────────────
Keep the plasma on between steps         Avoid re-ignition transients and
                                         charge-up
Ramp bias and gas flows over 5–20 s      Spread the polymer change over depth
Change one major parameter at a time     Avoid a combined shock to polymer
 when possible                           and sheath
Match the stabilization of pressure      Throttle-valve settling of 1–3 s
 and flow                                otherwise gives a pressure spike
Place transitions at non-critical depths Avoid transitions at the depth of
                                         maximum bow or at deck joints
```

---

## 7.5 Non-Periodic Layers in the Recipe

### 7.5.1 The Cap

The cap oxide (100–300 nm) is pure oxide, so it etches faster than the stack and carries less polymer. The CAP step sets the initial wall angle. A slightly tapered (88.5–89.5°) cap wall reduces the facet on the mask and limits top bow. A vertical or re-entrant cap wall starts the bow early (Chapter 11).

### 7.5.2 The Inter-Deck Joint

In a two-deck flow, deck-1 holes are etched, filled with a sacrificial plug (poly-Si or carbon), and covered with an inter-deck layer (IDL) and deck 2. The deck-2 etch must:

1. Etch through the deck-2 stack
2. Cross the IDL, which may be thicker oxide or a special joint layer
3. Land in the deck-1 plug, aligned to the deck-1 hole

```
Joint alignment budget (illustrative):

Deck-1 hole top opening (enlarged joint pad):    CD_j = 120 nm
Deck-2 hole bottom:                              CD_b = 75 nm
Allowed offset: (CD_j − CD_b)/2 = 22.5 nm

Contributors (3σ):
  Litho overlay deck 2 to deck 1:       12 nm
  Deck-1 top displacement (twist):       8 nm
  Deck-2 bottom displacement (twist):   15 nm
  Wafer-bow-induced distortion           8 nm
  Root-sum-square:  √(144 + 64 + 225 + 64) = √497 = 22.3 nm   (≈ budget)
```

The joint is one of the tightest budgets in the flow. A deck-2 recipe that lets the bottom drift by a few more nanometres (Chapter 12) uses up the whole margin.

### 7.5.3 The IDL Step

An oxide IDL etches about 6% faster than the stack (330 vs. 312.5 nm/min open-area rate) and carries less polymer. If the ME-3 conditions run through it unchanged, it bows slightly at the joint. Recipes either insert a short IDL step with more polymer or adjust the deck-2 ME-3 to tolerate pure oxide at the bottom.

---

## 7.6 Recipe Sensitivity

### 7.6.1 Depth Change From a 1% Drift

At fixed time, the change in final depth from small parameter drifts (illustrative sensitivities for the reference recipe):

```
Parameter (1% drift)       ΔR_eff     Δdepth at fixed time    Other effects
──────────────────────────────────────────────────────────────────────────────
Bias power                 +0.5%      +42 nm                  Bow +, mask −
Source power               +0.3%      +25 nm                  Uniformity
O₂ flow                    +0.2%      +17 nm                  ρ +, mask −
C₄F₆ flow                  −0.2%      −17 nm                  ρ −, taper +
CH₂F₂ flow                 +0.2%      +17 nm                  ρ +
Pressure                   −0.3%      −25 nm                  Angle wider
Chuck temperature (+1 °C)  +0.1%      +8 nm                   Polymer −
Stack thickness            —          −84 nm to landing       Time to land
                                       (+1% thicker)          +1%
```

### 7.6.2 What This Means

The stack thickness is the largest single contributor: a 1% thicker deck needs 1% more time to land. Recipe drifts of 1% each, combined, are similar in size. The overetch must cover all of them, plus the across-wafer front spread (Chapter 13). Feed-forward of stack thickness (Chapter 15) removes the largest term.

---

## 7.7 Holes, Slits, and Contacts

The same staged structure applies to every through-stack feature, with different emphasis:

```
Feature          Distinctive recipe features
───────────────────────────────────────────────────────────────────────────────
Memory hole      Energy-limited; strongest ARDE; most pulsing; tightest bottom
                 CD and twist control; deck joint landing
Slit             Faster (A₀ larger); thicker mask; edge tilt over a long line;
                 landing in the source stack with partial punch-through;
                 single pass through both decks or per-deck slits
Support holes    Etched through staircase fill oxide over a partial ON stack;
                 depth varies with the step underneath; lands on a stop layer
Through-array    Widest and deepest; mostly through both decks at once
 contact         (~17 µm); lands on metal; heavy polymer near the end for
                 metal selectivity; arcing risk on large open area
```

A fab usually develops a **platform recipe** for the stack (ratios, ramps, transitions) and adapts it per feature, rather than developing each from scratch. A stack change then becomes a platform update that propagates to every feature recipe.

---

## 7.8 Summary & Key Takeaways

1. **Stage by depth.** Top steps protect the mask and top wall with polymer and low energy. Bottom steps need energy, nitride support, and declogging.

2. **The reference recipe takes about 45 minutes.** 40.6 min to reach the landing layer and 4 min of overetch. It uses about 2.0 µm of the 2.4 µm mask, leaving almost no margin at the wafer edge.

3. **Ramp chemistry to hold ρ.** About +20–40% CH₂F₂ in the deepest step offsets the drift from 0.91 to 0.82.

4. **Transitions leave marks.** Keep the plasma on, ramp over 5–20 s, and keep transitions away from bow and joint depths.

5. **The deck joint is the tightest budget.** About 22 nm of allowed offset is spent by overlay and two decks of bottom displacement.

6. **Stack thickness is the largest drift.** 1% more stack needs 1% more time to land. Feed-forward removes it.

7. **One platform, many features.** Holes, slits, support holes, and contacts share the stack recipe structure and differ in emphasis.

---

## Study Questions

1. Using t(A) = (w̄/R₀)(A + A²/2A₀) with the reference values, compute the stage times if ME-1 ends at 2.5 µm and ME-2 ends at 5.5 µm. Which stage is the longest?

2. Using the mask erosion rates in Section 7.2.3, compute the remaining mask if ME-3 erosion rises to 60 nm/min and OE is extended to 6 min.

3. A deck-2 recipe change increases bottom displacement from 15 to 20 nm (3σ). Recompute the joint RSS budget. What joint pad CD would restore the margin?

4. The ME-2 → ME-3 transition is moved from 6.0 to 7.0 µm. Compute the new local rate at the transition and the depth occupied by a 10 s ramp.

5. If the stack is 1.5% thick at the wafer edge and the bias delivers 1% less power at the edge, estimate the extra time needed for edge features to land. How much extra mask does that cost at 52 nm/min?

---

**Previous Chapter:** [Chapter 6: Ion Energy, Angular Spread & Bias Waveform Engineering](./06-ion-energy-waveforms.md)  
**Next Chapter:** [Chapter 8: Wafer Temperature, Cryogenic Etch & Heat Flow](./08-temperature-cryogenic-etch.md)

---

**Chapter 7 Development Status:** Complete  
**Version:** 1.0
