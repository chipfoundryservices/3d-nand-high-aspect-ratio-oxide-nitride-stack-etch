# Chapter 9: Chamber Conditioning & Long-Recipe Stability

## Overview

A 45-minute recipe at 12–15 kW of bias wears the chamber in ways a short etch never does. The walls collect fluorocarbon polymer and give it back. The upper electrode and edge ring erode, which moves the gap and the edge sheath. Parts heat up during the recipe and change the radical balance. A chamber that is matched on Monday drifts by Friday. This chapter describes the chamber state that the ON-stack etch depends on, how it is reset between wafers and restored after maintenance, how consumables drift over radio-frequency (RF) hours, and how that drift appears on the wafer as depth, ρ, mask, and edge-tilt changes.

**Learning Objectives:**
- Describe how wall polymer acts as a source and sink of radicals and how it shifts the rate ratio
- Explain the first-wafer effect, waferless autoclean, and seasoning
- Model within-recipe wall drift with a time constant and estimate its effect on the early stages
- Compute edge-ring and electrode wear over RF hours and the resulting edge tilt
- Design a stability-monitoring plan with signals that predict wafer outcomes
- Estimate the yield cost of particles and polymer flakes for a HAR array

---

## 9.1 The Chamber as Part of the Chemistry

### 9.1.1 Walls, Electrode, and Rings

In a fluorocarbon CCP, every surface that sees the plasma either collects or releases chemistry:

```
Surface                     Material (typical)          Role in the chemistry
────────────────────────────────────────────────────────────────────────────────
Upper electrode /           Si or SiC                   Consumes F (forms SiF₄);
 showerhead                                             raises C/F in the gas
Edge (focus) ring           Si, SiC, quartz             Consumes F at the edge;
                                                        sets the edge sheath
Confinement rings           Quartz, SiC, Si             Wall area near the plasma
Chamber liner               Anodized Al, Y₂O₃-coated    Collects polymer; releases
                                                        it as temperature rises
Wafer itself                ON stack + a-C mask         Largest consumer of F;
                                                        releases O, N, H
```

### 9.1.2 Wall Polymer as a Buffer

A polymer-coated wall absorbs CF_x radicals when the gas is rich in them and releases fluorine-containing species when it is heated or bombarded. It acts like a capacitor in the chemistry. Changes in the feed gas reach the wafer filtered by the wall's response, and a change in wall temperature looks to the wafer like a change in the gas mixture.

```
Wall state                    Effect on the gas            Effect on the stack etch
───────────────────────────────────────────────────────────────────────────────────
Bare (just cleaned)           Absorbs CF_x; gas leaner in  Less polymer: ρ ↑, bow ↑,
                              polymer, richer in F         mask erosion ↑
Steady-state polymer          Balanced                     Reference
Thick polymer, heated         Releases F and CF_x          More F: rate ↑, mask ↓;
                                                           later flake risk
```

---

## 9.2 Resetting the Chamber Between Wafers

### 9.2.1 Waferless Autoclean (WAC)

After each wafer, a short O₂ plasma (with NF₃ if Si-containing deposits are present) removes the polymer deposited during the recipe. The chamber then starts every wafer from the same wall state.

```
Reference WAC: 60–90 s, O₂ 500 sccm (+ NF₃ 50 sccm), source only, no wafer
  Removes ~50–200 nm of wall polymer
  Leaves walls nearly bare → each wafer starts with a polymer-absorbing wall
```

### 9.2.2 Within-Recipe Wall Evolution

Starting from a clean wall, polymer builds toward a steady state with a time constant τ_w:

```
θ_w(t) = θ_ss · (1 − e^(−t/τ_w))

Illustrative τ_w = 4 min

  End of CAP  (t = 1 min):   θ_w = 22% of steady state
  End of ME-1 (t = 11 min):  θ_w = 94%
  ME-2 onwards:              ≈ steady state
```

The CAP and the first part of ME-1 run on a wall that is still absorbing polymer. Those steps see a leaner gas than the later ones. Because CAP and ME-1 set the top CD and the start of the bow (Chapter 11), **wall recovery after WAC matters most for the top of the feature.** Recipes often include a short pre-coat or seasoning step after WAC, which deposits a thin polymer on the walls before the wafer arrives, or tune CAP and ME-1 for the bare-wall condition.

### 9.2.3 The First-Wafer Effect

After an idle period, the chamber is cooler and the walls have relaxed. The first wafer of a lot sees a different wall temperature and polymer state than the tenth:

