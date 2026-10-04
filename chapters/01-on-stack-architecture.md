# Chapter 1: The ON Stack in 3D NAND — Why Every Critical Etch Goes Through Alternating Dielectrics

## Overview

A replacement-gate 3D NAND array starts life as a blanket stack of alternating silicon dioxide and silicon nitride layers, hundreds of layers deep. Nothing in the array has been patterned yet. Every structure that follows has to be cut through that stack: the vertical channels, the trenches that divide the array into blocks, the dummy holes that hold up the staircase, and the contacts that pass through the array to the logic below. This chapter describes the stack, what each layer becomes, which features are etched through it, and how the stack's height and the features' widths combine into the aspect ratios that make the etch hard. It ends with a specification sheet that applies, with different numbers, to every through-stack feature.

**Learning Objectives:**
- Describe the replacement-gate flow and what the oxide and nitride layers become
- List the features etched through the ON stack and their typical dimensions and aspect ratios
- Compute stack height from layer count, pair pitch, and overhead layers
- Explain why layer count, not lateral shrink, drives 3D NAND scaling, and what it costs the etch
- Write the specification sheet for a through-stack etch and identify which items the stack itself controls

---

## 1.1 From a Planar String to a Vertical String

### 1.1.1 The NAND String

A NAND string is a series chain of memory transistors between two select transistors. In planar NAND the chain lies along the wafer surface. In 3D NAND it stands on end: the channel is a vertical polysilicon tube, and each memory cell is the place where a horizontal word-line plate wraps around that tube.

```
Planar NAND string                      Vertical (3D) NAND string

  SSL  WL0  WL1  ...  WLn  GSL           ┌── bit line ──┐
  ─┬─  ─┬─  ─┬─        ─┬─  ─┬─                  │
   │    │    │          │    │           SSL ───██─── (select)
 ══╧════╧════╧══ ... ═══╧════╧══         WLn ───██─── (cell)
   channel along the surface             ...    ██
                                         WL1 ───██─── (cell)
                                         WL0 ───██─── (cell)
                                         GSL ───██─── (select)
                                                 │
                                           source plate
                                         ██ = vertical channel in a hole
```

To stack cells vertically, the process deposits all the gate levels first, as a blanket stack, and then cuts holes through it. One lithography step and one etch create every cell of every string at once. That is the economic reason for 3D NAND, and it is the reason the stack etch exists.

### 1.1.2 What the Layers Become

In the replacement-gate (charge-trap) flow, the stack is deposited as alternating oxide (O) and nitride (N) layers:

```
Layer         Thickness (ref.)   Role during etch        Final role
──────────────────────────────────────────────────────────────────────────────
SiO₂ (O)      22 nm              Etched                  Inter-word-line insulator
Si₃N₄ (N)     28 nm              Etched                  Sacrificial; removed in hot
                                                         H₃PO₄ through the slit and
                                                         replaced by W or Mo word line
Pair (ON)     50 nm (p)          One period of the etch  One word line + one insulator
```

The nitride is a placeholder. Its thickness is chosen for the word line it will become: thick enough for low resistance after the metal and barrier go in. The oxide thickness is chosen for word-line-to-word-line breakdown, capacitive coupling, and the cell's electrostatics. Neither choice is made for the etch.

The alternative gate-first stack uses oxide and doped polysilicon (OP). The polysilicon layers are the word lines and are never replaced. Chapter 4 covers how the chemistry changes for OP stacks.

### 1.1.3 The Replacement-Gate Sequence

```
Step                                    What the ON-stack etch must provide
──────────────────────────────────────────────────────────────────────────────────
1. Deposit ON stack (deck 1)            —
2. Etch deck-1 holes; fill sacrificial  Holes landed on the source layer
3. Deposit ON stack (deck 2)            —
4. Etch deck-2 holes aligned to deck 1  Holes landed in the deck-1 plug
5. Remove plug; deposit memory films    Wide enough, smooth enough walls for
   and channel                          ALD blocking/trap/tunnel films
6. Form staircase (Book #23)            —
7. Etch support holes in staircase      Holes landed through stepped stack
8. Etch slits                           Trenches landed in the source stack
9. Remove nitride through slits         Open path for liquid; no bridged
                                        blocks
10. Deposit word-line metal; recess     Bottom wide enough to fill and clear
11. Fill slit; form source contact      —
12. Etch through-array contacts         Contacts through both decks to CMOS
```

Four of these steps are ON-stack etches (2/4, 7, 8, 12). Together they are the largest block of etch chamber time in the whole flow.

---

## 1.2 Features Cut Through the Stack

