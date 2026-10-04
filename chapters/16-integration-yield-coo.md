# Chapter 16: Integration, Yield & Cost of Ownership

## Overview

The ON-stack etch is judged by what it hands to the next steps and by what it costs to do so. Holes must accept memory films, slits must let liquids and metals in and out, support holes must hold up the staircase, and contacts must reach the logic below. When the etch misses, the failure usually appears weeks later at electrical test, with nothing visible at the surface. And because every wafer spends three to four hours in HAR etch chambers across all stack layers, the stack etch is one of the largest capital and operating costs in a NAND fab. This chapter traces etch outcomes to downstream failures, builds a die-yield model with redundancy, reads wafer-map signatures, and computes the cost of ownership and chamber count of the ON-stack etch module.

**Learning Objectives:**
- Map each etch outcome to the downstream step and the electrical failure it causes
- Build a Poisson die-yield model with redundancy for random failure modes, and compare it with systematic edge loss
- Recognize wafer-map signatures and trace them to etch causes
- Compute cost per minute and cost per wafer for HAR etch chambers
- Estimate the chamber count for a given wafer-start rate, and the capital saved by faster etch
- Evaluate yield–cost trade-offs such as overetch time and ring replacement interval

---

## 16.1 What the Etch Hands Downstream

```
Feature        Next steps                         What they need from the etch
──────────────────────────────────────────────────────────────────────────────────
Memory hole    Plug/joint (multi-deck), blocking  Landed; bottom CD ≥ spec; smooth
               oxide, trap nitride, tunnel        wall (low modulation); joint
               oxide, channel poly, core fill     aligned; no residue; no bow merge
Slit           Hot H₃PO₄ nitride removal, WL      Landed in source stack; bottom
               metal (W/Mo) ALD, recess, liner,   wide enough for fill and recess;
               fill, source contact               no bridge; tilt inside clearance
Support hole   Oxide fill (mechanical support     Landed through the stepped stack;
               during nitride removal)            no unopened holes
TAC            Liner, barrier, metal fill to      Landed on metal with low recess;
               CMOS                               bottom area for resistance;
                                                  no arcing damage
```

---

## 16.2 Failure Modes

### 16.2.1 From Etch Outcome to Electrical Failure

```
Etch outcome                     Downstream consequence             Electrical failure
──────────────────────────────────────────────────────────────────────────────────────
Unlanded hole (etch stop,        No channel contact to source       String open
 clog, blocked by particle)
Hole over-recess into source     Source contact geometry off;       String current shift;
                                 punch-through in thin landings     leakage
Bow merge between holes          Memory films bridge adjacent       String-to-string short;
 (web gone)                      holes                              disturb
Joint miss (deck-2 bottom off    Channel pinched or broken at the   String open / high
 the deck-1 pad)                 joint                              resistance
Large modulation / rough wall    Film thickness and coupling        V_t spread; retention
                                 vary by cell                       loss; read margin
Slit unlanded or bridged         Nitride not removed; WLs of two    Block failure (two
                                 blocks connected                   blocks)
Slit tilt into hole row          Slit fill or WL metal near the     WL-to-channel leakage
                                 channel
TAC unlanded / high recess       Open or high-R contact; damage     Periphery failure (die
                                 to CMOS metal                      kill)
Arcing crater                    Local destruction of the stack     Die kill
```

### 16.2.2 Redundancy

NAND tolerates some failures:

- **Column redundancy and ECC** repair a limited number of failing strings and bits per page.
- **Bad-block management** maps out a small fraction of blocks (≈ 2% allowance, illustrative).

So a random hole failure usually costs nothing at die level. A cluster, a periphery contact, or a failure that exceeds the allowance costs the die.

---

## 16.3 Die-Yield Model

### 16.3.1 Random Modes

```
Y_random = exp(−Σ λ_i),     λ_i = N_i × p_i × u_i

N_i = features per die; p_i = failure probability per feature;
u_i = fraction not repaired by redundancy (illustrative)

Mode                         N_i per die   p_i       u_i     λ_i
────────────────────────────────────────────────────────────────────────
Unlanded hole (2 decks)      4.2×10⁹       2×10⁻¹²   0.1     8.4×10⁻⁴
Joint miss (deck 2)          2.1×10⁹       5×10⁻¹²   0.1     1.05×10⁻³
Slit bridge                  4,000         1×10⁻⁵    0.01    4.0×10⁻⁴
Large flakes (≥ 5 µm)        —             —         —       7.0×10⁻⁴
 (Chapter 9: 0.001/cm² × 0.7 cm²)
Arcing craters               —             —         —       2.0×10⁻⁴
────────────────────────────────────────────────────────────────────────
Σλ = 3.2×10⁻³  →  Y_random = 99.7%
```