```
Illustrative first-wafer signature (after 2 h idle):
  Depth at fixed time:   −1.5%
  Top CD:                −1.5 nm
  Edge tilt:             +0.03°
  Recovers by wafer 3 with standard WAC
```

Fabs counter this with **conditioning (dummy) wafers** after idle, a warm-up plasma, or an APC correction for the first wafer of a lot (Chapter 15).

---

## 9.3 Consumable Wear Over RF Hours

### 9.3.1 The Upper Electrode

A silicon upper electrode is consumed by fluorine and sputtering:

```
Illustrative consumption: 2 µm per RF-hour at reference conditions
RF hours per wafer: 0.75 h (45 min)
Consumption per wafer: 1.5 µm

Electrode life to a 1.5 mm loss limit: 1500 / 2 = 750 RF-hours ≈ 1000 wafers
```

As the electrode thins, the gap grows and its surface roughens. Its showerhead holes also widen, which changes gas distribution. Rate typically falls by 0.5–1.5% over electrode life, and radial uniformity shifts.

### 9.3.2 The Edge Ring

The edge ring sits next to the wafer edge and sets the height of the sheath there. As it erodes, the sheath over the ring thins relative to the sheath over the wafer, the boundary bends, and ions at the wafer edge arrive tilted outward:

```
Illustrative ring wear: 0.5 µm per RF-hour → 0.375 µm per wafer

Tilt sensitivity (illustrative): 0.05° per 100 µm of ring height loss
After 1000 wafers: 375 µm lost → tilt change ≈ 0.19°

Bottom displacement at the reference depth:
  θ = 0.19° = 3.3 mrad → 8.4 µm × 3.3×10⁻³ = 28 nm
```

The tilt specification at 3 mm from the edge is 0.15° (Chapter 1), equivalent to 22 nm of bottom displacement. **An uncompensated ring exceeds the tilt specification in under 1000 wafers.**

### 9.3.3 Compensation

```
Method                              How it works
──────────────────────────────────────────────────────────────────────────────
Ring replacement (PM)               Restores geometry; costs downtime and parts
Ring lift                           Raises the ring mechanically by the measured
                                    wear; restores the sheath step
Edge RF / DC tuning                 Separate power or bias applied to the ring
                                    region to adjust sheath height electrically
Recipe edge offset (APC)            Small edge gas or temperature offsets to
                                    trim residual tilt
Thicker or more resistant rings     SiC or composite rings wear more slowly
                                    but change the edge chemistry
```

With ring lift or edge tuning, ring life is limited by the total erosion the actuator can compensate, by ring shape changes (rounding of the inner edge), and by particles. Lives of several thousand RF-hours are reported for compensated designs.

---

## 9.4 How Drift Shows Up on the Wafer

```
Drift source              Time scale         Main wafer effect
────────────────────────────────────────────────────────────────────────────────
Wall recovery after WAC   Minutes, each      Top CD; early-stage bow
                          wafer
First-wafer / idle        Per lot            Depth, top CD, tilt
Electrode thinning        Hundreds of        Rate −0.5–1.5%, radial
                          RF-hours           uniformity
Edge-ring erosion         Hundreds of        Edge tilt, edge depth and CD
                          RF-hours
Liner polymer build-up    Between wet cleans ρ, mask erosion; flakes
Chiller and ESC drift     Weeks              Wafer temperature: ρ, bow
RF generator / match      Months             Delivered power → rate,
 ageing                                      energy → profile
```

The edge ring and the wall state are the two largest contributors to ON-stack etch variation in most fabs. Both act most at the wafer edge.

---

## 9.5 Preventive Maintenance and Recovery

### 9.5.1 After a Wet Clean

A wet clean removes all wall deposits and often replaces consumables. The chamber is then far from its production state:

```
Recovery sequence (illustrative):
  1. Pump down, leak check, bake if required
  2. Chamber seasoning: 5–20 seasoning wafers or long waferless polymer
     deposition to build the wall state
  3. Blanket and stack monitor wafers: rate, ρ, uniformity
  4. Patterned qualification wafers: depth, CD, bow, tilt, mask
  5. Match to reference chamber; set APC offsets (Chapter 15)
  6. Release to production
Total: 8–24 h of chamber time
```

### 9.5.2 Choosing Clean Intervals

Longer intervals between wet cleans raise availability but increase the risk of particles and flakes and the size of the drift that APC must absorb. The optimum is set by the flake defect rate (Section 9.6) more than by drift.

---

## 9.6 Particles and Flakes

### 9.6.1 Why HAR Etch Is Sensitive

A particle that lands on the mask during the etch blocks every opening under it. In a dense hole array, one particle can block many holes:

