# Preface: Etching a Material That Changes Every 25 Nanometres

## Why This Book Exists

Most etch processes see one material at the front. The oxide/nitride stack etch sees two, and they alternate every 22–28 nm for 8 µm, then start again in the next deck. A 3D NAND wafer with 300 word lines carries more than 600 dielectric layers. Every memory hole, every slit, every support hole in the staircase, and every contact through the array has to cross all of them. Each crossing must keep the feature straight and keep its width, and each feature has to reach the bottom at the same moment as billions of others.

Earlier books in this series treat the features that are cut through the stack: the memory hole (Book #24), the slit, and the staircase (Book #23). Each of them meets the same questions about the stack. Why does the sidewall have ridges at every interface? Why does the etch rate depend on the nitride deposition recipe? Why does changing the thickness ratio move the endpoint? Why does the wafer bow change the edge tilt? How many layers can one deck hold? This book answers those questions once, from the stack's point of view.

The stack asks a great deal of the etch:

1. **Two materials, one rate.** The time to etch one pair is d_ox/R_ox + d_N/R_N. The effective rate is a thickness-weighted *harmonic* mean, 312.5 nm/min in the reference process. The slower material dominates.

2. **Ions must be nearly vertical.** At A = 93 the acceptance half-angle is 10.8 mrad. With 5 keV ions and 0.5 eV transverse temperature, σ_θ = 10 mrad and only 44% of the ions reach the bottom without striking the wall.

3. **Depth costs more than linearly.** With R = R₀/(1 + A/A₀), the reference hole needs 40.6 minutes per deck. A single deck of twice the height would need 2.7 times as long.

4. **The wall remembers every interface.** The top layers see plasma for the whole 40 minutes. A lateral-rate difference of only 0.05 nm/min between oxide and nitride leaves a 2 nm step at every interface near the top.

5. **The stack bends the wafer.** A net stack stress of −32 MPa across 17 µm of film bows a 300 mm wafer by more than 300 µm. That bow sets chucking, backside cooling, and edge tilt.

6. **Layer signals disappear.** The pair period is visible in optical emission only while the etch fronts across the wafer agree to within a fraction of a pair. With 1.5% front spread, the signal falls to 1/e after 750 nm, about 15 pairs.

This book treats ON-stack etch as **a materials-and-transport problem in a periodic medium**, not as a deep oxide etch with some nitride in it.

---

## Unique Aspects of ON-Stack Etch

### 1. The Material Is Designed for the Device, Not the Etch

The nitride thickness is set by the word-line metal it will become. The oxide thickness is set by the word-line-to-word-line breakdown and coupling. Deposition is optimized for throughput, uniformity, and stress. The etch has to accept a material it did not choose, so the etch engineer must understand how deposition choices change the rate.

### 2. A Periodic Front

The etch front crosses an interface every 4–12 seconds. The polymer on the front, the surface chemistry, and the products leaving the feature all oscillate at that period. Most of the time the front is curved enough to span both materials at once, and the etch acts on the average.

### 3. One Stack, Many Features

The same stack is etched as round holes, long slits, large contacts, and sparse support holes. Each has its own aspect ratio and ARDE constant, and they meet the same landing layers. A recipe that is matched for one feature is mismatched for another.

### 4. Stress Is a Process Variable

The stack is the largest stressed film on the wafer. Its bow changes with every deck and every etch, and the etch changes it again by cutting the stack. The chuck, the edge sheath, and the overlay of later layers all feel it.

### 5. Scaling Is Vertical

Planar scaling shrinks features. 3D NAND scaling adds layers. Each generation makes the stack taller, the pairs thinner, and the etch longer. The etch, more than lithography, now sets the cost of each additional layer.

---

## Why This Book Is Organized This Way

Book #25 follows the same four-part structure as Books #19–24:

**Part I: Fundamentals (Chapters 1–4)**
- The architecture of the stack and its features, the films, the physics of etching alternating layers, and the chemistry of rate matching

**Part II: Hardware & Process Design (Chapters 5–9)**
- The reactor and RF systems, ion energy and waveforms, recipe architecture, wafer temperature and cryogenic etch, and chamber stability

**Part III: Phenomena (Chapters 10–14)**
- Striation and scalloping, profile, charging and distortion, mask and landing across features, and scaling to 1000 layers

**Part IV: Production (Chapters 15–16)**
- Endpoint, metrology, and control; integration, yield, and cost of ownership

### Reading Paths

**Process Engineers:** Chapters 3, 4, 6, 7, 10, 11, 13  
→ Layer physics, chemistry, energy, recipe, striation, profile, landing

**Equipment Engineers:** Chapters 5, 6, 8, 9, 15  
→ Reactor, waveforms, temperature, conditioning, monitoring

**Thin-Film & Integration Engineers:** Chapters 1, 2, 3, 13, 14, 16  
→ Stack design, films, effective rate, landing, decks, yield

**Device Engineers:** Chapters 1, 10, 12, 16  
→ How wall shape and distortion become cell variation and failures

**Researchers:** Chapters 3, 4, 8, 12, 14  
→ Interface transients, chemistry, cryogenic etch, charging, next generation

---

## Key Questions This Book Answers

1. **Which features are cut through the ON stack, and what does each require?**
2. **How do oxide and nitride deposition conditions change the etch rate?**
3. **Why is the effective rate a harmonic mean, and what does a rate mismatch cost?**
4. **How many layers does the etch front span, and does it matter that it alternates?**
5. **What chemistry makes R_N/R_ox ≈ 1, and why does hydrogen matter so much for nitride?**
6. **How much ion energy does a given aspect ratio need, and what does it cost in mask and heat?**
7. **Where do sidewall striations come from, and how large can they get?**
8. **How do stack stress and wafer bow change the etch at the wafer edge?**
9. **How many layers can one deck hold, and when does an extra deck pay for itself?**
10. **Why can't production endpoint count layers, and what replaces it?**

---

## How to Read This Book

**Complete study (2–3 weeks):** Read Part I closely, then work through Parts II and III in order. Finish with Part IV.

**Focused study (3–5 days):** Read Chapters 1 and 3, then follow the reading path for your role.

**Reference mode:** Go straight to the chapter you need. Use the INDEX, GLOSSARY, and the Appendix G troubleshooting guide.

**Every chapter includes:**
- Learning objectives
- Quantitative models with worked numerical examples
- Representative production values, labelled as illustrative where appropriate
- Summary and key takeaways
- Study questions

**Appendices provide:**
- A: Stack film, mask, and gas properties
- B: Chemistry and reaction data
- C: Standard procedures
- D: Process windows and lookup tables
- E: Stack-etch calculations
- F: Endpoint and metrology reference
- G: Troubleshooting guide

---

## A Note on Data and Depth

The relationships in this book are established in the plasma etch and thin-film literature. They include ion angular spread, Clausing and Knudsen transport, ARDE, charging deflection, Stoney bow, polymer-thickness etch models, and Poisson yield. The specific numbers in recipes, tables, and worked examples are **representative**. They are chosen to be physically consistent and close to typical practice, but they are not qualified conditions for any particular tool, mask, or stack. Where a value is illustrative, the text says so and shows the arithmetic, so readers can repeat the analysis with their own measurements.

Throughout the book, a **reference process** ties the examples together:

```
Reference stack:    SiO₂ 22 nm / Si₃N₄ 28 nm per pair (p = 50 nm, φ_ox = 0.44)
Reference deck:     160 pairs (8.0 µm) + 0.4 µm select/dummy/cap → H = 8.4 µm
Reference device:   2 decks + 0.4 µm inter-deck layer → total ON stack ≈ 17.2 µm
Reference rates:    R_ox,0 = 330 nm/min, R_N,0 = 300 nm/min (open area, A → 0)
                    → R_eff,0 = 312.5 nm/min, ρ = R_N/R_ox = 0.91
Reference hole:     CD_top 105 nm, CD_bottom 75 nm, w̄ = 90 nm, A = 93, 160 nm hex pitch
Reference slit:     W_top 180 nm, W_bottom 120 nm, w̄ = 150 nm, A = 56
Reference ARDE:     R = R_eff,0 / (1 + A/A₀); A₀ = 90 (hole), 120 (slit)
                    → hole 40.6 min per deck; slit 33.2 min
Reference ions:     5 keV mean, T_⊥ = 0.5 eV (σ_θ = 10 mrad), 4 kW to the wafer
Reference mask:     2.4 µm amorphous carbon + 50 nm SiON; 45 nm/min erosion in main etch
Reference chamber:  60 MHz source 3 kW, 400 kHz bias 12 kW, 20 mTorr, chuck +20 °C
                    (cryogenic variant: chuck −60 °C)
Reference stress:   SiO₂ −200 MPa, Si₃N₄ +100 MPa → stack −32 MPa
```

We assume you know basic plasma physics and fluorocarbon dielectric etch from earlier books. We do **not** assume you know 3D NAND architecture, PECVD stack design, high-aspect-ratio transport, or multi-keV bias engineering.

---

## Organization of This Repository

1. **README.md**: overview, scope, file structure, cross-references
2. **PREFACE.md**: this document
3. **INDEX.md**: detailed chapter outline, reading paths, estimated times
4. **chapters/**: Chapters 1–16
5. **appendices/**: Appendices A–G
6. **GLOSSARY.md**: technical terminology

---

## Acknowledgments & Scope

Book #25 is part of the **ChipFoundryServices Technical Series**. It draws on:

- The published plasma etch literature (ion-enhanced etching, fluorocarbon polymer models, Knudsen transport, charging in high-aspect-ratio features, cryogenic etch)
- The PECVD thin-film literature on silicon oxide and silicon nitride composition and stress
- Published descriptions of 3D NAND architecture and stack scaling
- Representative industrial practice for 3D NAND high-aspect-ratio etch modules
- The earlier books in this series, especially Books #19–24

It is a **technical reference for professionals**. Background in plasma processing is assumed.

---

## Final Thought

The ON stack looks like a simple material: two familiar dielectrics, repeated. Its difficulty is that the repetition never stops. The sidewall records every interface, the wafer carries the stress of every layer, and every new generation adds more of them.

Mastering stack etch means seeing that **the slower film sets the rate, the cone sets the energy, the mask sets the time, the bow sets the edge, and the height sets the number of decks**. This book is meant to build that understanding.

---

**Welcome to Book #25: 3D NAND High-Aspect-Ratio Oxide/Nitride Stack Etch.**

---

**Preface Version:** 1.0  
**Last Updated:** 2026-10-04
