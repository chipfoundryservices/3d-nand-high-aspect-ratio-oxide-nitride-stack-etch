# Appendix G: Troubleshooting Guide

Symptom-driven guide for ON-stack etch excursions. For each symptom: likely causes ranked from most to least common, checks to tell them apart, and corrective actions. Chapter references point to the underlying physics.

---

## G.1 Unlanded Features (Depth Short)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Stack thicker than the feed-forward     Stack thickness map vs. model;      Correct FF model;
   assumed (Ch. 2, 15.5)                   unlanded region = thick region      use bottom rate
2. Rate low: electrode end of life, RF     Early OES pair-frequency rate;      Recalibrate RF;
   calibration, MFC drift (Ch. 9)          RF-hours; V_pp trend                PM; trim time
3. Clogging tail (bimodal depth)           VC: scattered unlanded features;    Flash steps; less
   (Ch. 11.5)                              depth histogram bimodal             C₄F₆ in ME-3/LS
4. Nitride rate dropped (new nitride       FTIR H content; ρ_stack on short    Restore film; ramp
   recipe/chamber) (Ch. 2.2, 4.3)          stacks                              CH₂F₂/O₂
5. Profiles adding (stack centre thick,    Compare stack and etch radial maps  Match ESC zones to
   etch centre slow) (Ch. 13.4)                                                stack profile
6. Top CD small (litho / mask open)        CD-SEM top CD; correlation of       Litho/mask-open
                                           depth with CD                       correction; FF
```

## G.2 Landing Recess Too Deep / Punch-Through

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Overetch too long for the actual        Endpoint transition time vs. model  Endpoint-based OE;
   arrival (stack thin, rate high)                                             FF on thickness
2. LS selectivity low (O₂/NF₃ high,        Blanket poly rate in LS; MFC        Restore LS
   C₄F₆ low)                               check                               chemistry
3. Co-etched wide features (Ch. 13.3)      Recess only in wide features        Layout rule; thicker
                                                                               stop; separate etch
4. Landing layer thin (deposition)         Landing thickness metrology         Restore thickness
```

## G.3 Bow Above Specification

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Mask facet grown (low mask selectivity; Remaining mask; facet angle; a-C    Lower ME-1 energy;
   new a-C lot) (Ch. 11.2)                 density                             a-C incoming check
2. Polymer thin: O₂ high, wafer hot        MFC; ESC zone temps; He leak        Recalibrate; check
   (Ch. 8.3)                                                                   chucking
3. Wall state: bare walls after clean or   OES F/Ar, CF₂/Ar trend; time since  Pre-coat; extend
   new parts (Ch. 9.2)                     PM                                  seasoning
4. Wide-angle ions: pressure high, IED     Throttle position; V_pp/waveform    Pressure cal;
   changed (Ch. 5.3, 6.2)                  logs                                waveform restore
5. Bias energy raised without mask         Recipe audit                        Rebalance
   compensation
```

## G.4 Bottom CD Too Small / Taper Too Large

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Excess polymer at depth (C₄F₆ high, O₂  Depth series: where does the taper  ME-3 NF₃/O₂ +;
   low, wafer cold) (Ch. 11.4)             steepen?                            energy +
2. ρ drift at depth (nitride slow)         Modulation increasing toward the    Raise ME-3 CH₂F₂
   (Ch. 3.6.3, 7.3)                        bottom; short-stack ρ in ME-3
3. Top CD small → higher A                 CD-SEM top CD                       FF; litho
4. Deck taller than reference              Stack thickness                     Time/FF; recipe
                                                                               for height
5. Neck restricting flux (Ch. 11.3)        Cross-section top 1 µm              Adjust ME-1
                                                                               polymer
```

## G.5 Layer Modulation (Wall Steps) Increased

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Post-etch clean more aggressive (DHF    Pre-clean vs. post-clean TEM        Restore clean;
   time/concentration) (Ch. 10.4)                                              gentler chemistry
2. Lateral-rate difference up (O₂/NF₃ at   TEM at bow depth; OES O/Ar           Restore flows;
   the bow depth) (Ch. 10.2)                                                   more ME-1 polymer
3. ρ mismatch at depth (modulation near    Modulation vs. depth profile; ρ     ME-3 ramp
   the bottom) (Ch. 10.3.1)                per stage
4. Stack interfaces changed (deposition    Interface TEM/EELS; deposition      Restore switching
   gas-switch timing) (Ch. 10.3.2)         recipe audit                        sequence
