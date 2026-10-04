# Chapter 14: Scaling to 300–1000 Layers — Decks, Thinner Pairs & Next-Generation Etch

## Overview

Every generation of 3D NAND adds layers, and every added layer is more stack to etch. Some of the growth is absorbed by thinner pairs, some by splitting the stack into more decks, and some by better etch. This chapter brings together the per-deck limits from the earlier chapters into a single design-space model. It shows that time, mask, bottom CD, and twist all bind at nearly the same deck height in the reference process. It then compares deck counts on etch time and cost, examines what thinner pairs do to the etch, and evaluates the next-generation options (cryogenic HF chemistry, high-energy tailored and pulsed bias, better masks, and engineered stacks) by how far each moves the per-deck limit.

**Learning Objectives:**
- Compute the maximum deck height allowed by each of the four per-deck constraints
- Explain why an optimized process sits where several constraints bind together
- Compare etch time and cost for different deck counts at a given layer count
- Describe the etch consequences of thinner pairs
- Estimate how cryogenic chemistry, higher ion energy, and better masks move the per-deck limit
- Build a scaling roadmap for stack height, decks, and etch time per wafer

---

## 14.1 How Much Stack

```
H_total = N_pairs · p + n_decks · h_overhead + (n_decks − 1) · h_IDL

Generation (WL)   Total pairs   p (nm)   Pair height   Overhead (2–3 decks)   H_total
─────────────────────────────────────────────────────────────────────────────────────
300+ (ref.)        320           50       16.0 µm       0.8 + 0.4 µm           17.2 µm
400+               440           45       19.8 µm       0.8 + 0.4              21.0 µm
500+               540           42       22.7 µm       1.2 + 0.8              24.7 µm
1000 (outlook)    1080           40       43.2 µm       1.6–2.4 + 1.2–2.0      46–48 µm
```

*(Illustrative. Total pairs include dummy and select levels.)*

At 1000 layers, even with 40 nm pairs, the stack is about 45 µm tall. At today's per-deck limit of about 8–9 µm, that would mean five or six decks. The economics of 3D NAND scaling are now largely the economics of the per-deck limit.

---

## 14.2 The Per-Deck Limit

### 14.2.1 Four Constraints

Using the reference hole (w̄ = 90 nm, R₀ = 312.5 nm/min, A₀ = 90) and the models of earlier chapters:

```
Constraint 1 — Time: main etch ≤ 45 min (throughput target)
  0.288 (A + A²/180) ≤ 45 → A ≤ 100.3 → H ≤ 9.03 µm

Constraint 2 — Mask: 45 nm/min × (t + 4 min OE) × 1.10 + 300 nm ≤ 2400 nm
  t ≤ 38.4 min → A ≤ 89.2 → H ≤ 8.02 µm

Constraint 3 — Bottom CD ≥ 70 nm (two-zone taper, Chapter 11)
  105 − 8.7 − 2 × 3.14×10⁻³ × (H − 5000 nm) ≥ 70 → H ≤ 9.19 µm

Constraint 4 — Twist 3σ ≤ 25 nm (σ_x ∝ H^(3/2), Chapter 12)
  H ≤ 8.4 × (8.33 / 7.95)^(2/3) = 8.67 µm
```

### 14.2.2 The Design Space

```
Constraint        H_max (µm)   Reference H = 8.4 µm
────────────────────────────────────────────────────
Mask (edge)        8.0          Violated by 0.4 µm (no edge margin; Ch. 13)
Twist              8.7          Margin 0.3 µm
Time               9.0          Margin 0.6 µm
Bottom CD          9.2          Margin 0.8 µm
```

**All four limits fall between 8.0 and 9.2 µm.** That is not a coincidence. A mature process is one in which effort has gone into whichever constraint was binding until several bind together. To make a taller deck, every constraint has to move, not just one. An improvement in only one of them (for example a faster chemistry) buys almost nothing if the others stay put.

### 14.2.3 What Moves Each Constraint

```
Constraint     Moved by
──────────────────────────────────────────────────────────────────────────────
Time           Higher R₀, larger A₀ (cryogenic HF, high-peak pulsing, energy)
Mask           Higher-selectivity mask, less erosion per µm, less overetch
Bottom CD      Less polymer at depth with the same protection (cryogenic,
               tailored IED), ρ held at depth, larger top CD
Twist          Higher energy (δθ ∝ 1/V_i), better charge relief (pulsing,
               tailored waveforms), shorter deck
```

---

## 14.3 How Many Decks

### 14.3.1 Etch Time Versus Deck Count

The ARDE time grows faster than depth, so more, shorter decks need less etch time:

