# Index: Book #25 Navigation Guide

## Quick Navigation

**Total Content:** 16 chapters + 7 appendices + glossary  
**Estimated Read Time:** 22–30 hours for the complete book; 6–10 hours for a focused reading path

| Part | Chapters | Theme |
|------|----------|-------|
| I | 1–4 | Fundamentals: stack architecture, films, alternating-layer physics, rate-matching chemistry |
| II | 5–9 | Hardware & process design: reactor and RF, ion energy and waveforms, recipe architecture, temperature and cryo, chamber stability |
| III | 10–14 | Phenomena: striation and modulation, profile, charging and distortion, mask and landing, scaling to 1000 layers |
| IV | 15–16 | Production: endpoint, metrology, APC, integration, yield, cost |

---

## Part I: Fundamentals (Chapters 1–4)

### Chapter 1: [The ON Stack in 3D NAND — Why Every Critical Etch Goes Through Alternating Dielectrics](./chapters/01-on-stack-architecture.md)
**Estimated Time:** 60 min | **Difficulty:** Foundation | **Reading Level:** All roles  
**Focus:** What is the stack, which features are cut through it, and what must they deliver?

**Key Topics:**
- Replacement-gate flow; what oxide and nitride layers become
- Holes, slits, support holes, and through-array contacts
- Stack height by generation; why height, not width, drives scaling
- Etch time and the per-deck limit
- Generic specification sheet and the items the stack controls

**Prerequisites:** None (foundational)  
**Cross-References:** Book #23 (Staircase Etch); Book #24 (Memory Hole Etch); slit-etch companion  
**Critical Equations:** H_deck = N·p + h_overhead; A = H/w̄; t = (w̄/R₀)(A + A²/2A₀)  
**Study Questions:** 5 calculations on height, etch time, density, and yield

---

### Chapter 2: [Stack Films — PECVD Oxide & Nitride, Thickness Ratio & Stress](./chapters/02-stack-film-properties.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Thin-film/Integration roles  
**Focus:** How do deposition choices set the etch?

**Key Topics:**
- PECVD oxide and nitride; density, hydrogen, stoichiometry
- Atom and Si density; why nitride needs more work per nanometre
- Thickness ratio and effective rate; systematic vs. random height variation
- Stack stress, Stoney bow, stress-balanced stacks
- Non-periodic layers; monitoring the stack for the etch

**Prerequisites:** Chapter 1  
**Cross-References:** Silicon Nitride Etch companion; Books #6–10  
**Critical Equations:** σ_stack = φ_ox σ_ox + φ_N σ_N; κ = 6σt_f/(M t_s²); σ_N,balance = −φ_ox σ_ox/φ_N  
**Data Tables:** Film properties (Appendix A)  
**Study Questions:** 5 calculations on density, stress, bow, landing time, and composition sensitivity

---

### Chapter 3: [Etching Alternating Layers — Effective Rate, Rate Alternation & Interface Physics](./chapters/03-alternating-layer-etch-physics.md)
**Estimated Time:** 90 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** What does it mean to etch a material that changes every 25 nm?

**Key Topics:**
- Series model and harmonic-mean effective rate; sensitivity = time fraction
- Front speed oscillation at top and bottom
- Polymer interface transients; stack vs. blanket rates
- Curved front spanning both films
- Ion acceptance and Monte Carlo neutral transmission for holes and slots
- ARDE of a layered material; ρ drift with depth

