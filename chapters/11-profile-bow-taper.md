# Chapter 11: Profile Control — Bow, Necking, Taper & Bottom CD

## Overview

A feature in an ON stack is never a perfect cylinder or slot. It widens below the mask (bow), sometimes pinches just under the top (neck), narrows steadily toward the bottom (taper), and ends in a bottom whose width decides whether the downstream films and fills will work. Every one of these deviations is the result of a balance between deposition and removal on the wall, and the balance shifts with depth. This chapter describes the anatomy of the profile, models where the bow forms and how large it grows, builds a two-zone taper model that sets the bottom CD and the depth limit, and covers clogging. It ends with a lever map that shows why profile control is a set of trade-offs rather than a single optimum.

**Learning Objectives:**
- Define the profile parameters and compute the mean taper angle from top and bottom CD
- Locate the bow depth from mask-facet reflection geometry and from wide-angle ions
- Estimate bow growth from the lateral rate and exposure time
- Build a two-zone taper model and use it to predict bottom CD and closure depth
- Describe necking and clogging and their remedies
- Use a lever map to choose recipe changes for a given profile problem

---

## 11.1 Profile Anatomy

```
              ← CD_top = 105 nm →
           ┌────────────────────────┐   a-C mask (facet at top corners)
           │                        │
  z = 0 ───┤                        ├─── top of stack (cap)
           │  ← neck (if present)   │
  z ≈ 2 µm  )                      (    max CD = bow (≤ 115 nm)
           │                        │
           │    taper zone 1        │   gentle taper
  z ≈ 5 µm  \                      /
            \   taper zone 2      /     steeper taper (polymer-rich bottom)
             \                   /
  z = 8.4 µm  └───────────────┘         CD_bottom = 75 nm, bowl-shaped
```

```
Parameter            Definition                                Reference
─────────────────────────────────────────────────────────────────────────────
CD_top               Width at the top of the stack             105 nm
CD_max (bow)         Largest width below the top               ≤ 115 nm
z_bow                Depth of CD_max                           1.5–2.5 µm
Neck                 Local minimum just below the top          None (target)
CD_bottom            Width at the landing interface            ≥ 70 nm (75 nominal)
Mean taper angle α   (CD_top − CD_bottom) / (2H)                1.79 mrad (0.10°)
Bow ratio            CD_max / CD_top                            ≤ 1.10
```

A mean wall angle of 89.9° looks vertical. But over 8.4 µm, 0.1° takes 30 nm off the width.

---

## 11.2 Where the Bow Forms

### 11.2.1 Reflection From the Mask Facet