```
Hole density: 45 holes per µm² (Chapter 1)

Particle diameter     Holes blocked (approx.)
───────────────────────────────────────────────
  100 nm               ~0–1
  300 nm               ~3
  1 µm                 ~35
  5 µm                 ~900
```

A blocked hole is not etched. It becomes a string with no channel, which is a bit failure, or, if many holes are blocked, a block failure. Slits are more sensitive: one particle on a slit leaves a bridge between two blocks, and both blocks fail (Chapter 16).

### 9.6.2 Sources During a Long Recipe

- **Wall polymer flakes** after many wafers between wet cleans
- **Electrode and ring debris** from erosion and arcing
- **Plasma-off transients** at step changes if the plasma is extinguished: particles trapped at the sheath edge fall onto the wafer (Chapter 7 recommends keeping the plasma on)
- **Backside and bevel** particles moved by chucking and dechucking

### 9.6.3 Defect Budget

```
Illustrative: 0.02 adders per cm² ≥ 0.3 µm during etch
  Wafer area 707 cm² → 14 adders per wafer
  Die area 0.7 cm² → 0.014 per die
  Fraction that land in the array and kill a block: ~50%
  Blocks lost per die ≈ 0.007, recoverable within a bad-block allowance

Particles ≥ 5 µm (rare flakes): 0.001 per cm² → 0.7 per wafer
  Each kills one or more die → ~0.1% die yield loss
```

Small particles cost blocks that redundancy can absorb. Large flakes cost die. Flake control, through clean intervals, liner temperature, and polymer adhesion, is the priority.

---

## 9.7 Stability Monitoring

```
Signal                          What it tells you                  Action limit example
────────────────────────────────────────────────────────────────────────────────────────
OES ratios (F/Ar, CF₂/Ar,       Wall state, gas chemistry          ±3% from baseline
 CO/Ar) in ME-2
RF V, I, phase at electrode     Delivered power, sheath voltage,   ±2% V_pp
                                arc events
Throttle valve position at      Flow/pumping drift, leaks          ±5% from baseline
 fixed pressure
He leak per zone                Chucking, wafer bow, ESC wear      Zone limit by bow class
ESC zone temperatures           Chiller/heater drift               ±0.5 K
RF-hours on ring and electrode  Consumable life, tilt compensation Lift schedule
Arc counts                      Electrical weak points             Any hard arc → hold
Particle monitors               Chamber cleanliness                Per-lot adders
```

Chapter 15 combines these into fault detection and classification (FDC) and virtual metrology.

---

## 9.8 Summary & Key Takeaways

1. **The chamber is part of the chemistry.** Walls, electrode, and rings absorb and release radicals. A bare wall makes the gas leaner in polymer.

2. **WAC resets the wall every wafer.** Wall polymer then rebuilds with a time constant of minutes, so the top of the feature sees a different chemistry from the bottom.

3. **Idle chambers drift.** First-wafer effects of about 1.5% depth and 1.5 nm top CD are typical and are handled with conditioning wafers or APC.

4. **Consumables move the edge.** About 0.375 µm of ring wear per wafer can push edge tilt past 0.15° within 1000 wafers without compensation.

5. **Drift concentrates at the wafer edge.** Ring wear and wall state are the largest variation sources.

6. **Particles block arrays; flakes kill die.** One 1 µm particle blocks about 35 holes; large flakes are the main yield risk from the chamber.

---

## Study Questions

1. With τ_w = 6 min, compute the wall coverage at the end of CAP (1 min) and ME-1 (11.4 min). How would you modify the recipe if top CD drifts with τ_w?

2. A ring wears at 0.6 µm per RF-hour and the recipe takes 45 min. With a tilt sensitivity of 0.04° per 100 µm, how many wafers until the tilt changes by 0.12°? How much ring lift is needed at that point?

3. An electrode consumes 2.5 µm per RF-hour with a 1.2 mm limit. How many wafers does it last? If rate falls 1.2% over its life, how much extra time is needed at end of life to reach the same depth?

4. Estimate how many holes a 2 µm particle blocks in the reference array. If such particles land at 0.003 per cm², how many blocked-hole events occur per wafer?

5. List three signals that would distinguish wall-state drift from RF delivery drift, and explain what each would show.

---

**Previous Chapter:** [Chapter 8: Wafer Temperature, Cryogenic Etch & Heat Flow](./08-temperature-cryogenic-etch.md)  
**Next Chapter:** [Chapter 10: Sidewall Striation, Scalloping & Layer-Selective Recess](./10-striation-scalloping-recess.md)

---

**Chapter 9 Development Status:** Complete  
**Version:** 1.0
