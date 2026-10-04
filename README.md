# Book #25: 3D NAND High-Aspect-Ratio Oxide/Nitride Stack Etch — Cutting Through Hundreds of Alternating Dielectric Layers

## Overview

**Book #25** is a technical reference on **high-aspect-ratio (HAR) etch of oxide/nitride (ON) stacks**: the plasma etch that drives holes, trenches, and contacts straight through hundreds of alternating layers of silicon dioxide and silicon nitride in 3D NAND. The ON stack is the raw material of a replacement-gate 3D NAND array. Each nitride layer will become a word line and each oxide layer the insulator between two word lines. Every critical vertical feature in the array is cut through it. That includes the memory (channel) holes, the gate-line slits, the dummy and support holes in the staircase, and the through-array contacts that reach the CMOS below.

The earlier volumes in this series treat those features one at a time. This book treats the **stack as the etch medium**. A monolithic oxide film etches at one rate with one surface chemistry. An ON stack does not. The etch front switches material every 20–30 nm, and the polymer layer, surface chemistry, etch yield, and products change with it. The sidewall carries a record of every switch. The stack's thickness ratio, hydrogen content, density, and stress were all chosen in the deposition tool, and they decide how the etch behaves 10 µm down. As layer counts grow from 100 to 300 and on toward 1000, the stack also sets the limits of the etch: how deep a single deck can be, how much time a wafer spends in the chamber, and how much mask the etch consumes.

The basic method is the same for every feature. A thick amorphous-carbon mask defines the openings. A fluorocarbon/hydrofluorocarbon plasma, driven by multi-kilovolt ions, removes oxide and nitride at nearly equal rates and protects the sidewall with polymer. The etch stops in a landing layer. **Match the two materials, keep the ions vertical, keep enough mask, and arrive everywhere at once.**

Doing it is hard. The rate falls by half or more as the feature deepens. Ions must arrive within a fraction of a degree of normal. A wafer spends 30–45 minutes in the chamber for every deck. The stack bows the wafer by hundreds of micrometres. The sidewall striates at every interface, and the deepest features twist under charge. This book covers the materials science, physics, chemistry, equipment, and production engineering of etching the ON stack, and how those change as the stack grows.

---

## Intended Audience

This book is written for **semiconductor industry professionals** with working knowledge of plasma processing:

- **Process Engineers**: developing HAR recipes for ON stacks; matching oxide and nitride rates; controlling striation, bow, taper, twisting, and landing; balancing rate against mask budget
- **Equipment Engineers**: specifying reactors with 10–40 kW low-frequency bias, tailored waveforms, multi-zone and cryogenic chucks; managing arcing, drift, and parts wear over long recipes
- **Thin-Film & Integration Engineers**: designing stacks that are easy to etch: thickness ratio, film composition, hydrogen, stress, deck partitioning, and landing layers
- **Device Engineers**: understanding how stack-etch errors become cell-to-cell variation, word-line shorts, and edge-die loss
- **Researchers**: studying multilayer etch dynamics, interface transients, charging in layered dielectrics, cryogenic HF chemistry, and feature-scale simulation