Ions striking the sloped sidewall of the mask opening (the facet) at grazing angles reflect with most of their energy (Book #24, Chapter 3). If the mask sidewall is tilted by β from vertical, a vertical ion that grazes it reflects at about 2β from vertical. It crosses the feature and strikes the opposite wall at depth:

```
z_bow ≈ w / tan(2β)

w = 105 nm (top opening):
  β = 0.5° → 2β = 1° → z_bow ≈ 105 / 0.0175 = 6.0 µm
  β = 1.0° → 2β = 2° → z_bow ≈ 3.0 µm
  β = 1.5° → 2β = 3° → z_bow ≈ 2.0 µm
  β = 2.0° → 2β = 4° → z_bow ≈ 1.5 µm
```

As the mask erodes and its facet grows (β increases), the reflected ions strike higher on the wall. Bow forms at 1.5–3 µm for facets of 1–2°, typical in the second half of the etch.

### 11.2.2 Wide-Angle Ions

Ions outside the acceptance cone, especially the low-energy, wide-angle tail produced by sheath collisions and sinusoidal bias (Chapters 5 and 6), strike the wall directly. An ion at angle θ entering at the centre of a feature reaches the wall at depth w/(2 tan θ):

```
θ = 20 mrad (2σ at 5 keV):    z ≈ 105 / (2 × 0.020) = 2.6 µm
θ = 40 mrad (low-energy tail): z ≈ 1.3 µm
```

Both mechanisms put the maximum wall flux in the 1–3 µm range. That is why the bow sits there in nearly every HAR feature.

### 11.2.3 How Large It Grows

The bow grows on each side at the lateral rate at z_bow for the time that depth is exposed:

```
ΔCD_bow = 2 · r_lat(z_bow) · t_exp(z_bow)

z_bow = 2 µm, t_exp = 37.9 min (Chapter 10):
  r_lat = 0.12 nm/min → ΔCD = 2 × 0.12 × 37.9 = 9.1 nm → CD_max ≈ 114 nm
  r_lat = 0.15 nm/min → ΔCD = 11.4 nm             → CD_max ≈ 116 nm (fails)
```

The bow specification (≤ 115 nm) is met with only a small margin. A 25% rise in the lateral rate at the bow depth, which a thinner mask, a hotter wafer, or a few percent more O₂ can cause, breaks it.

---

## 11.3 The Neck

A neck is a local narrowing just below the top of the stack, usually at the cap or the first micrometre. It forms when polymer and redeposited material (sputtered from the mask facet) build up on the upper wall faster than ions remove them.

```
Cause                                       Remedy
────────────────────────────────────────────────────────────────────────────
Heavy polymerizer in CAP/ME-1 (C₄F₆ high)   Lower C₄F₆ or add O₂ in ME-1
Mask material sputtered from the facet      Denser mask; lower ME-1 energy;
                                            less facet
Low wall temperature in the upper stack     Wafer temperature; heat load
Flash steps too short to clear the neck     Longer O₂/NF₃ flash at the
                                            transition
```

A neck shadows the lower feature. It narrows the ion cone and reduces the neutral conductance, so it speeds up taper and can lead to clogging (Section 11.5). A neck is worse than an equal bow, because bow widens the feature while a neck restricts everything below it.

---

## 11.4 Taper and Bottom CD

### 11.4.1 Why the Feature Narrows

The wall below the bow is formed at the moving front. The local wall angle depends on the balance at the corner of the front between deposition (polymer, redeposited products) and removal (ions). As the feature deepens:

- Ion flux to the corner falls (narrower cone)
- Polymer precursors that reach the bottom deposit preferentially at the corners
- Products redeposit on the lower wall (Chapter 3, Section 3.8)

So the local taper is gentle in the upper stack and steeper in the lower stack.

### 11.4.2 Two-Zone Model

```
Zone 1: 0 – 5.0 µm,   local taper α₁ = 0.87 mrad (0.050°)
  ΔCD₁ = 2 × α₁ × 5000 nm = 8.7 nm
Zone 2: 5.0 – 8.4 µm, local taper α₂ = 3.14 mrad (0.180°)
  ΔCD₂ = 2 × α₂ × 3400 nm = 21.4 nm

CD_bottom = 105 − 8.7 − 21.4 = 74.9 nm ≈ 75 nm (reference)
```

### 11.4.3 Sensitivities

```
Change                                         New CD_bottom    Spec (≥ 70 nm)
────────────────────────────────────────────────────────────────────────────────
Reference                                       74.9 nm          Pass
Zone-2 taper +20% (more polymer at depth)       70.6 nm          Marginal
Top CD −3 nm (litho/mask open)                  71.9 nm          Pass
Deck height +1.0 µm (zone 2 extended)           68.6 nm          Fail
Zone-2 taper −20% (more NF₃/energy in ME-3)     79.2 nm          Pass, but bow
                                                                 and mask cost
```

**The lower zone controls the bottom CD.** A 1 µm taller deck, all else equal, takes 6.3 nm off the bottom, and that alone fails the specification. This is one of the four per-deck limits in Chapter 1.

### 11.4.4 Closure Depth

If the zone-2 taper continued indefinitely, the feature would close at:

```
z_close = 5.0 µm + CD(5 µm) / (2 α₂) = 5.0 + 96.3 / (2 × 3.14×10⁻³) nm
        = 5.0 µm + 15.3 µm = 20.3 µm
```

In practice the taper steepens further as the feature deepens, and the etch stops long before geometric closure, through clogging or through the collapse of the rate at the narrowing bottom.

---

## 11.5 Clogging and Etch Stop

### 11.5.1 What Happens

At high aspect ratio and with polymer-rich chemistry, deposits at the neck or on the lower wall can grow faster than the ions remove them. The feature narrows, fewer ions get through, deposition wins further, and the feature stops etching. This is **etch stop**. In a hole array it shows up as a population of unlanded holes whose depth is far short of the rest, a tail rather than a shift.

### 11.5.2 Signs and Remedies

```
Sign                                    Interpretation
──────────────────────────────────────────────────────────────────────────
Bimodal depth distribution              Some features stopped; others normal
Unlanded features concentrated where    Local polymer excess (loading, wall
 CD is small or density high            temperature)
Landing step causes stop                LS chemistry too polymerizing for the
                                        bottom CD at that point

Remedy                                  Cost
──────────────────────────────────────────────────────────────────────────
NF₃ or O₂ flash steps in ME-2/ME-3      Mask erosion; bow if placed high
Lower C₄F₆ in deep steps                Lower ρ control; less mask protection
Higher energy / pulsed high energy      Heat, mask, arcing (Ch. 6)
Shorter, more selective LS              Requires better uniformity (Ch. 13)
Cryogenic chemistry (less polymer)      Hardware (Ch. 8)
```

---

## 11.6 Profile in a Layered Stack

The profile phenomena above occur in any HAR dielectric etch. The ON stack adds:

- **Bow is modulated.** In the bow region, the film with the higher lateral rate (usually oxide) bows more. The largest layer modulation sits at the bow depth (Chapter 10).
- **The taper depends on ρ.** If nitride slows at depth (ρ falls), the nitride layers at the corner etch more slowly and leave more of the corner behind. The taper steepens in proportion. Holding ρ with chemistry ramps (Chapter 7) also helps the bottom CD.
- **Non-periodic layers change the wall.** The cap oxide, the inter-deck layer, and the landing layer each have their own lateral behaviour. A thick oxide IDL bows slightly; a poly-Si landing layer etches laterally under F-rich overetch.

---

## 11.7 The Lever Map

```
Lever (increase)       Bow      Neck     Taper /    Mask      Rate     Modulation
                                         CD_bottom  loss
──────────────────────────────────────────────────────────────────────────────────────
C₄F₆                   ↓        ↑        taper ↑    ↓         ↓        ↓ (top)
O₂                     ↑        ↓        taper ↓    ↑         ↑        ↑
CH₂F₂                  ↓        ≈ / ↑    taper ↑    ↓         N ↑      ↓ (bottom,
                                                                       via ρ)
NF₃ (flash)            ↑ (if    ↓        taper ↓    ↑         ↑        ≈
                       high)
Bias energy            ↑ (facet ↓        taper ↓    ↑         ↑        ≈
                       grows)
Tailored narrow IED    ↓        ↓        taper ↓    ↓         ↑        ↓
Pulsed (low duty,      ↓        ↓        taper ↓    ≈ / ↓     top ↓    ≈
 high peak)                                                   bottom ↑
Lower pressure         ↓        ≈        taper ↓    ≈         ≈        ↓
Lower wafer temp       ↓        ↑        taper ↑    ↓         ↓        ↓
Thicker / denser mask  ↓ (less  ≈        ≈          ↓         ≈        ≈
                       facet)
```

Only a few levers improve several columns at once: **narrow IEDs, high-peak pulsing, lower pressure, and better masks**. They are hardware and materials improvements. Gas-flow levers mostly move a problem from one column to another.

---

## 11.8 Holes, Slits, and Contacts

```
Feature          Profile emphasis
──────────────────────────────────────────────────────────────────────────────
Memory hole      Bow vs. web margin (adjacent holes); bottom CD for memory
                 films; joint CD for the next deck
Slit             Bottom width for nitride removal and metal fill; bow along a
                 long line; taper interacts with tilt at the wafer edge
Support hole     Must reach bottom through a stepped stack; taper less critical,
                 landing more
TAC              Wide; bow and taper smaller in angle; bottom must expose enough
                 metal for contact resistance
```

---

## 11.9 Summary & Key Takeaways

1. **A 0.1° taper costs 30 nm.** Over 8.4 µm, a wall that looks vertical narrows the reference hole from 105 to 75 nm.

2. **The bow sits at 1–3 µm.** Mask-facet reflection (z ≈ w/tan 2β) and wide-angle ions both put the most wall flux there.

3. **Bow margin is thin.** At 0.12 nm/min lateral rate, the bow reaches 114 nm against a 115 nm limit.

4. **Necks are worse than bows.** They restrict ions and neutrals for everything below and lead to clogging.

5. **The lower zone sets the bottom CD.** A 20% steeper lower taper takes 4 nm off; a 1 µm taller deck takes 6 nm off and fails.

6. **Clogging gives tails, not shifts.** Flash steps, less polymer at depth, and energy prevent it, each at a cost.

7. **Few levers help everything.** Narrow IEDs, pulsing, lower pressure, and better masks improve several profile metrics; gas changes trade them.

---

## Study Questions

1. A mask facet grows from 1.0° to 1.8° during the etch. Compute the bow depth at each for a 110 nm opening. Which part of the stack is affected as the facet grows?

2. With r_lat = 0.10 nm/min at z_bow = 2.5 µm, compute the bow using the reference timings. What lateral rate gives exactly 115 nm?

3. For the two-zone model, compute the zone-2 taper that gives CD_bottom = 72 nm with a 9.0 µm deck (zone 2 from 5.0 to 9.0 µm) and the reference zone 1.

4. A recipe change lowers zone-2 taper by 15% but raises r_lat at the bow by 20%. Compute the new CD_bottom and CD_max. Is the change acceptable?

5. Explain why clogging produces a bimodal depth distribution, and why the mean depth of a lot can look normal while landing yield falls.

---

**Previous Chapter:** [Chapter 10: Sidewall Striation, Scalloping & Layer-Selective Recess](./10-striation-scalloping-recess.md)  
**Next Chapter:** [Chapter 12: Charging, Twisting & Stress-Driven Distortion](./12-charging-twisting-distortion.md)

---

**Chapter 11 Development Status:** Complete  
**Version:** 1.0
