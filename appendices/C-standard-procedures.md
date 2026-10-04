# Appendix C: Standard Operating Procedures

Representative procedures for developing, qualifying, and maintaining an ON-stack etch. They are templates. Adapt the limits, sample sizes, and tools to your own specifications and equipment.

---

## C.1 Depth-Series Profile Development

**Purpose:** See how the profile, the rate ratio, and the wall modulation evolve through the recipe, so each stage can be judged separately (Chapter 7, Section 7.3.3).

```
Prerequisites
  - Product or short-loop wafers with the full deck stack and a-C mask
  - Time-to-depth model for the current recipe (Chapter 3, Section 3.6.2)

Procedure
  1. Choose stop points at the end of each stage and one inside the longest
     stage (reference: end CAP, end ME-1, mid ME-2, end ME-2, end ME-3, full).
  2. Run one wafer per stop point in the same chamber, consecutively, with
     standard WAC between wafers.
  3. Keep the mask on half of each wafer (cleave or protect), and ash the
     other half.
  4. Cross-section at: centre; mid-radius; 3 mm from the edge (two
     orthogonal directions); one array-edge site.
  5. Measure at each site: depth; CD every 0.1 µm for the top 3 µm and every
     0.5 µm below; remaining mask and facet angle; layer modulation (TEM) at
     three depths; bottom shape (sag); top-to-bottom offset.
  6. Run CD-SAXS on the same wafers where arrays allow, for array-averaged
     profile and modulation.

Interpretation
  - Bow growing after ME-1 with facet growth → facet-driven; act on ME-1
    energy or mask (Chapter 11)
  - Modulation growing toward the bottom → ρ drift; adjust the ME-3 ramp
    (Chapters 3, 7)
  - Step marks at stop depths → transition problem (Chapter 7, Section 7.4)
  - Edge offset appearing only below a given depth → stage-dependent edge
    mismatch (Chapters 9, 12)
```

---

## C.2 Stack Rate and Rate-Ratio Measurement

**Purpose:** Measure R_ox, R_N, R_eff, and ρ as the stack actually experiences them, and the interface-transient correction (Chapter 3, Section 3.3).

```
Samples
  - Blanket PECVD oxide and nitride from the production deposition chamber
  - Short ON stacks (20–40 pairs) of the production thickness ratio
  - Optional: patterned short-loop arrays for A-dependent rates

Procedure
  1. Run each stage's condition for a fixed time on blanket oxide, blanket
     nitride, and the short stack, in the same chamber session.
  2. Measure removed thickness (ellipsometry for blankets; X-ray
     reflectometry or cross-section for stacks).
  3. Compute:
       R_eff,predicted = 1/(φ_ox/R_ox + φ_N/R_N) from the blanket rates
       R_eff,measured  from the stack
  4. Fit the transient: choose k_N, k_ox, τ_p that reproduce R_eff,measured
     and, if available, the per-layer times seen in the in-situ OES
     oscillation (Section C.7).
  5. Record ρ_blanket and ρ_stack per stage.

Acceptance
  - ρ_stack within the stage target (e.g., 0.85–1.05)
  - R_eff,measured within ±2% of the model
```

---

## C.3 Rate-Matching Matrix Calibration

**Purpose:** Build the local sensitivity matrix of Chapter 4 (Section 4.3.2) for the production recipe.

```
1. Choose knobs (C₄F₆, CH₂F₂, O₂, NF₃, bias power; optionally temperature).
2. For each knob, run ±10% of its reference value at the stage of interest,
   on blanket oxide, blanket nitride, and a-C mask wafers; 3 repeats each.
3. Fit ΔR/R per +10% for each material; check linearity with a ±20% point.
4. Validate: predict a two-knob change and confirm on a short stack.
5. Re-calibrate after any change of nitride deposition recipe, mask
   material, or chamber hardware.
```

---

## C.4 Chamber Seasoning After Wet Clean

```
1. Pump down; leak-up rate within limit; base pressure within limit.
2. Waferless polymer deposition (fluorocarbon plasma, 15–30 min) or
   10–20 seasoning wafers with the production recipe.
3. Monitor OES ratios (F/Ar, CF₂/Ar, CO/Ar) during each seasoning run;
   continue until three consecutive runs are within ±3% of baseline.
4. Blanket rate wafers (oxide, nitride, a-C) → R_ox, R_N, ρ, mask erosion.
5. One full-recipe patterned wafer → depth, CD, bow, edge offset.
6. Release, or extend seasoning.
```