The material assumes a working knowledge of plasma physics (Books #1–5) and fluorocarbon dielectric etch (Books #6–10). Book #19 (Carbon Hard Mask Etch) is helpful background for the mask chapter. Book #24 (3D NAND Memory Hole Etch) and the companion volume *3D NAND Slit Etch* treat the two largest customers of the stack etch in feature-specific depth.

---

## Technical Scope

### Core Concepts Covered

**Stack & Physics:**
- The ON stack as a periodic etch medium: pair pitch, thickness ratio, effective (harmonic-mean) rate
- Rate alternation, interface transients, and the multi-layer etch front
- Ion and neutral transport in holes and trenches at aspect ratios of 50–100+
- Aspect-ratio-dependent etching (ARDE) of a layered material
- Differential charging in a dielectric of alternating permittivity and leakage

**Materials & Chemistry:**
- PECVD oxide and nitride: density, hydrogen bonding, stoichiometry, stress, and how each sets etch rate
- Fluorocarbon and hydrofluorocarbon chemistries (C₄F₆, C₄F₈, CH₂F₂, CHF₃) with O₂, Ar, NF₃
- Oxide/nitride rate matching: the role of hydrogen, oxygen, and polymer thickness
- Cryogenic and hydrogen-fluoride-based etch of ON stacks
- Amorphous-carbon masks and landing layers

**Equipment Design:**
- Capacitively coupled reactors with VHF source and high-power low-frequency bias
- Ion energy distribution, tailored and pulsed bias waveforms, arcing control
- Multi-step and ramped recipes for deep stacks
- Wafer temperature, cryogenic chucks, and heat flow through a bowed wafer
- Wall conditioning and stability over 40-minute recipes

**Process Phenomena:**
- Sidewall striation, scalloping, and layer-selective lateral recess
- Bowing, necking, taper, and bottom-CD collapse
- Charging, twisting, tilt, and stress-driven pattern distortion
- Mask selectivity, landing, and loading between holes, slits, and contacts in one stack
- Scaling: multi-deck stacks, thinner pairs, 300–1000 layers, next-generation etch

**Production Integration:**
- Endpoint at extreme aspect ratio and why layer counting fades with depth
- Layer-resolved metrology: CD-SAXS, cross-section, X-ray, and inline inspection
- Feed-forward and feedback APC on stack thickness, rate, and edge tuning
- Yield signatures, throughput, chamber count, and cost of ownership

### Technology Context

- **Device architectures:** Replacement-gate charge-trap 3D NAND from 64 to 300+ word-line layers; one, two, and three decks; CMOS-under-array (CuA) and wafer-bonded configurations
- **Stack types:** SiO₂/Si₃N₄ (primary focus). SiO₂/poly-Si (OPOP) gate-first stacks and doped or modified films are covered where they differ
- **Features covered:** memory holes, slits, dummy and support holes, through-array contacts, and other through-stack openings
- **Manufacturing scale:** 300 mm wafers, 30–45 minutes of etch per deck, hundreds of HAR dielectric-etch chambers per high-volume fab

---

## Book Organization

### Part I: Fundamentals (4 Chapters)

**Chapter 1: The ON Stack in 3D NAND — Why Every Critical Etch Goes Through Alternating Dielectrics**
- The replacement-gate array and what the stack becomes
- Features cut through the stack: holes, slits, support holes, through-array contacts
- Stack height, aspect ratio, and layer-count scaling
- The specification sheet of a stack etch

**Chapter 2: Stack Films — PECVD Oxide & Nitride, Thickness Ratio & Stress**
- Deposition chemistry and film properties of stack oxide and nitride
- Hydrogen, density, and stoichiometry: what the etch sees
- Thickness ratio, pair pitch, and stack-height variation
- Film stress, wafer bow, and stress-balanced stacks

**Chapter 3: Etching Alternating Layers — Effective Rate, Rate Alternation & Interface Physics**
- The series model and the harmonic-mean effective rate
- Interface transients in the polymer layer
- The curved etch front and how many layers it spans
- ARDE of a layered material

**Chapter 4: ON Etch Chemistry — Fluorocarbons, Hydrogen & Rate Matching**
- Oxide and nitride etch mechanisms under fluorocarbon plasma
- Hydrogen, oxygen, and the polymer balance that sets R_N/R_ox
- Mask and landing selectivity
- Cryogenic and HF-based chemistries

### Part II: Hardware & Process Design (5 Chapters)

**Chapter 5: Reactor & RF Systems for Extreme-Aspect-Ratio Dielectric Etch**
- Why high-power capacitively coupled plasma
- Source and bias frequencies, power delivery, and arcing
- Uniformity, standing waves, and the edge
- Platforms and chamber matching

**Chapter 6: Ion Energy, Angular Spread & Bias Waveform Engineering**
- Required ion energy versus aspect ratio
- Ion energy distributions under sinusoidal and tailored bias
- Pulsing for charge relief and polymer control
- Energy cost: mask, heat, and parts

**Chapter 7: Recipe Architecture — Steps, Ramps & Deck Transitions**
- Mask open, main etch stages, landing, and overetch
- Ramping energy, chemistry, and temperature with depth
- Inter-deck joints and dummy layers
- Recipe sensitivity and robustness

**Chapter 8: Wafer Temperature, Cryogenic Etch & Heat Flow**
- Heat load from multi-kW ion power and the path to the chuck
- Temperature dependence of polymer, adsorption, and rate matching
- Cryogenic ON etch
- Chucking a bowed wafer

**Chapter 9: Chamber Conditioning & Long-Recipe Stability**
- Wall polymer, seasoning, and first-wafer effect
- Drift within a 40-minute recipe and across ring life
- Parts wear and edge control
- Stability monitoring

### Part III: Process Phenomena (5 Chapters)

**Chapter 10: Sidewall Striation, Scalloping & Layer-Selective Recess**
- How alternating layers write a pattern on the wall
- Lateral rate mismatch and exposure time
- Striation amplitude and its downstream cost
- Levers for a smooth wall

**Chapter 11: Profile Control — Bow, Necking, Taper & Bottom CD**
- Bow formation and depth
- Necking, taper, and bottom-CD collapse
- Profile across 8–20 µm
- Profile trade-offs

**Chapter 12: Charging, Twisting & Stress-Driven Distortion**
- Charging in a layered dielectric
- Twisting and bottom deflection
- Edge tilt
- Stress release, leaning, and in-plane distortion

**Chapter 13: Mask Selectivity, Landing & Loading Between Features**
- Mask budget and remaining mask
- Landing layers and overetch
- Holes, slits, and contacts in one stack: loading and ARDE
- Within-wafer uniformity

**Chapter 14: Scaling to 300–1000 Layers — Decks, Thinner Pairs & Next-Generation Etch**
- Height, aspect ratio, and the per-deck limit
- Thinner pairs and their etch consequences
- Deck count economics
- Next-generation chemistries, waveforms, and stacks

### Part IV: Production Scale (2 Chapters)

**Chapter 15: Endpoint, Layer-Resolved Metrology & Advanced Process Control**
- Endpoint at extreme aspect ratio; damping of layer-count signals
- Depth, profile, striation, and tilt metrology
- Feed-forward from stack thickness and mask
- Feedback, FDC, and virtual metrology

**Chapter 16: Integration, Yield & Cost of Ownership**
- What the stack etch hands to the next steps
- Defect modes and yield signatures
- Throughput, chamber count, and consumables
- Cost of ownership for the ON-stack etch module

---

## Key Technical Themes

1. **The stack is the etch medium.** Every through-stack feature etches the same alternating material. The stack's thickness ratio, hydrogen content, and density set the etch rate before any recipe is written.
2. **Match the rates, not just the average.** The effective rate is the thickness-weighted harmonic mean of the two rates. A mismatch shows up first as striation, then as profile and front roughness.
3. **The front spans layers.** A rounded bottom exposes oxide and nitride at once, and each region of the front is at a different point of the pair cycle. Interface transients are short, so the front acts on the average.
4. **Depth costs more than linearly.** ARDE makes etch time grow faster than depth. That fact, more than any other, decides how many decks a stack needs.
5. **The stack bends the wafer.** Hundreds of micrometres of bow change chucking, temperature, and edge tilt. Stress is an etch parameter.
6. **Layer signals vanish with depth.** The pair-period signal in optical emission averages out within the first micrometre, so production endpoint relies on landing layers and time, not layer counting.

---

## Cross-References to Prior Books

**Related Books in the Series:**

- **Books #1–5** (Plasma Physics & Chemistry Fundamentals): sheath physics, ion energy and angular distributions, radical generation and transport
- **Books #6–10** (Dielectric Etch & Fluorocarbon Chemistry): fluorocarbon polymer, F/C ratio, oxide and nitride etch mechanisms
- **Books #11–15** (Advanced Plasma Engineering): RF delivery, pulsing, gas delivery, endpoint detection
- **Book #19** (Carbon Hard Mask Etch): amorphous-carbon mask deposition, opening, and selectivity
- **Book #20** (Photoresist Ashing): removal of the remaining carbon mask
- **Book #23** (Staircase Etch): the same ON stack, etched one pair at a time
- **Book #24** (3D NAND Memory Hole Etch): the channel hole, the deepest customer of the stack etch
- **Companion volumes:** *3D NAND Slit Etch*, *Silicon Nitride Etch: Chemistry, Selectivity and Integration*, and *Contact-Hole Etch*

This book collects the parts of those volumes that belong to the stack itself, and adds the materials and scaling view that none of them treats on its own.

---

## File Organization

```
3d-nand-high-aspect-ratio-oxide-nitride-stack-etch/
├── README.md            ← You are here
├── PREFACE.md
├── INDEX.md
├── GLOSSARY.md
│
├── chapters/
│   ├── 01-on-stack-architecture.md
│   ├── 02-stack-film-properties.md
│   ├── 03-alternating-layer-etch-physics.md
│   ├── 04-on-etch-chemistry.md
│   ├── 05-reactor-rf-systems.md
│   ├── 06-ion-energy-waveforms.md
│   ├── 07-recipe-architecture.md
│   ├── 08-temperature-cryogenic-etch.md
│   ├── 09-chamber-conditioning-stability.md
│   ├── 10-striation-scalloping-recess.md
│   ├── 11-profile-bow-taper.md
│   ├── 12-charging-twisting-distortion.md
│   ├── 13-mask-landing-loading.md
│   ├── 14-scaling-multideck-nextgen.md
│   ├── 15-endpoint-metrology-apc.md
│   └── 16-integration-yield-coo.md
│
└── appendices/
    ├── A-stack-film-properties.md
    ├── B-chemistry-reaction-data.md
    ├── C-standard-procedures.md
    ├── D-process-windows.md
    ├── E-stack-etch-calculations.md
    ├── F-endpoint-metrology-reference.md
    └── G-troubleshooting-guide.md
```

---

## Constraints & Scope

### What This Book Covers
✅ HAR plasma etch of SiO₂/Si₃N₄ stacks (primary focus) and SiO₂/poly-Si stacks where they differ  
✅ Stack film properties as etch inputs: composition, hydrogen, density, stress, thickness ratio  
✅ All through-stack features: holes, slits, support holes, through-array contacts  
✅ Equipment design, chamber control, and production integration  
✅ Layer-count scaling, multi-deck partitioning, and next-generation etch  
✅ Yield impact and cost of ownership  

### What This Book Does NOT Cover
❌ Feature-specific detail already covered by Book #24 and the slit-etch companion (hole web margin, slit wiggle, common-source formation), beyond what the stack decides  
❌ Staircase formation (see Book #23)  
❌ Wet nitride removal, word-line metal fill, and channel deposition, beyond what they require of the etch  
❌ Lithography of the hole and slit layers  
❌ Vendor-specific recipes or proprietary tool parameters  

### A Note on Numbers
Numbers in this book come from established plasma physics, published literature trends, and representative production practice. Worked examples use **illustrative values** chosen to show the method, and the arithmetic is written out so readers can substitute their own data. A single **reference process** (a two-deck stack of 22 nm oxide / 28 nm nitride pairs, 160 pairs per deck, a 90 nm mean-width hole and a 150 nm mean-width slit, and a 2.4 µm carbon mask) is used across chapters so that examples connect. Treat recipe values as starting points for a design of experiments, never as qualified process conditions.

---

## Development Status

**Book #25 Foundation:** Complete  
**Part I (Chapters 1–4):** Complete  
**Part II (Chapters 5–9):** Complete  
**Part III (Chapters 10–14):** Complete  
**Part IV (Chapters 15–16):** Complete  
**Back Matter (Appendices A–G, Glossary):** Complete  

---

## Next Steps

1. **Read [PREFACE.md](./PREFACE.md)** for the motivation and reading guidance
2. **Read [INDEX.md](./INDEX.md)** for the detailed chapter outline and reading paths by role
3. **Begin [Chapter 1](./chapters/01-on-stack-architecture.md)**: The ON Stack in 3D NAND

---

**Book #25 Version:** 1.0  
**Last Updated:** 2026-10-04  
**Series:** ChipFoundryServices Technical Series