### 1.2.1 The Feature Table

```
Feature                  Shape     Width (top)    Depth            A (=H/w̄)   Lands on
──────────────────────────────────────────────────────────────────────────────────────────
Memory (channel) hole    Round     90–120 nm      One deck,        70–100     Source poly /
                                                  6–10 µm                     plug
Slit (gate-line slit)    Line      150–250 nm     Full stack,      40–80      Source stack
                                                  8–18 µm
Support (dummy) hole     Round     150–300 nm     Varies with      30–60      Source / stop
                                                  staircase step              layer
Through-array contact    Round or  300–600 nm     Full stack,      30–50      CMOS metal
 (TAC)                    slot                    15–20 µm                    landing pad
Select-gate cut          Line      60–100 nm      Top 3–6 pairs    2–5        In stack
```

**Reference values used through this book:**

```
Reference hole:   CD_top 105 nm, CD_bottom 75 nm, w̄ = 90 nm, depth 8.4 µm
                  A = 8400 / 90 = 93
Reference slit:   W_top 180 nm, W_bottom 120 nm, w̄ = 150 nm, depth 8.4 µm (per deck)
                  A = 8400 / 150 = 56
Reference support hole: w̄ = 200 nm, depth 8.4 µm → A = 42
Reference TAC:    w̄ = 400 nm, depth 17.2 µm → A = 43
```

The aspect ratio here is defined with the **mean width** w̄ = (top + bottom)/2, because that is the width that best predicts the transport (Chapter 3). Specifications often quote the top width, which gives a smaller number: the reference hole is 80:1 by top CD and 93:1 by mean CD.

### 1.2.2 Why the Features Differ

All of these features cut the same material, and their etches share chemistry and hardware. But they differ in shape, width, and density:

- **Holes** are the narrowest and densest. They set the hardest transport limit and the largest exposed area at the bottom.
- **Slits** are long trenches. A slot passes several times more neutral flux than a round hole of the same aspect ratio (Chapter 3), so the slit etches faster at the same depth, but it must stay straight over millimetres.
- **Support holes** sit in the staircase, where the stack above each tread has a different thickness. They see oxide fill above a partial ON stack.
- **TACs** go through both decks at once and land on metal, so they are the deepest single etch in absolute depth, but wide.

Because these features share the same layers, an improvement in the stack (for example a nitride that etches closer to the oxide rate) helps all of them at once. The same is true of a problem.

---

## 1.3 Stack Height and Layer Count

### 1.3.1 Height of a Deck

```
H_deck = N_pairs × p + h_overhead

N_pairs     = word lines + dummy word lines + select-gate levels
p           = pair pitch = d_ox + d_N
h_overhead  = cap oxide, bottom buffer, etch-stop and inter-deck layers

Reference deck:
  N_pairs = 160, p = 50 nm → 8.0 µm
  h_overhead = 0.4 µm
  H_deck = 8.4 µm
```

### 1.3.2 Scaling by Generation

```
Generation   Total pairs    Pair pitch   Pair height    Decks   Height per deck
(word lines) (incl. dummy,  (nm)         (µm)                   (µm, approx.)
              select)
──────────────────────────────────────────────────────────────────────────────────
  64           72            62            4.5           1          4.5
  96          108            58            6.3           1–2        6.3 or 3.2
 128          144            55            7.9           1–2        7.9 or 4.0
 176          196            52           10.2           2          5.1
 236          260            50           13.0           2          6.5
 300+ (ref.)  320            50           16.0           2          8.0
 400+         440            45           19.8           2–3        9.9 or 6.6
```

*(Illustrative trend values. Real products vary in dummy count, overhead, and deck split.)*

Two trends run together. **Layer count grows**, raising total height. **Pair pitch shrinks**, partly offsetting it. The pitch cannot shrink as fast as the layer count grows, because the word line needs enough metal and the insulator needs enough breakdown margin. Total stack height therefore rises with each generation.

### 1.3.3 Why Height, Not Width

Bit density per unit area scales as:

```
Bits per mm² ∝ (layers × bits per cell) / (hole pitch)²
```

```
Option                                Density gain     Etch consequence
───────────────────────────────────────────────────────────────────────────────
+33% layers (240 → 320)               +33%             +33% height; > +33% time
−10% hole pitch (160 → 144 nm)        +23%             narrower hole → higher A,
                                                       thinner web
+1 bit per cell (TLC → QLC)           +33%             tighter cell variation →
                                                       tighter profile spec
```

