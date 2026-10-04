# Chapter 15: Endpoint, Layer-Resolved Metrology & Advanced Process Control

## Overview

The ON-stack etch is hard to watch. Its features are a few tens of nanometres wide and ten micrometres deep, their bottoms are invisible from above, and the signal they send into the plasma is small next to the mask and the feed gas. The stack's periodicity offers one obvious signal, a pair-frequency oscillation in optical emission, but that signal disappears within the first micrometre. This chapter explains why, and how to use it while it lasts. It sets out what landing endpoint can and cannot detect, reviews the metrology that measures depth, profile, modulation, and tilt, and builds the control loops (feed-forward from the stack and the mask, feedback on depth, CD and tilt, fault detection, and virtual metrology) that keep the process centred.

**Learning Objectives:**
- Estimate the product signal from feature bottoms relative to the mask and feed gas
- Derive the damping of the pair-frequency OES signal with depth from the front spread, and use the early signal as a rate monitor
- Interpret a landing endpoint transition and extract the arrival-time spread from its width
- Choose metrology for depth, bottom CD, profile, layer modulation, and tilt, and check its precision-to-tolerance ratio
- Compute feed-forward corrections from stack thickness, including the ARDE effect on the correction
- Set up EWMA feedback, fault detection, and virtual metrology for the stack etch

---

## 15.1 The Signal Budget

### 15.1.1 Where the Products Come From

```
Reference, at the bottom of the hole etch (A ≈ 93):

Stack removed at the feature bottoms:
  Bottom area ≈ 20% of the array cell × 65% array fraction ≈ 13% of the wafer
  13% × 707 cm² = 92 cm² at 153.7 nm/min
  Si atoms removed ≈ 7.0×10¹⁷ s⁻¹

Mask eroded (75% of the wafer covered, 45 nm/min, 9×10²² C atoms/cm³):
  C atoms removed ≈ 3.6×10¹⁸ s⁻¹

Feed gas: 300 sccm ≈ 1.3×10²⁰ molecules s⁻¹
```

The bottoms produce about one fifth as much as the mask. Their main product, SiF₄, is about 0.5% of the gas throughput. **Any endpoint signal from the bottoms is a fraction of a percent of the gas, on top of a mask signal several times larger.** Endpoint at high aspect ratio uses multivariate methods (principal component analysis of the full OES spectrum, ratios to actinometer lines) rather than a single emission line.

---

## 15.2 Layer Counting and Why It Fades

### 15.2.1 The Pair-Frequency Signal

Each pair changes the products from oxide-type (CO, O) to nitride-type (CN, N₂) and back (Chapter 3). With all fronts on the wafer in phase, the OES would oscillate at the pair frequency:

```
f_pair = R / p

Top of the etch: R = 312.5 nm/min = 5.2 nm/s, p = 50 nm → period 9.6 s
At 8 µm:         R ≈ 157 nm/min = 2.6 nm/s              → period 19 s
```

### 15.2.2 Damping by Front Spread

The fronts are not in phase. With a Gaussian spread σ_z of front depths across the wafer, the summed signal is the single-front signal convolved with that Gaussian. Its fundamental component is reduced by:

```
M(z) = exp(−2π² σ_z² / p²)

σ_z = 1.5% of depth (Chapter 3, Section 3.7), p = 50 nm:

Depth (µm)    σ_z (nm)    M
──────────────────────────────
 0.25           3.8       0.90
 0.50           7.5       0.64
 0.75          11.3       0.37
 1.00          15.0       0.17
 1.50          22.5       0.02
 2.00          30.0       0.001
```

