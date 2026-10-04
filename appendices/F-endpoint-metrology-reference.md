# Appendix F: Endpoint & Metrology Reference

Reference tables for in-situ sensing, endpoint, and metrology of ON-stack etch. Capabilities are representative; check the actual performance of your tools against your specifications with the precision-to-tolerance method in F.5.

---

## F.1 In-Situ Sensors

```
Sensor                        Measures                              Use in ON-stack etch
────────────────────────────────────────────────────────────────────────────────────────────
OES (full spectrum,           Emission of radicals and products     Pair-frequency rate (first µm);
 200–900 nm, ≥ 10 Hz)                                               landing transition; chamber
                                                                    state (PCA); FDC
RF V/I probes at electrode    V_pp, I, phase, harmonics             Delivered power; sheath voltage;
                                                                    arc detection
Arc detectors                 Fast V/I transients, reflected        Arc events; wafer hold
                              power spikes
Pressure / throttle position  Chamber pressure, valve angle         Leaks, flow drift
He flow / leak per zone       Backside He flow at set pressure      Chucking quality; bow class
ESC zone thermocouples / RTDs Chuck surface temperature             Thermal drift; zone faults
Wafer temperature             Sensor wafers (offline), or           Calibration; cryogenic
                              fluorescence / phosphor probes        control
Self-excited electron         Electron density, collision rate      Chamber state, wall
 resonance (SEERS) / probes                                         conditioning
```

---

## F.2 OES Endpoint Signals

```
Event                         Signal change (reference chemistry)              Notes
────────────────────────────────────────────────────────────────────────────────────────────
Pair crossings (first µm)     CN 388 / N₂ 337 vs. CO bands oscillate at        Damps to 1/e at
                              period p/R_eff (≈ 9.6 s at the top)              ≈ 750 nm depth
Cap → stack                   CN appears; CO falls slightly                    Confirms CAP time
IDL crossing (deck 2)         CN drops for the IDL duration                    Weak; wafer-averaged
Landing on poly-Si            CO, CN fall; SiF/F change; small                 Multivariate; 10–90%
                              (<1% of gas)                                     width = 2.56 σ_t
Landing on W (TAC)            CO, CN fall; W lines weak                        Very small open area
Mask breakthrough at edge     CO from a-C falls; underlying cap oxide          Indicates mask
 (fault)                      signal rises at edge sites                       exhaustion
```

---

## F.3 Endpoint Algorithms

```
Algorithm                     Description                               Use
────────────────────────────────────────────────────────────────────────────────────
Single-ratio threshold        Ratio of a product line to Ar              Low-AR features only
PCA / multivariate            Project the spectrum on components         HAR landing
                              trained on landing transitions
Derivative / slope            Detect the inflection of a smoothed        Transition centre
                              PCA score
Width estimate                Time between 10% and 90% of the            σ_t per wafer
                              transition
Frequency tracking            Detrended CN/CO signal; dominant period    Early rate per wafer
                              in the first µm                            (Appendix C.7)
```

---

## F.4 Metrology Methods

```
Method                       Quantities                       Resolution /           Limits
                                                              precision (illustr.)
──────────────────────────────────────────────────────────────────────────────────────────────
CD-SEM (top-down)            Top CD, opening shape,           σ ≈ 0.3–0.5 nm         Top only
                             LER/LWR
HV-SEM (high voltage)        Bottom CD, top/bottom offset,    σ ≈ 0.5–1 nm           Depth- and
                             unlanded features in some cases                         material-dependent
Voltage-contrast e-beam      Landed vs. unlanded features     Single-feature         Needs a grounded
 inspection                  over large areas                 detection              landing; throughput
CD-SAXS (transmission)       Depth, CD(z), bow, taper,        Depth σ ≈ 5–10 nm;     Periodic arrays;
                             modulation, tilt                 CD σ ≈ 0.3 nm;         array average;
                                                              tilt σ ≈ 0.01°         throughput
Optical CD (scatterometry)   Top/mid CD, mask thickness;      Model-dependent        Weak at depth
                             depth at moderate AR
X-ray reflectometry (XRR)    Stack layer thicknesses          ~0.1 nm per layer      Blanket stacks /
                                                              (model)                pads
Spectral reflectometry       Total stack and mask thickness   ~0.1–0.5%              Multilayer model
FTIR                         Nitride Si–H, N–H content        ~0.5 at%               Monitor wafers
Wafer shape (interferometry) Bow, warp, local slope, IPD      µm bow; nm IPD         —
Cross-section SEM / TEM      Full profile, modulation,        nm-scale               Destructive; few
                             interfaces, joint                                       features
```

---

## F.5 Precision-to-Tolerance Worksheet

```
P/T = 6 σ_meas / (USL − LSL)      Target ≤ 0.2 (good), ≤ 0.3 (acceptable)

Quantity        Spec window     Method       σ_meas     P/T
──────────────────────────────────────────────────────────────
Top CD          6 nm (±3)       CD-SEM       0.3 nm     0.30
Bottom CD       10 nm           CD-SAXS      0.3 nm     0.18
Bottom CD       10 nm           HV-SEM       0.6 nm     0.36
Bow (CD_max)    10 nm           CD-SAXS      0.4 nm     0.24
Edge tilt       0.30°           SAXS rocking 0.01°      0.20
Depth           300 nm          CD-SAXS      8 nm       0.16
Modulation      2 nm (0–2)      TEM          0.2 nm     0.60  (use for
                                                               engineering only)
```

---

## F.6 Sampling Plan (Illustrative)

```
Measurement                       Frequency                          Sites
────────────────────────────────────────────────────────────────────────────────────
Top CD (CD-SEM)                   Every lot, 2 wafers                 13 sites
CD-SAXS profile and depth         Every lot, 1 wafer                  9 sites incl. 2 edge
SAXS tilt (rocking)               Daily per chamber                   8 edge sites (4
                                                                      azimuths × 2 radii)
VC landing inspection             Every lot, 1 wafer; full wafer      Array regions
                                  weekly per chamber
Remaining mask (cross-section)    Weekly per chamber                  Centre, mid, edge
Modulation (TEM)                  Monthly; after recipe or stack      3 depths, 2 radii
                                  changes
Wafer bow                         Every wafer, before and after etch  Full map
Stack thickness map               Every wafer (or every lot)          Full map
Nitride FTIR                      Daily deposition monitor            —
```

---

## F.7 APC Parameters (Illustrative)

```
Loop                 Model                                    λ (EWMA)   Limits
──────────────────────────────────────────────────────────────────────────────────────
Main-etch time       Δt = ΔH/R(A_end) + offset                0.3        ±5% of t
Early-rate trim      t_rem scaled by R_ref / R_meas           —          ±3%
Bottom CD            ME-3 NF₃ / energy trim                   0.2        ±10% of setting
Radial CD            ESC zone offsets                         0.3        ±3 K per zone
Edge tilt            Ring lift / edge RF vs. RF-hours + FB    0.2        Actuator range
Bow class            Chucking sequence lookup                 —          Class D → hold

EWMA variance inflation: 1 + λ/(2 − λ)
  λ = 0.2 → 1.11;  λ = 0.3 → 1.18
```

---

**Appendix F Version:** 1.0  
**Last Updated:** 2026-10-04