Shrinking the hole pitch makes the hole narrower and the wall between holes thinner, so it makes the etch harder in two ways at once. Adding layers makes the etch longer but not narrower. For most of the 3D NAND roadmap, manufacturers have preferred to add layers and keep the hole roughly the same width. That choice moves the difficulty from lithography to the stack etch.

---

## 1.4 What Aspect Ratio Means for the Etch

### 1.4.1 Three Consequences

Aspect ratio controls three things that do not scale the same way (Chapter 3):

```
Quantity                   How it depends on A           Reference hole (A = 93)
─────────────────────────────────────────────────────────────────────────────────
Ion acceptance angle       θ_c ≈ 1/A                     10.8 mrad (0.62°)
Neutral transmission       W ≈ 1/(1 + 3A/4) for a        1.4% (non-sticking
 (round hole)              long tube                      neutral)
Etch rate                  R = R₀/(1 + A/A₀)             R/R₀ = 0.49 at the bottom
```

### 1.4.2 Etch Time

Integrating the rate over depth (Chapter 3, Section 3.5):

```
t(A) = (w̄ / R₀) · (A + A²/(2A₀))

Reference hole: w̄ = 90 nm, R₀ = 312.5 nm/min, A₀ = 90
  w̄/R₀ = 0.288 min
  t(93) = 0.288 × (93 + 93²/180) = 0.288 × (93 + 48.1) = 40.6 min

Reference slit: w̄ = 150 nm, A₀ = 120
  w̄/R₀ = 0.480 min
  t(56) = 0.480 × (56 + 56²/240) = 0.480 × (56 + 13.1) = 33.2 min
```

The A²/(2A₀) term is the cost of ARDE. In the reference hole it adds 52% to the time an un-slowed etch would take. In a deck twice as tall it would add 103%.

### 1.4.3 The Per-Deck Limit

A deck cannot be made arbitrarily tall, because:

1. **Time** grows as A + A²/(2A₀), which costs chamber capacity (Chapter 16).
2. **Mask** erodes at a roughly constant rate while the front slows down, so the mask thickness must grow with time, and a thicker mask raises the effective aspect ratio further (Chapter 13).
3. **Bottom CD** shrinks with taper. With a fixed taper angle, a hole twice as deep closes off before it reaches the bottom (Chapter 11).
4. **Distortion** (twisting and tilt) grows with depth, and the bottom displacement must stay inside the joint tolerance for the next deck (Chapter 12).

Production stacks have settled at roughly 6–10 µm per deck for holes, with 2 decks above about 200 layers and 3 decks expected above about 400 layers. Chapter 14 builds this limit into a deck-count model.

---

## 1.5 The Density of the Problem

### 1.5.1 How Many Features

```
Reference hole array: hexagonal pitch 160 nm
  Area per hole = (√3/2) × 0.160² µm² = 0.02217 µm²
  Hole density  = 45.1 holes per µm² = 4.51 × 10⁷ per mm²

Array fraction of the die ≈ 0.65 (rest is staircase, slits, periphery)
Die area ≈ 70 mm² (illustrative)
  Holes per die ≈ 70 × 0.65 × 4.51×10⁷ = 2.1×10⁹ per deck
  Die per wafer ≈ 800 → 1.6×10¹² holes per wafer per deck
```

Every one of these holes must reach the landing layer, keep its bottom CD, and stay inside its displacement budget. A failure rate of 10⁻¹² per hole would still leave one or two failing holes per wafer. The control problem is a tail problem (Chapter 16).

### 1.5.2 Exposed Area

```
Hole top area   = π/4 × 105² = 8,659 nm²   → 39% of the cell area
Hole bottom area= π/4 × 75²  = 4,418 nm²   → 20% of the cell area

Array open area at the top ≈ 0.65 × 39% ≈ 25% of the die
```

A quarter of the die area is open at the start of the hole etch, and the mask covers the rest. The open fraction matters for loading (Chapter 13) and for endpoint signal (Chapter 15).

---

## 1.6 The Specification Sheet

### 1.6.1 Generic Through-Stack Specification

Every through-stack etch is specified with the same list of items. Only the numbers change.

```
Item                    Reference hole spec          Controlled mostly by
───────────────────────────────────────────────────────────────────────────────────
Landing                 All holes in landing layer;  Time, selectivity, ARDE,
                        recess ≤ 30 nm               stack height variation
Top CD                  105 ± 3 nm (3σ)              Mask open, litho, mask facet
Max CD (bow)            ≤ 115 nm                     Ion angle, passivation, mask
Bottom CD               ≥ 70 nm                      Taper, chemistry at depth
Striation amplitude     ≤ 2 nm peak-to-valley        ON rate matching, lateral
                                                     rate, exposure time
Bottom displacement     ≤ 25 nm (3σ, twist)          Charging, energy, pulsing
Edge tilt               ≤ 0.15° at 3 mm from edge    Edge sheath, ring wear, bow
Remaining mask          ≥ 300 nm a-C at the edge     Mask thickness, selectivity
Front uniformity        Depth 3σ ≤ 3% before landing Rate uniformity, stack
                                                     thickness uniformity
Defects                 No blocked holes, no         Particles, polymer flakes,
                        unopened arrays              mask defects
```