**Prerequisites:** Chapters 1–2; plasma physics (Books #1–5)  
**Critical Equations:** R_eff = 1/(φ_ox/R_ox + φ_N/R_N); z = R_ss t + (k−1)τ_p R_ss; W_slot ≈ (ln A + 0.1)/A; ρ(A)  
**Study Questions:** 5 calculations on effective rate, transients, slots, ρ drift, and phase spread

---

### Chapter 4: [ON Etch Chemistry — Fluorocarbons, Hydrogen & Rate Matching](./chapters/04-on-etch-chemistry.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** How is the gas mixture used to make oxide and nitride etch alike?

**Key Topics:**
- Oxide and nitride mechanisms; the roles of O, N, and H
- Knob table and linear rate-matching matrix
- Worked recovery from a nitride film change
- Mask selectivity through the etch; landing selectivity
- Cryogenic HF chemistry; ammonium fluorosilicate; OPOP stacks

**Prerequisites:** Chapter 3; fluorocarbon etch (Books #6–10)  
**Critical Equations:** Linear matrix ΔR = M·Δu; S(z) = R(A)/r_m; θ = Kp/(1+Kp), K ∝ exp(E_ads/kT)  
**Study Questions:** 5 calculations on rate matching, selectivity, adsorption, and landing

---

## Part II: Hardware & Process Design (Chapters 5–9)

### Chapter 5: [Reactor & RF Systems for Extreme-Aspect-Ratio Dielectric Etch](./chapters/05-reactor-rf-systems.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment roles  
**Focus:** What reactor delivers multi-keV ions with independent chemistry?

**Key Topics:** CCP vs. ICP; frequency stack; kV sheath thickness and collisions; ion transit time; bias power split; VHF standing waves; residence time; arcing; platforms  
**Prerequisites:** Chapters 3–4  
**Critical Equations:** s = (√2/3)λ_D(2V/T_e)^(3/4); τ_i ≈ 3s/v; I_i = P_i/E_i; V(r)/V(0) ≈ J₀(kr); τ = pV/Q  
**Study Questions:** 5 calculations on sheath, transit time, power, uniformity, residence time

---

### Chapter 6: [Ion Energy, Angular Spread & Bias Waveform Engineering](./chapters/06-ion-energy-waveforms.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Equipment roles  
**Focus:** How much energy does a feature need, and how should it be delivered?

**Key Topics:** E_req ∝ A² for holes and slots; T_⊥; arcsine IED; tailored waveforms; high-peak pulsed bias; energy costs; ramping energy with depth  
**Prerequisites:** Chapters 3, 5  
**Critical Equations:** E_req = 2T_⊥A² ln[1/(1−f)]; E_req,slot = 2T_⊥A²[erf⁻¹ f]²; F(E) = ½ + (1/π)arcsin[(E−V̄)/V₁]  
**Study Questions:** 5 calculations on energy, IED, pulsing, slots, and ramps

---

### Chapter 7: [Recipe Architecture — Steps, Ramps & Deck Transitions](./chapters/07-recipe-architecture.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process roles  
**Focus:** Why is the recipe staged, and how is it built?

**Key Topics:** Stage functions; reference recipe and stage times; mask budget by stage; chemistry ramps for ρ; transitions and step marks; cap, IDL, and deck joint; sensitivities; holes vs. slits vs. contacts  
**Prerequisites:** Chapters 3, 4, 6  
**Critical Equations:** Stage times from t(A); joint RSS budget; Δdepth from 1% drifts  
**Study Questions:** 5 calculations on stage times, mask, joint budget, transitions, and edge landing

---

### Chapter 8: [Wafer Temperature, Cryogenic Etch & Heat Flow](./chapters/08-temperature-cryogenic-etch.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** What sets the wafer temperature, and how cold can the etch run?

**Key Topics:** Heat load; thermal path dominated by backside He; time constant; temperature sensitivities; cryogenic window and ±1 K requirement; cryogenic hardware; chucking bowed wafers  
**Prerequisites:** Chapters 4, 5  
**Critical Equations:** ΔT = q/h; τ = ρct/h; d ln K/dT = −E_ads/kT²; q = δ·64D(1+ν)/[a⁴(5+ν)]; P(g) = ε₀V²/[2(g + d/ε_r)²]  
**Study Questions:** 5 calculations on temperature, uniformity, adsorption, chucking, and throughput

---

### Chapter 9: [Chamber Conditioning & Long-Recipe Stability](./chapters/09-chamber-conditioning-stability.md)
**Estimated Time:** 60 min | **Difficulty:** Intermediate | **Reading Level:** Equipment roles  
**Focus:** How does the chamber drift, and how is it held steady?

**Key Topics:** Wall polymer as a buffer; WAC; within-recipe wall recovery; first-wafer effect; electrode and ring wear; tilt compensation; PM recovery; particles and flakes; stability signals  
**Prerequisites:** Chapters 5, 7  
**Critical Equations:** θ_w = θ_ss(1 − e^(−t/τ_w)); tilt = sensitivity × ring wear; displacement = H·θ  
**Study Questions:** 5 calculations on wall recovery, ring life, electrode life, particles, diagnostics

---

## Part III: Process Phenomena (Chapters 10–14)

### Chapter 10: [Sidewall Striation, Scalloping & Layer-Selective Recess](./chapters/10-striation-scalloping-recess.md)
**Estimated Time:** 70 min | **Difficulty:** Advanced | **Reading Level:** Process/Device roles  
**Focus:** How does the stack write itself onto the wall?

**Key Topics:** Layer modulation vs. vertical striation; exposure-time model; bow-depth peak; front-shape and interface terms; DHF clean amplification; cell V_t cost; levers; intentional recess; measurement  
**Prerequisites:** Chapters 3, 4, 7  
**Critical Equations:** δ(z) = Δr_lat·t_exp(z); ledge ≈ g·d·(1−ρ); q_z = 2π/p  
**Study Questions:** 5 calculations on modulation, ledges, clean, V_t, and SAXS interpretation

---

### Chapter 11: [Profile Control — Bow, Necking, Taper & Bottom CD](./chapters/11-profile-bow-taper.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process roles  
**Focus:** What shapes the feature from top to bottom?

**Key Topics:** Profile anatomy; bow depth from facet reflection and wide-angle ions; bow growth; necking; two-zone taper and bottom CD; closure depth; clogging; lever map  
**Prerequisites:** Chapters 3, 6, 7, 10  
**Critical Equations:** z_bow ≈ w/tan 2β; ΔCD_bow = 2r_lat t_exp; CD_bottom = CD_top − 2Σα_i Δz_i  
**Study Questions:** 5 calculations on bow depth, bow size, taper, trade-offs, clogging

---

### Chapter 12: [Charging, Twisting & Stress-Driven Distortion](./chapters/12-charging-twisting-distortion.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration/Research roles  
**Focus:** What moves the bottom of the feature away from its target?

**Key Topics:** Differential charging; deflection by lateral fields; layered-wall permittivity; twist as a random walk (∝ H^(3/2)); edge-sheath tilt; chucking-induced tilt; in-plane distortion; slit relaxation; placement budget  
**Prerequisites:** Chapters 6, 8, 9  
**Critical Equations:** δθ ≈ ΔV/(2V_i); σ_x ≈ σ_δθ ℓ N^(3/2)/√3; displacement = H·θ; u ≈ (t_s/2)·slope  
**Study Questions:** 5 calculations on deflection, twist, tilt, bow slope, and placement budget

---

### Chapter 13: [Mask Selectivity, Landing & Loading Between Features](./chapters/13-mask-landing-loading.md)
**Estimated Time:** 70 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** Will the mask last and will every feature land?

**Key Topics:** Mask budget with edge excess; mask–AR feedback; mask options; overetch for 10¹² features; recess and required selectivity; co-etched widths; staircase support holes; macroloading; array-edge loading; matching deposition and etch profiles  
**Prerequisites:** Chapters 4, 7, 11  
**Critical Equations:** T_mask ≥ Σr_m t (1 + e) + T_min; OE = systematic + 7σ; Recess = t_OE R_b/S; t_land ∝ H(r)/R(r)  
**Study Questions:** 5 calculations on mask, overetch, selectivity, co-etching, and profiles

---

### Chapter 14: [Scaling to 300–1000 Layers — Decks, Thinner Pairs & Next-Generation Etch](./chapters/14-scaling-multideck-nextgen.md)
**Estimated Time:** 70 min | **Difficulty:** Advanced | **Reading Level:** All roles  
**Focus:** How tall can a deck be, and how many decks does the future need?

**Key Topics:** Stack height to 1000 layers; four per-deck limits and the design space; deck count vs. etch time and cost; thinner pairs; cryogenic HF, high-energy pulsing, masks, engineered stacks; roadmap  
**Prerequisites:** Chapters 6, 11, 12, 13  
**Critical Equations:** H_max per constraint; deck-count time comparison; twist H_max ∝ (1/σ_δθ)^(2/3)  
**Study Questions:** 5 calculations on limits, masks, deck count, cryogenic time, thinner pairs

---

## Part IV: Production Scale (Chapters 15–16)

### Chapter 15: [Endpoint, Layer-Resolved Metrology & Advanced Process Control](./chapters/15-endpoint-metrology-apc.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** All roles  
**Focus:** How do you see and control an etch you cannot look into?

**Key Topics:** Product signal budget; pair-frequency OES and its damping; early-rate monitoring; landing transition width; metrology methods and P/T; feed-forward with ARDE; EWMA feedback; FDC; virtual metrology; wafers at risk  
**Prerequisites:** Chapters 3, 9, 13  
**Critical Equations:** M = exp(−2π²σ_z²/p²); R_eff = p·f; width = 2.56σ_t; Δt = ΔH/R(A_end); 1 + λ/(2−λ)  
**Study Questions:** 5 calculations on damping, rate, transition width, feed-forward, EWMA

---

### Chapter 16: [Integration, Yield & Cost of Ownership](./chapters/16-integration-yield-coo.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** All roles  
**Focus:** What does the etch hand downstream, and what does it cost?

**Key Topics:** Downstream needs per feature; failure modes and redundancy; Poisson die yield; edge loss; wafer-map signatures; cost per chamber-minute; cost per wafer; chamber count; value of faster etch; overetch and ring-life trade-offs; handoff specification  
**Prerequisites:** All earlier chapters  
**Critical Equations:** Y = exp(−ΣN p u); $/min = capex/(yr·min·uptime) + consumables; chambers = WSPM·min/(60·730·uptime)  
**Study Questions:** 5 calculations on yield, chamber count, cost, PM economics, signatures

---

## Back Matter

- [Glossary](./GLOSSARY.md)
- [Appendix A: Stack Film, Mask & Gas Properties](./appendices/A-stack-film-properties.md)
- [Appendix B: Chemistry & Reaction Data](./appendices/B-chemistry-reaction-data.md)
- [Appendix C: Standard Operating Procedures](./appendices/C-standard-procedures.md)
- [Appendix D: Process Windows & Lookup Tables](./appendices/D-process-windows.md)
- [Appendix E: Stack-Etch Calculations](./appendices/E-stack-etch-calculations.md)
- [Appendix F: Endpoint & Metrology Reference](./appendices/F-endpoint-metrology-reference.md)
- [Appendix G: Troubleshooting Guide](./appendices/G-troubleshooting-guide.md)

---

## Reading Paths by Role

**Process Engineers (≈ 10 h):** Ch. 3, 4, 6, 7, 10, 11, 13 → Appendices B, D, G  
**Equipment Engineers (≈ 8 h):** Ch. 5, 6, 8, 9, 15 → Appendices C, F, G  
**Thin-Film & Integration Engineers (≈ 8 h):** Ch. 1, 2, 3, 13, 14, 16 → Appendices A, E  
**Device Engineers (≈ 5 h):** Ch. 1, 10, 12, 16  
**Researchers (≈ 8 h):** Ch. 3, 4, 8, 12, 14 → Appendices B, E

---

## Study Problem Themes

- Compute the effective rate and its sensitivity to each film (Ch. 2, 3)
- Correct a film change with the rate-matching matrix (Ch. 4)
- Integrate ARDE into stage times and a mask budget (Ch. 3, 7, 13)
- Compute required energy and the effect of IED shape and pulsing (Ch. 6)
- Estimate wafer temperature, cryogenic tolerance, and chucking limits (Ch. 8)
- Model layer modulation, bow, and bottom CD versus depth (Ch. 10, 11)
- Build twist, tilt, and joint budgets (Ch. 7, 12)
- Find the per-deck limit and choose a deck count (Ch. 14)
- Use OES damping and feed-forward with ARDE (Ch. 15)
- Combine failure modes into die yield and a cost per wafer (Ch. 16)

---

## How to Use This Index

1. **First time?** Read PREFACE.md, then this INDEX, then Chapter 1.
2. **Focused reading?** Pick your role from the reading paths above.
3. **Reference mode?** Jump to the chapter. Use Appendix G for symptoms and Appendix D for lookup tables.
4. **Deep dive?** Read Chapters 1–16 in order and work the study questions.

---

**Index Version:** 1.0  
**Last Updated:** 2026-10-04  
**Next:** Begin [Chapter 1: The ON Stack in 3D NAND](./chapters/01-on-stack-architecture.md)