```
Reference stack, 16.8 µm of ON (hole w̄ = 90 nm):
  1 deck of 16.8 µm (A = 187):  t = 0.288 × (187 + 194) = 109.5 min
  2 decks of 8.4 µm (A = 93):   t = 2 × 40.8           =  81.6 min

400+ layer stack, ~21 µm, compared for 2 and 3 decks (ON only, w̄ = 90 nm):
  2 decks of 10.5 µm (A = 117): t = 2 × 55.4 = 110.8 min
  3 decks of 7.0 µm (A = 78):   t = 3 × 32.1 =  96.2 min
```

### 14.3.2 What a Deck Costs Besides Etch

Each deck adds a full set of non-etch steps:

```
Per-deck adder (illustrative)
───────────────────────────────────────────────────────────────
Stack deposition (split, not extra)     ~0 (same total layers)
Hard mask deposition                    Yes
Lithography (critical layer + overlay)  Yes
Mask open and strip                     Yes
Plug fill, CMP, and plug removal        Yes
Joint (IDL) deposition and joint etch   Yes
Metrology and inspection                Yes
```

### 14.3.3 The Trade

```
Etch chamber cost per minute (Chapter 16): ≈ $3 (depreciation + consumables)

400+ layers, 3 decks vs. 2 decks:
  Etch time saved:            14.6 min → ≈ $44 per wafer
  Extra deck of non-etch:     ≈ $80–150 per wafer (illustrative)
  Two decks of 10.5 µm:       violate all four limits of Section 14.2
                              with today's process
```

Three decks cost more in non-etch steps than they save in etch time. But two decks of 10.5 µm are not feasible with the reference process. **The decision is set by whether the per-deck limit can be raised to the needed height, not by etch time alone.** A process improvement that moves all four constraints to 10.5 µm saves a deck and is worth far more than its effect on etch time.

---

## 14.4 Thinner Pairs

### 14.4.1 What Changes When p Falls From 50 to 40 nm

```
Effect                                  Direction    Reason
────────────────────────────────────────────────────────────────────────────────
Stack height for a given layer count    −20%         H = N·p
Pair time at the bottom                 19.5 → 15.6 s
Interface transient share per layer     +25%         Fixed extra depth per interface
                                                     (Ch. 3, Section 3.3.3); films
                                                     look better matched
Front span in pairs                     0.6 → 0.75   Same 30 nm sag over a shorter
                                                     period; more averaging
Absolute layer modulation               Unchanged    Set by Δr_lat × t_exp
Modulation relative to the layer        +25%         Same steps on thinner layers
Layer thickness control                 Harder       Same absolute σ is a larger
                                                     fraction
Word-line resistance                    Higher       Thinner metal; drives the move
                                                     to Mo and other metals
Interlayer breakdown/coupling           Worse        Thinner oxide
```

For the etch, thinner pairs are mostly neutral or slightly helpful: the stack is shorter and behaves more like a uniform material. The difficulty moves to the device (resistance and coupling) and to the films (thickness control), and back to the etch only through modulation, which matters more relative to a thinner layer.

### 14.4.2 The Limit of Thinning

Pair pitch below about 40 nm runs into the word-line resistance and cell interference limits. Layer count growth then has to be carried by height again, so the per-deck limit becomes the main scaling lever.

---

## 14.5 Next-Generation Etch

### 14.5.1 Cryogenic HF-Based Etch

Published reports describe two to three times higher rates at depth (Chapter 4, Section 4.6). In the ARDE model, model this as R₀ doubled and A₀ raised to 150:

```
R₀ = 625 nm/min, A₀ = 150, w̄ = 90 nm → w̄/R₀ = 0.144 min

Single 16.8 µm deck (A = 187):
  t = 0.144 × (187 + 187²/300) = 0.144 × (187 + 116) = 43.6 min
```

The time constraint for a single 16.8 µm deck would be met. Twist (∝ H^(3/2)) and bottom CD would still need their own improvements: at the same σ_δθ, twist at 16.8 µm would be 2.8 times the reference. Cryogenic etch moves the time and mask limits most. The other two limits need charge control and profile control as well.

### 14.5.2 Higher Ion Energy and Tailored Waveforms

```
Energy 5 → 10 keV (pulsed, same average power, Chapter 6):
  Pass fraction at A = 93: 0.44 → 0.69
  Twist deflection δθ ∝ 1/V_i: halved → twist limit H_max × 2^(2/3) = 1.59×
  Bottom/top rate ratio: 0.44 → 0.68 (larger effective A₀)
  Costs: generator power, arcing margin, parts wear
```

Higher energy is the single most effective lever on twist and on ARDE. Tailored waveforms raise the useful energy without raising the peak, which makes it more affordable.