5. Film H/density changed                  FTIR; refractive index              Restore film
```

## G.6 Edge Tilt Out of Specification

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Ring wear beyond the compensation       Ring RF-hours vs. curve; tilt trend Update edge
   curve (Ch. 9.3)                         vs. RF-hours                        setting/lift;
                                                                               replace ring
2. Wafer edge not seated (bow, particle    He leak per zone; tilt correlated   Staged chucking;
   under the wafer) (Ch. 8.5, 12.3.2)      with incoming bow                   clean ESC; bow
                                                                               class handling
3. Saddle-shaped wafer (cos 2φ pattern)    Wafer shape; tilt vs. azimuth       Bow control before
   (Ch. 12.3.3)                                                                etch; chucking
                                                                               sequence
4. Edge APC sign or gain error             Offset history; tilt moving away    Fix sign; verify
                                           from target after corrections       with offset test
5. Wrong ring part or mis-seated ring      Part number; height gauge;          Reinstall; verify
   after PM                                cos φ pattern
```

## G.7 Twisting / Joint Misses Increased

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Pulsing or waveform changed (less       Generator logs; duty/frequency      Restore
   charge relief) (Ch. 6.3, 12.1.4)
2. Ion energy lower in ME-3                V_pp; delivered power               RF calibration
3. Deck taller (twist ∝ H^(3/2))           Stack thickness                     Accept/limit; FF
   (Ch. 12.2.2)
4. Array-edge twist (dummy rows            Location of misses                  Layout: dummy rows
   insufficient) (Ch. 13.3.4)
5. Deck-1 joint pad small or deck-2        CD-SEM of pad; overlay              Pad CD; overlay
   overlay drift (Ch. 7.5.2)                                                   correction
```

## G.8 Mask Exhausted at the Edge

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Overetch extended (APC or manual)       Recipe and APC history              Endpoint-based OE;
                                                                               fix stack FF
2. Edge erosion higher (ring wear, edge    Remaining mask edge/centre ratio    Edge tuning; ring
   temperature) (Ch. 13.1)                 vs. RF-hours
3. Mask thinner / softer (deposition lot)  Incoming a-C thickness, density     Incoming spec
4. ME-3 O₂/NF₃ increased to fix bottom CD  Recipe audit                        Rebalance with
   (Ch. 4.3.3)                                                                 energy/pulsing
```

## G.9 Arcing Events

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Backside He breakdown (He pressure,     Arc location on ESC; He pressure    He path/plug
   worn plugs) (Ch. 5.7)                   logs                                service; pressure
2. Bevel film or particles at the edge     Bevel inspection                    Bevel clean
3. Bias ramp too fast                      Generator logs at step changes      Ramp rates
4. ESC dielectric ageing                   Clamp current trend; arc history    Replace ESC
5. Defects in the stack (voids,            Arc craters correlated with         Deposition particle
   particles from deposition)              incoming defect maps                control
```

## G.10 Chamber-to-Chamber Mismatch

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. RF delivered power / V_pp calibration   Calibration at the electrode        Recalibrate
2. Consumables at different life           RF-hours of ring and electrode      Align PM schedules;
                                                                               per-chamber APC
3. ESC zone calibration                    Sensor-wafer map                    Recalibrate zones
4. Part-number or lot differences          Part records                        Standardize
5. MFC calibration                         Rate-of-rise test                   Recalibrate
```

## G.11 Pattern Follows the Deposition Tool

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Nitride composition (H, density)        FTIR, RI per deposition chamber     Restore film;
   differs between deposition chambers                                         per-source FF
2. Thickness profile differs               Thickness maps per deposition       Profile matching;
                                           chamber                             FF on thickness
3. Stress / bow differs                    Bow per deposition chamber          Backside
                                                                               compensation
4. Interface sharpness differs             TEM of interfaces                   Gas-switch timing
```

---

## G.12 First Checks for Any Excursion

```
1. Did anything change upstream? (stack deposition chamber, film recipe, mask
   lot, litho CD) → the stack is part of the etch (Ch. 2)
2. Does the symptom follow the etch chamber, the deposition chamber, or the lot?
3. Where on the wafer? (centre, ring, arcs, random) → Chapter 16, Section 16.4 signatures
4. Where in depth? (top, bow depth, bottom) → depth series (Appendix C.1)
5. When did it start relative to PM, RF-hours, or idle time? → Chapter 9
```

---

**Appendix G Version:** 1.0  
**Last Updated:** 2026-10-04