### 16.3.2 Systematic Edge Loss

The random modes cost about 0.3% of die. Systematic edge problems can cost ten times more:

```
Die in the outer ring (within ~5 mm of the edge exclusion): ~24 of 800 (3%)

Edge tilt in spec (≤ 0.15°):        loss ≈ 0
Edge tilt 0.25° (ring worn, bow):   most of the outer ring fails → loss ≈ 3%
Edge mask exhausted (Ch. 13):       bow and CD fail at the edge  → loss ≈ 1–3%
```

**The wafer edge sets the yield of the stack etch.** The random tail of 10¹² features matters for the design of the overetch, but it costs less yield than a worn ring or an unseated wafer.

---

## 16.4 Wafer-Map Signatures

```
Signature                                 Likely etch cause                       Chapter
──────────────────────────────────────────────────────────────────────────────────────────
Full outer ring of failing die            Edge tilt (ring wear, edge tuning);     9, 12
                                          edge mask exhaustion                    13
Two opposite edge arcs (cos 2φ)           Saddle-shaped wafer chucking; tilt      8, 12
                                          from anisotropic bow
One-sided edge arc                        Ring seated off-centre; wafer           9, 12
                                          placement offset; gas asymmetry
Centre-low depth (unlanded at centre)     Stack thick at centre + etch slow at    13
                                          centre (profiles adding)
Isolated die, random                      Particles, flakes, arcing               5, 9
First wafer of lot worse                  First-wafer / idle effect               9
Pattern follows the chamber, not the lot  Chamber mismatch (RF, parts)            5, 9
Pattern follows the deposition chamber    Stack composition or thickness          2
                                          (H content, profile)
Gradual drift over weeks then reset       Ring/electrode wear and PM cycle        9
```

The last two rows are the stack-specific ones: if the yield pattern follows the **deposition** tool rather than the etch tool, the stack itself is the cause.

---

## 16.5 Cost of Ownership

### 16.5.1 Cost per Chamber-Minute

```
Capital (illustrative): $5.0M per chamber (including platform share)
Depreciation: 5 years → $1.0M per year
Available time: 525,600 min/yr × 85% uptime = 446,760 min/yr
Depreciation per minute: $2.24

Consumables per wafer pass (illustrative, reference hole recipe):
  Upper electrode   $15,000 / 1,000 wafers       $15.0
  Edge ring         $6,000 / 1,500 wafers         $4.0
  ESC               $120,000 / 30,000 wafers      $4.0
  Other parts       (liners, confinement)         $5.0
  Gases                                           $4.0
  Electricity       (~30 kW × 0.75 h)             $2.3
  ───────────────────────────────────────────────────────
  Total                                          $34.3  → $0.76 per min of etch

Total ≈ $3.0 per chamber-minute
```

### 16.5.2 Cost per Wafer

```
Chamber time per wafer = etch (incl. OE) + overhead (WAC, transfer, stabilize ≈ 3.5 min)

Layer               Etch (min)    Chamber time (min)    Cost at $3.0/min
─────────────────────────────────────────────────────────────────────────
Hole, deck 1         45.1           48.6                 $146
Hole, deck 2         45.1           48.6                 $146
Slit                 36.5           40.0                 $120
Support holes        31.5           35.0                 $105
TAC                  44.5           48.0                 $144
─────────────────────────────────────────────────────────────────────────
ON-stack etch module                220 min              ≈ $660 per wafer
```