**The pair-frequency signal falls to 1/e at about 750 nm (15 pairs) and is gone by 1.5 µm.** Layer counting works well in a staircase etch (Book #23), where each step etches only one or two pairs. It cannot count the hundreds of pairs of a HAR feature. It also cannot be rescued by better optics: the loss is in the physics of averaging over 10¹² out-of-phase fronts.

### 15.2.3 Using the Early Signal

During the first micrometre, the oscillation is strong. Its frequency gives the **instantaneous effective rate** on every wafer:

```
R_eff (top) = p · f_pair

Measured period 9.8 s instead of 9.6 s → R_eff = 50/9.8 = 5.10 nm/s = 306 nm/min (−2%)
```

This in-situ rate measurement feeds the APC model for that wafer: a wafer that starts 2% slow will need about 2% more time to land (Section 15.5). The oscillation's decay rate also gives σ_z, an in-situ measure of uniformity.

---

## 15.3 Landing Endpoint

### 15.3.1 The Transition

When the fronts reach the landing layer (doped poly-Si in the reference), stack products fall and silicon-etch products change. Because arrivals are spread in time, the signal changes gradually:

```
Signal fraction S(t) ≈ Φ[(t − t̄_land) / σ_t]        (Φ: normal CDF)

Width of the 10%–90% transition = 2.56 σ_t
```

### 15.3.2 What the Width Tells You

```
Reference random spread σ_t = 1.0% × 40.6 min = 0.41 min; systematic spread adds
  Combined σ_t ≈ 0.6 min (illustrative)
  10–90% width ≈ 1.5 min
```

A wider transition on one wafer means a larger arrival spread. That can come from non-uniform rate, from stack thickness variation, or from a population of slow (clogging) features. The transition width is a per-wafer uniformity indicator available without metrology.

### 15.3.3 Using Endpoint for Overetch

```
Strategy                         How                                Risk
──────────────────────────────────────────────────────────────────────────────────
Fixed time                       Main-etch time from model and      Absorbs no wafer-
                                 feed-forward; fixed OE             to-wafer variation
Endpoint + fixed OE              Detect the 50% point; add a        Late tail invisible
                                 fixed overetch                     to OES
Endpoint + width-scaled OE       OE = k × (10–90% width)            Needs a reliable
                                                                    width estimate
```

The tail of slow features that sets most of the overetch (Chapter 13, Section 13.2.2) is far below what OES can see: a 10⁻¹² fraction of features contributes nothing measurable to the signal. **Endpoint can centre the overetch, but the tail term must still be covered by design.**

---

## 15.4 Metrology

### 15.4.1 Methods

```
Quantity             Method                              Notes
────────────────────────────────────────────────────────────────────────────────────
Top CD               CD-SEM                              Routine; fast
Bottom CD / landing  High-voltage SEM (HV-SEM)            Images hole bottoms through
                                                         HAR features in some cases
                     Voltage-contrast (VC) e-beam        Landed vs. unlanded features
                     inspection                          on a grounded layer; samples
                                                         large areas
Depth, bow, taper    CD-SAXS (transmission small-angle   Non-destructive profile of
                     X-ray scattering)                   periodic arrays; average over
                                                         the beam spot
Layer modulation     CD-SAXS superlattice peaks at       Array-averaged amplitude
                     q_z = 2π/p
Tilt                 CD-SAXS rocking curve; overlay of   0.01°-class resolution on
                     top and bottom (HV-SEM)             arrays
Twist (hole-to-hole) Cross-section / plan-view TEM at    Destructive; few holes;
                     depth; HV-SEM bottom vs. top        statistics limited
Remaining mask       Cross-section; spectral             Edge sites critical
                     reflectometry on mask
Full profile         Cross-section SEM / TEM             Destructive; the reference for
                                                         all models
```

### 15.4.2 Precision-to-Tolerance

```
P/T = 6 σ_meas / (USL − LSL)          (target ≤ 0.2–0.3)

Bottom CD: spec 70–80 nm (10 nm window)
  HV-SEM σ_meas = 0.6 nm → P/T = 3.6 / 10 = 0.36  (marginal)
  CD-SAXS σ_meas = 0.3 nm → P/T = 0.18             (adequate)

Edge tilt: spec ±0.15° (0.30° window)
  SAXS rocking σ_meas = 0.01° → P/T = 0.2          (adequate)
```

Bottom-of-feature metrology is the weakest link. CD-SAXS is well suited to the ON stack because the arrays are periodic. Its weakness is that it averages over many features and cannot see the tail.

---

## 15.5 Feed-Forward Control

### 15.5.1 From Stack Thickness

The extra depth of a thicker stack is etched at the **bottom** rate, not the average rate:

```
Δt = ΔH / R(A_end)

Reference: ΔH = +1% = +84 nm, R(A_end) = 153.7 nm/min
  Δt = 84 / 153.7 = 0.55 min = +1.35% of 40.6 min
```

A naive correction (time ∝ thickness) would add only 1.0%. **Because of ARDE, a 1% thicker stack needs 1.35% more time.** The feed-forward model must use the bottom rate.

### 15.5.2 Other Feed-Forward Inputs

```
Input (measured upstream)       Adjusts                              Model
───────────────────────────────────────────────────────────────────────────────────
Stack thickness map             Main-etch / LS time; radial ESC      Δt = ΔH/R(A_end);
                                zones to match the profile           Ch. 13.4
Top CD after mask open          ARDE: wider holes etch faster;       ΔA/A = −ΔCD/CD
                                trim time
Mask thickness                  OE limit; erosion-sensitive steps    Remaining-mask
                                                                     model
Wafer bow                       Chucking sequence; He pressure;      Bow class table
                                edge setting
Nitride composition (monitor)   ρ ramp (CH₂F₂ in ME-3)               Rate-matching
                                                                     matrix (Ch. 4)
Early OES pair frequency        Remaining time for this wafer        R_eff = p·f
 (in-situ, Section 15.2.3)
Ring and electrode RF-hours     Edge tuning / ring lift              Wear curve (Ch. 9)
```

---

## 15.6 Feedback Control

### 15.6.1 EWMA

Post-etch measurements (depth from SAXS, bottom CD, tilt) update the model offset with an exponentially weighted moving average:

```
b_{k+1} = λ y_k + (1 − λ) b_k         (offset estimate)
u_{k+1} = (target − b_{k+1}) / G        (recipe setting)

Steady-state variance inflation for white noise: 1 + λ/(2 − λ)
  λ = 0.3 → 1.18 (18% more variance than the noise itself)
```

λ is chosen to track drifts such as ring wear and electrode thinning (time constants of hundreds of wafers) without chasing measurement noise.

### 15.6.2 Typical Loops

```
Loop               Measured              Actuator                  Update rate
───────────────────────────────────────────────────────────────────────────────
Depth / landing    VC landing, SAXS      Main-etch time            Per lot
                   depth
Bottom CD          SAXS, HV-SEM          ME-3 NF₃/energy trim      Per lot
Radial CD          CD-SEM top, SAXS      ESC zone setpoints        Per lot
Edge tilt          SAXS rocking at edge  Ring lift / edge RF       Per n lots and
                                                                   per RF-hour
                                                                   schedule
Mask remaining     Cross-section (sample) OE limit                 Weekly
```

---

## 15.7 Fault Detection and Virtual Metrology

### 15.7.1 FDC

```
Signal                         Fault it catches
───────────────────────────────────────────────────────────────────────────
Arc counts, RF V/I transients  Electrical breakdown at wafer, ESC, ring
He leak per zone               Chucking failure, wafer bow outliers, ESC wear
OES PCA scores per stage       Chemistry or wall-state change; MFC faults
Throttle valve position        Leaks, pumping drift
Endpoint transition width      Uniformity loss, clogging tail
Early pair-frequency           Rate shift on this wafer
ESC zone temperatures          Chiller faults; zone heater failure
```

### 15.7.2 Virtual Metrology

A virtual metrology (VM) model predicts depth, bottom CD, and tilt for every wafer from FDC signals and upstream data, trained against measured wafers. For the stack etch, the most predictive inputs are usually the stack thickness, the early pair-frequency rate, the endpoint transition, the edge-ring RF-hours, and the He leak. VM covers the wafers that are not measured and flags the ones that need measuring.

### 15.7.3 Wafers at Risk

```
If a fault is detected only by lot-end metrology:
  Lot of 25 wafers × chambers sharing the fault × lots before detection

With per-wafer FDC/VM:
  The faulty wafer is held; next wafer in that chamber is inhibited
```

At 45 minutes per wafer, a chamber processes about 32 wafers per day. A fault found one day late by sampled metrology puts about 32 wafers at risk per chamber. With hundreds of stack layers above, each is a very expensive wafer.

---

## 15.8 Summary & Key Takeaways

1. **The bottoms are a weak source.** About 0.5% of the gas throughput, against a mask signal five times larger. Endpoint needs multivariate OES.

2. **Layer counting fades in a micrometre.** M = exp(−2π²σ_z²/p²): 1/e at 750 nm, gone by 1.5 µm with 1.5% front spread.

3. **Use the early oscillation as a rate meter.** Its period gives R_eff for every wafer, and its decay gives σ_z.

4. **The landing transition width measures uniformity.** 10–90% width = 2.56σ_t, but the 10⁻¹² tail is invisible.

5. **Feed-forward must include ARDE.** A 1% thicker stack needs 1.35% more time because the extra depth is etched at the bottom rate.

6. **Bottom metrology is the weak link.** CD-SAXS gives adequate P/T on periodic arrays but averages; HV-SEM and VC sample features directly.

7. **FDC and VM limit wafers at risk.** Per-wafer prediction catches faults before a day's production is lost.

---

## Study Questions

1. With σ_z = 1.0% of depth and p = 40 nm, compute the depth at which M = 1/e. Would thinner pairs make layer counting easier or harder?

2. The early pair period is 10.1 s on a wafer, with p = 50 nm. Compute R_eff and the predicted main-etch time (scale the reference 40.6 min by the rate ratio). What other information would you want before trusting the correction?

3. A landing transition has a 10–90% width of 2.2 min, against a baseline of 1.5 min. Compute σ_t for both. What overetch increase does the new σ_t imply if OE scales with σ_t?

4. A stack is 1.8% thinner than reference. Compute the feed-forward time change using the bottom rate. Compare with the naive proportional correction.

5. An EWMA loop uses λ = 0.2. Compute the variance inflation factor. If ring wear causes a drift of 0.3 nm per lot in bottom CD, estimate the steady-state lag error of the EWMA (lag ≈ drift × (1 − λ)/λ).

---

**Previous Chapter:** [Chapter 14: Scaling to 300–1000 Layers](./14-scaling-multideck-nextgen.md)  
**Next Chapter:** [Chapter 16: Integration, Yield & Cost of Ownership](./16-integration-yield-coo.md)

---

**Chapter 15 Development Status:** Complete  
**Version:** 1.0