### 14.5.3 Masks

Doped and denser carbon masks lower erosion by 30–50% (Chapter 13). That moves the mask constraint from 8.0 µm to about 10 µm at the same thickness. Metal-containing masks offer more but bring contamination and strip problems.

### 14.5.4 Stacks Designed for Etch

The stack itself can be engineered:

```
Option                                 Etch benefit                     Device / film cost
───────────────────────────────────────────────────────────────────────────────────────────
Nitride composition tuned for ρ ≈ 1    Less modulation; simpler ramps   Stress; retention
 at depth
Oxide/nitride with graded doping       Compensates ARDE drift of ρ      Deposition complexity
 by depth
Sharper interfaces                     Less interface notching          Deposition time
Stress-balanced stack (Ch. 2)          Less bow; less tilt; easier      Nitride composition
                                       chucking
Thinner overhead layers                Less height                      Integration margins
```

### 14.5.5 Process Concepts

- **Deposition–etch cycling**: alternating short passivation and etch steps to control bow and taper independently
- **Quasi-atomic-layer landing**: cyclic, self-limiting steps at the bottom for very high landing selectivity
- **Data-driven recipe control**: per-wafer adjustment of stage times and ramps from upstream data (Chapter 15)

---

## 14.6 A Scaling Roadmap

```
                       Today (ref.)      Next              Outlook
────────────────────────────────────────────────────────────────────────────────
Word lines              300+              400–500           1000
Pair pitch              50 nm             42–45 nm          ~40 nm
ON stack                ~17 µm            21–25 µm          ~45 µm
Per-deck limit          8–9 µm            10–12 µm          12–16 µm (cryo,
                                                            high-E, new masks)
Decks                   2                 2–3               3–4
Hole etch per wafer     ~82 min           ~95–110 min       ~150–200 min
 (all decks, etch only)
Key enablers            Pulsed LF bias,   Cryogenic HF,     Tailored high-E
                        a-C mask, ramps   doped masks,      waveforms, new
                                          tailored IED      stacks, cyclic etch
```

*(Illustrative trend values.)*

The per-deck limit is what keeps the number of decks down. If it stayed at 8–9 µm with today's rates, a 1000-layer product would need six decks of about 7.2 µm: roughly 200 min of hole etch per wafer, plus six sets of litho, mask, and plug steps. The outlook column assumes the limit rises to 12–16 µm with faster chemistry. Etch time is then similar, but there are half as many decks.

---

## 14.7 Summary & Key Takeaways

1. **The stack keeps growing.** About 17 µm for 300+ layers today; about 45 µm at 1000 layers even with 40 nm pairs.

2. **Four limits bind together.** Mask (8.0 µm), twist (8.7), time (9.0), and bottom CD (9.2) all sit near the 8.4 µm reference deck.

3. **Improving one limit is not enough.** A taller deck needs time, mask, bottom CD, and twist to move together.

4. **More decks save etch time but cost process steps.** For 400+ layers, a third deck saves about 15 min of etch but adds more than that in litho, mask, and plug steps.

5. **Thinner pairs are mostly neutral for the etch.** They shorten the stack and improve averaging. The difficulty moves to the device and the films.

6. **Cryogenic etch moves time and mask; energy moves twist and ARDE.** In the illustrative model, cryogenic HF meets the time limit for a single 16.8 µm deck, and 10 keV pulsed bias raises the twist-limited height by 1.6×.

---

## Study Questions

1. Recompute the four per-deck limits for a hole with w̄ = 100 nm (CD_top 115 nm, same taper model shifted by +10 nm, same twist parameters). Which limit binds?

2. A doped mask cuts erosion by 40%. Compute the new mask-limited deck height. Which constraint now binds?

3. For a 500-layer stack (24.7 µm total, ON only ~22.7 µm), compare etch time for 2, 3, and 4 decks with the reference ARDE. At $3/min of etch and $110 per deck adder, which is cheapest if the per-deck limit is 10 µm?

4. Using the cryogenic model (R₀ = 625 nm/min, A₀ = 150), compute the time for a 12 µm deck. With twist ∝ H^(3/2) and the reference twist parameters, what charging deflection σ_δθ would keep 3σ twist at 25 nm?

5. Explain why thinner pairs make the interface transient more important but make layer modulation relatively worse.

---

**Previous Chapter:** [Chapter 13: Mask Selectivity, Landing & Loading Between Features](./13-mask-landing-loading.md)  
**Next Chapter:** [Chapter 15: Endpoint, Layer-Resolved Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)

---

**Chapter 14 Development Status:** Complete  
**Version:** 1.0