*(Chapter 5's platform example used 40.6 min of etch without overetch; the full chamber time is used here.)*

### 16.5.3 Chamber Count

```
Fab: 50,000 wafer starts per month
Chamber-hours needed per month = 50,000 × 220 / 60 = 183,500 h
Available per chamber per month = 730 × 0.85 = 620 h
Chambers needed ≈ 296   (≈ $1.5B of capital at $5M each)
```

### 16.5.4 What Faster Etch Is Worth

```
10% shorter chamber time on every layer (220 → 198 min):
  Chambers saved ≈ 30   → ≈ $150M of capital
  Cost per wafer saved ≈ $66

Cryogenic hole etch (Chapter 8 question): 18 min etch + 2.5 min extra cool/warm
  vs. 45.1 min: hole chamber time 48.6 → 24.0 min per deck
  Saves ≈ 49 min per wafer (two decks) → ≈ $147 per wafer, ≈ 66 chambers
  Against: cryogenic chamber cost premium, chiller power, new failure modes
```

The capital involved explains why each etch-rate improvement in HAR etch is pursued so hard, and why a deck saved (Chapter 14) is worth even more.

---

## 16.6 Yield–Cost Trade-Offs

### 16.6.1 Overetch

```
Adding 1 min of overetch to each hole deck:
  Cost: 2 min × $3.0 = $6 per wafer; ≈ 45 nm more mask consumed per deck
  Benefit: random tail covered to ~9σ instead of 7σ (σ = 0.41 min: 3.8 vs. 2.8 min)
    → unlanded-hole p_i falls by orders of magnitude, but λ was already 8.4×10⁻⁴
  Risk: edge mask exhaustion (Ch. 13) → systematic edge loss

Net: more overetch rarely pays in yield; it often costs edge yield through the mask.
```

### 16.6.2 Ring Replacement Interval

```
Ring life extended from 1,500 to 3,000 wafers (with ring lift):
  Saves $2 per wafer in ring cost and one PM per 1,500 wafers
  Risk: edge tilt drift beyond compensation → outer-ring die loss (up to 3%)
  At a die value of ~$5 and 800 die per wafer, 3% loss = $120 per wafer

Net: a ring replacement that prevents even 0.1% edge loss ($4 per wafer)
pays for itself twice over.
```

**In HAR stack etch, yield at the wafer edge is worth far more than the consumables that protect it.**

---

## 16.7 The Stack Etch Handoff Specification

```
Item                         Reference spec              Verified by
──────────────────────────────────────────────────────────────────────────────
Landing                      All features landed;        VC inspection; SAXS depth;
                             recess ≤ 30 nm              cross-section sample
Bottom CD (hole)             ≥ 70 nm                     SAXS; HV-SEM
Bow (hole)                   ≤ 115 nm                    SAXS; cross-section
Layer modulation (after      ≤ 2 nm etch; ≤ 3 nm after   SAXS superlattice peaks;
 clean)                      clean                       TEM sample
Bottom displacement / joint  ≤ 22.5 nm offset to the pad SAXS; HV-SEM top/bottom
Edge tilt                    ≤ 0.15° at 3 mm             SAXS rocking at edge sites
Remaining mask               ≥ 300 nm at the edge        Cross-section sample
Defects                      Adders and blocked arrays   Inspection after strip
                             within limits
Wafer bow after etch         Within the chucking class   Wafer shape metrology
                             of the next step
```

---

## 16.8 Summary & Key Takeaways

1. **Every etch outcome has a downstream owner.** Unlanded holes become string opens, bridged slits become block failures, and edge tilt becomes word-line leakage.

2. **Redundancy absorbs random feature failures.** The illustrative random modes cost about 0.3% of die.

3. **The edge costs more than the tail.** Out-of-spec edge tilt or edge mask exhaustion can cost about 3% of die.

4. **Wafer maps point to the cause.** A pattern that follows the deposition tool means the stack is the cause.

5. **Chamber time costs about $3 per minute.** The ON-stack etch module costs about $660 per wafer and needs about 300 chambers for 50,000 wafer starts per month.

6. **Rate is capital.** A 10% faster etch saves about 30 chambers (≈ $150M) in that fab.

7. **Protect the edge.** Rings, chucking, and edge mask margin are cheap compared with the die they protect.

---

## Study Questions

1. Recompute Y_random if the joint-miss probability rises to 2×10⁻¹¹ because deck 2 is 15% taller (twist ∝ H^(3/2)). Which mode now dominates?

2. A fab runs 80,000 wafer starts per month with the module times in Section 16.5.2. How many chambers are needed? How many are saved if the hole etch alone becomes 20% faster?

3. Compute the cost per chamber-minute for a chamber that costs $6.5M with 88% uptime and $40 of consumables per 45-minute pass.

4. An edge-ring PM costs $6,000 in parts plus 10 h of downtime. Express the downtime in chamber-minutes and dollars at $3.0/min. With a die value of $5, how much edge yield must the PM protect to break even per 1,500 wafers?

5. Wafer maps show a cos 2φ edge pattern that appeared after slits were moved earlier in the flow. Explain the likely mechanism and two actions that would address it.

---

**Previous Chapter:** [Chapter 15: Endpoint, Layer-Resolved Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)

**Back Matter:** [Glossary](../GLOSSARY.md) | [Appendix A](../appendices/A-stack-film-properties.md) | [Appendix G: Troubleshooting](../appendices/G-troubleshooting-guide.md)

---

**Chapter 16 Development Status:** Complete  
**Version:** 1.0