---

## C.5 New-Chamber Qualification

```
1. Hardware checks
   - RF delivered-power calibration at the electrode (source and bias)
   - Bias waveform check (V_pp, IED estimate if available)
   - Electrode gap, edge-ring height, ring and electrode part numbers
   - ESC zone temperature calibration (sensor wafer; cryogenic if used)
   - He leak baseline per zone on flat and bowed reference wafers
   - MFC calibration (rate-of-rise); throttle valve position at reference flow
2. Seasoning (C.4)
3. Stack rates and ρ per stage (C.2)
4. Patterned monitors: 3 full-recipe wafers
   - Landing (VC inspection of full array regions); depth (SAXS)
   - Top CD, bow, bottom CD, modulation (SAXS + one cross-section)
   - Edge offset at 3 mm in two orthogonal directions
   - Remaining mask at centre and edge
5. Matching to the reference chamber (C.9)
6. Release with chamber-specific APC offsets
```

---

## C.6 Edge-Tilt Calibration and Ring Compensation Curve

**Purpose:** Measure edge tilt against ring wear and edge setting, to drive ring lift or edge tuning (Chapter 9, Section 9.3).

```
1. With a new ring, run full-recipe wafers at three edge settings
   (nominal, ±1 step).
2. Measure tilt (SAXS rocking or top/bottom offset) at 3 mm and 5 mm from
   the edge at four azimuths.
3. Repeat at ring life milestones (e.g., every 200 RF-hours).
4. Fit tilt = a·(ring wear) + b·(edge setting) + c.
5. Set the compensation: edge setting or ring lift as a function of RF-hours
   that keeps tilt within ±0.05° of target.
6. Check azimuthal residuals: a cos φ term means ring offset or wafer
   placement; a cos 2φ term means wafer shape (bow) effects.
```

---

## C.7 In-Situ Rate Measurement From the OES Pair Frequency

**Purpose:** Use the pair-frequency OES oscillation in the first micrometre as a per-wafer rate monitor (Chapter 15, Section 15.2.3).

```
1. Record CN (388 nm) and CO band emission at ≥ 10 Hz during CAP and ME-1.
2. Detrend each signal (subtract a moving average over ~30 s).
3. Compute the dominant period in the window from ~0.3 to ~0.8 µm of
   depth (≈ 1 to 3 min into the etch).
4. R_eff = p / period. Compare with the chamber baseline.
5. Estimate σ_z from the oscillation decay: fit M(z) = exp(−2π²σ_z²/p²)
   with σ_z = k·z.
6. Pass R_eff and k to APC and FDC.
```

---

## C.8 Wafer Bow Classification and Chucking

```
1. Measure bow (and shape: sphere vs. saddle) on every wafer before etch.
2. Assign bow class: A (< 100 µm), B (100–250 µm), C (250–400 µm),
   D (> 400 µm: hold).
3. Use the class to select the chucking sequence (staged voltage), He
   pressure ramp, and edge setting.
4. Log He leak per zone; flag wafers whose leak exceeds the class limit.
5. Review weekly: tilt and edge CD vs. bow class.
```

---

## C.9 Chamber Matching

```
Matching metrics (full recipe, 3 wafers per chamber):
  Depth at fixed time                  ±1.0%
  Top CD                               ±1.0 nm
  Bottom CD                            ±1.5 nm
  Bow (CD_max)                         ±1.5 nm
  Edge tilt                            ±0.03°
  Remaining mask                       ±50 nm
  ρ per stage (C.2)                    ±0.02

If out of match:
  1. Check RF delivered power and V_pp
  2. Check ring and electrode parts and RF-hours
  3. Check ESC zone calibrations and He leak
  4. Check MFC calibration
  5. Apply chamber offsets in APC only after hardware causes are excluded
```

---

## C.10 Mask Budget Verification

```
1. On a full-recipe wafer, cross-section at centre, mid-radius, and 3 mm
   from the edge.
2. Measure remaining a-C thickness and facet angle at each site.
3. Compute edge excess e_edge = (consumed_edge / consumed_centre) − 1.
4. Confirm remaining ≥ T_min (300 nm reference) at the edge with margin
   ≥ 50 nm. If not: reduce OE, change deep-step erosion, or change mask.
5. Repeat after any change of mask lot, mask deposition tool, or ME-3
   chemistry.
```

---

**Appendix C Version:** 1.0  
**Last Updated:** 2026-10-04