### 1.6.2 What the Stack Controls

Several items are set by the stack before the wafer reaches the etch chamber:

```
Specification item     Stack property that sets it            Chapter
─────────────────────────────────────────────────────────────────────────
Rate and time          Oxide/nitride rates and thickness       2, 3
                       ratio (harmonic mean)
Striation              Rate and lateral-rate mismatch          10
Landing margin         Stack height variation (±1–2%)          2, 13
Edge tilt              Wafer bow from stack stress             2, 12
Front uniformity       Radial thickness profile of the stack   2, 15
Bottom CD              Composition change at the stack bottom  2, 11
```

A stack change (new deposition recipe, new chamber, a new nitride precursor) is an etch change. Chapter 2 describes the stack properties that the etch engineer should monitor.

---

## 1.7 Where the Stack Etch Sits

```
                ┌──────────────────────────────────────────────────┐
  Thin film ──▶ │ ON stack deposition (PECVD, multi-station,       │
                │ ~4–8 h per deck, stress compensation on backside)│
                └──────────────────────────────────────────────────┘
                                      │
                ┌──────────────────────────────────────────────────┐
  Litho/mask ─▶ │ a-C hard mask (2–3 µm) + SiON + litho + mask open│
                └──────────────────────────────────────────────────┘
                                      │
                ┌──────────────────────────────────────────────────┐
  Etch ───────▶ │ HAR ON-stack etch (30–45 min per deck)           │
                │  → this book                                     │
                └──────────────────────────────────────────────────┘
                                      │
                ┌──────────────────────────────────────────────────┐
  Strip/clean ▶ │ Ash mask, wet clean, metrology                   │
                └──────────────────────────────────────────────────┘
                                      │
                Memory films / slit fill / nitride replacement / contact fill
```

Because deposition and etch are in different modules, a common failure is that each side optimizes alone. The deposition engineer reduces hydrogen to improve the cell, and the nitride rate drops by 15%. The etch engineer raises bias to recover rate, and the mask budget runs out. The stack etch works best when the stack is treated as a shared design.

---

## 1.8 Summary & Key Takeaways

1. **The ON stack is the raw material of the array.** Nitride layers become word lines, oxide layers become insulators, and every vertical feature is cut through both.

2. **Four families of features share one material.** Holes, slits, support holes, and through-array contacts differ in width and shape (A = 40–100) but etch the same layers.

3. **Height grows with layer count.** H_deck = N·p + overhead. The reference deck is 8.4 µm, and the reference device has two decks for about 17 µm of stack.

4. **Time grows faster than height.** t = (w̄/R₀)(A + A²/2A₀): 40.6 min for the reference hole. ARDE adds half again to the time.

5. **The per-deck limit is set by time, mask, bottom CD, and distortion.** It sits near 6–10 µm for holes today.

6. **The stack sets part of the specification.** Rate, striation, landing margin, edge tilt, and uniformity are partly decided by deposition.

---

## Study Questions

1. A product has 280 word lines, 24 dummy and select levels, and a pair pitch of 48 nm. Overhead is 0.5 µm per deck. Compute the total height for one deck and for two equal decks.

2. For a hole with w̄ = 95 nm, A₀ = 85, and R₀ = 300 nm/min, compute the time to etch 7.6 µm. What fraction of that time is caused by the ARDE term?

3. A designer proposes cutting the hole pitch from 160 nm to 150 nm at constant hole CD. By what percentage does bit density rise? By how much does the top web between holes shrink if the top CD stays 105 nm?

4. A single-deck alternative to the reference two-deck device would be 16.8 µm tall with the same hole. Compute its aspect ratio and etch time with the reference ARDE values. Compare with two reference decks.

5. Using Section 1.5, estimate how many holes per wafer would fail to land if the per-hole failure probability is 3×10⁻¹². What die yield loss results if each failing hole kills one die (Poisson, 800 die)?

---

**Next Chapter:** [Chapter 2: Stack Films — PECVD Oxide & Nitride, Thickness Ratio & Stress](./02-stack-film-properties.md)

---

**Chapter 1 Development Status:** Complete  
**Version:** 1.0
