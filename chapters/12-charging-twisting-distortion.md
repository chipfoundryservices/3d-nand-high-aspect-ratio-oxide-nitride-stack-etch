# Chapter 12: Charging, Twisting & Stress-Driven Distortion

## Overview

A through-stack feature must end where it was aimed. Three groups of effects push it off course. Charging inside the feature bends the ions that make the bottom, so deep features wander at random (twisting). The ion direction itself tilts at the wafer edge, and a bowed wafer that is not fully seated presents the wrong surface angle to the ions (tilt). The stack's stress moves the pattern in the plane of the wafer before and after the etch (distortion). This chapter treats each of these as a displacement at the feature bottom, since that is what the joint, the landing, and the downstream contacts care about, and shows how each scales with depth.

**Learning Objectives:**
- Explain differential charging in a HAR feature and estimate ion deflection from a lateral potential difference
- Describe what the layered ON wall changes about charging and what it does not
- Model twisting as a random walk of the ion direction and show that displacement grows as depth^(3/2)
- Compute edge tilt from sheath bending and from imperfect chucking of a bowed wafer
- Estimate in-plane distortion from wafer-shape changes and its effect on deck-to-deck overlay
- Combine the displacement terms into a bottom-placement budget

---

## 12.1 Differential Charging

### 12.1.1 The Mechanism

Ions arrive at the feature in a narrow cone along the axis. Electrons arrive nearly isotropically with a few electronvolts of energy, and the aspect ratio shades them: very few reach the bottom of a deep feature. Over each bias cycle, the top of the mask collects a net negative charge, while the bottom and lower walls collect a net positive charge. A potential builds up inside the feature until it repels enough of the slow ions, or attracts enough electrons, to balance the currents.

```
Region of the feature        Net charge     Consequence
──────────────────────────────────────────────────────────────────────────
Mask top and upper wall      Negative       Attracts ions sideways at the top
                                            (contributes to bow and facet)
Lower wall and bottom        Positive       Decelerates slow ions; deflects
                                            ions toward less-charged regions
```

### 12.1.2 Deflection by a Lateral Field

If the charge is not symmetric, a lateral potential difference ΔV develops across the feature near the bottom. An ion passing through a lateral field E_⊥ ≈ ΔV/w over a length L receives a transverse impulse:

```
δθ ≈ (ΔV / 2V_i) · (L / w)

V_i = ion energy / e. For L ≈ w (field region about one width tall):
  δθ ≈ ΔV / (2 V_i)

E_i = 5 keV:
  ΔV = 1 V   → δθ = 0.1 mrad
  ΔV = 4 V   → δθ = 0.4 mrad
  ΔV = 20 V  → δθ = 2.0 mrad
```

Bottom potentials in deep features can reach tens to hundreds of volts relative to the plasma. Their asymmetry is a fraction of that. **Higher ion energy reduces deflection in proportion**, which is one more reason energy has risen with aspect ratio.

### 12.1.3 What the Layered Wall Changes

The ON wall is a stack of two dielectrics with different permittivity and different leakage:

```
Property                      Oxide         Nitride
───────────────────────────────────────────────────────────
Relative permittivity          ~4            ~7
Bulk leakage under field       Very low      Higher (trap-assisted,
                                             Poole–Frenkel conduction)

Effective permittivity of the stack:
  Field in the plane of the layers (radial):     ε_∥ = φ_ox ε_ox + φ_N ε_N = 5.68
  Field across the layers (vertical):            ε_⊥ = 1/(φ_ox/ε_ox + φ_N/ε_N) = 5.26
```

The stack is a mildly anisotropic dielectric. Its permittivity contrast slightly favours radial over vertical field penetration into the wall. The more important feature is conduction. Charge spreads along the wall mostly through the fluorocarbon polymer and the ion-damaged surface layer. The nitride layers add a small, periodic leakage path. The layered wall does not dominate twisting, but it adds a pair-period modulation to the local wall potential, which feeds the small charging term in layer modulation (Chapter 10, Section 10.3.3).

### 12.1.4 Reducing Charging

```
Method                               Mechanism                           Chapter
──────────────────────────────────────────────────────────────────────────────────
Higher ion energy                    Smaller δθ for the same ΔV           6
Pulsed bias, afterglow               Electrons and negative ions enter    6
                                     during the off-time and neutralize
Tailored waveforms                   Short positive excursion each cycle  6
                                     sends electrons to the surface
Conductive wall polymer              Lateral charge spreading             4, 8
Lower pressure                       Narrower ion angle; less charge on   5
                                     upper walls
```

---

## 12.2 Twisting

### 12.2.1 A Random Walk of Direction

Twisting is the random departure of a feature's axis from vertical, different for each feature and usually growing toward the bottom. Each small deflection changes the direction in which the front advances, and later deflections add to it. Treat the direction as a random walk in steps of length ℓ, each with an independent deflection of rms σ_δθ:

```
After N = z/ℓ steps:
  Angle:         σ_θ(z) = σ_δθ √N
  Displacement:  σ_x(z) ≈ σ_δθ · ℓ · N^(3/2) / √3

Reference: ℓ = 0.5 µm, σ_δθ = 0.4 mrad (from ΔV ≈ 4 V at 5 keV), z = 8.4 µm
  N = 16.8
  σ_x = 0.0004 × 500 nm × 68.9 / 1.732 = 8.0 nm   →   3σ = 24 nm
```

The reference specification for bottom displacement is 25 nm (3σ, Chapter 1). The reference hole meets it only just.

### 12.2.2 Scaling With Depth

```
σ_x ∝ z^(3/2)

Deck height    σ_x      3σ
────────────────────────────
 8.4 µm        8.0 nm   24 nm
12.6 µm       14.6 nm   44 nm   (1.5× the height → 1.84× the twist)
```

**Twisting grows faster than depth.** A deck 50% taller nearly doubles the bottom displacement. This is the fourth per-deck limit of Chapter 1: even if time, mask, and bottom CD allowed a taller deck, the joint budget (Chapter 7) would not.

### 12.2.3 What Twist Looks Like

```
Signature                            Interpretation
──────────────────────────────────────────────────────────────────────────
Random bottom offsets, no            Charging-driven twist
 correlation between neighbours
Neighbouring holes twist together    Shared cause: local mask defect, wafer-
 (correlated)                        scale tilt, or loading at array edge
Elliptical or split bottoms          Strong late deflection; the bottom
                                     splits into two lobes
Twist larger at array edges          Asymmetric neighbourhood: charge and
                                     loading differ on one side
```

---

## 12.3 Tilt

### 12.3.1 Tilt From the Edge Sheath

At the wafer edge, the sheath boundary curves from the wafer to the edge ring. Ions accelerated across a curved boundary arrive at an angle (Chapter 9):

```
Bottom displacement from tilt = H · tan θ ≈ H · θ

θ = 0.15° = 2.62 mrad, H = 8.4 µm → 22 nm
θ = 0.25° = 4.36 mrad              → 37 nm
```

Tilt is systematic: all features at the same radius and angle tilt the same way. It can therefore be corrected by tuning the edge sheath (ring height, edge power), unlike twisting.

### 12.3.2 Tilt From an Unseated Bowed Wafer

If the wafer edge is not fully pulled down onto the chuck, the local surface is inclined to the ion direction. Features are etched along the ions, so after the wafer relaxes they are tilted relative to the wafer normal by the local slope:

```
Spherical bow, δ = 336 µm at r = 150 mm (uncompensated two decks):
  Edge slope = 2δ/r = 2 × 336×10⁻⁶ / 0.150 = 4.5 mrad = 0.26°

Partially seated edge: 50 µm gap over the last 10 mm:
  Local slope = 50 µm / 10 mm = 5.0 mrad = 0.29°
```

**A small seating error at the edge produces more tilt than the whole edge-sheath budget.** Edge tilt problems that follow incoming wafer bow (rather than ring RF-hours) point to chucking (Chapter 8, Section 8.5).

### 12.3.3 Azimuthal Tilt Patterns

A saddle-shaped wafer (after slits) seats along one axis first. Tilt then varies with angle around the edge, typically with a two-fold (cos 2φ) pattern. Edge tuning is radially symmetric and cannot correct it. The remedy is better bow control before the etch, or chucking sequences designed for saddle shapes.

---

## 12.4 Stress-Driven Distortion

### 12.4.1 In-Plane Distortion From Wafer Shape

When the stack is etched, its stress partly relaxes and the wafer bow changes. The next lithography step chucks the wafer flat, which stretches or compresses the surface in proportion to the slope that was removed:

```
In-plane displacement at the surface ≈ (t_s/2) · slope

Bow change after deck-1 hole etch: Δδ = 30 µm (illustrative)
  Δκ = 2Δδ/r² = 2 × 30×10⁻⁶ / 0.0225 = 2.67×10⁻³ m⁻¹
  Slope change at r = 150 mm: Δκ · r = 4.0×10⁻⁴
  u = (775×10⁻⁶ / 2) × 4.0×10⁻⁴ = 155 nm   (at the wafer edge, before correction)
```

Scanners correct most of this with high-order overlay models, fed by wafer-shape measurement. The residual after correction (a few nanometres, illustrative) enters the deck-joint budget as the "wafer-bow-induced distortion" term in Chapter 7 (Section 7.5.2).

### 12.4.2 Slits and Anisotropic Relaxation

Slits cut the stack into long blocks. Stress relaxes across the slits but not along them. Results:

- **Saddle-shaped wafer** (different curvature along and across the slits)
- **Block leaning**: tall, narrow blocks bend slightly toward or away from the slit, moving the tops of holes near the slit by a few nanometres
- **Distortion in later layers**: contacts and bit lines patterned after slit etch must follow the moved holes

These effects are the subject of the slit-etch companion volume. For the stack etch they matter because the stack's stress sets their size. A stress-balanced stack (Chapter 2, Section 2.4.3) reduces all of them.

---

## 12.5 The Bottom-Placement Budget

```
Term (3σ unless systematic)          Reference hole     Scaling with deck height H
──────────────────────────────────────────────────────────────────────────────────
Twisting                              24 nm              ∝ H^(3/2)
Edge tilt (after edge tuning)         ≤ 22 nm (edge)     ∝ H
Chucking-induced tilt                 0–40 nm (edge)     ∝ H × seating error
Litho overlay (to the layer below)    12 nm              Independent of H
In-plane distortion residual          8 nm               ∝ stack stress × H
```

At the wafer centre, twisting and overlay dominate. At the edge, tilt and chucking dominate. **Every term except overlay grows with deck height**, and twisting grows fastest.

---

## 12.6 Summary & Key Takeaways

1. **Electron shading charges the bottom positive.** Asymmetric charge deflects ions by δθ ≈ ΔV/(2V_i): 0.4 mrad for 4 V at 5 keV.

2. **The layered wall is a minor player in charging.** ε_∥ = 5.68 and ε_⊥ = 5.26; conduction through polymer and damaged surface dominates.

3. **Twist is a random walk.** Displacement grows as depth^(3/2): 24 nm (3σ) at 8.4 µm, 44 nm at 12.6 µm.

4. **Tilt is systematic and correctable.** Edge-sheath tilt of 0.15° gives 22 nm at the bottom and can be tuned out at the ring.

5. **Chucking can beat the edge sheath.** A 50 µm gap over 10 mm of the edge tilts features by 0.29°.

6. **Stress moves the pattern.** A 30 µm bow change gives 155 nm of uncorrected in-plane displacement at the edge; scanner correction leaves a few nanometres.

7. **The placement budget grows with height.** All terms but overlay scale with deck height.

---

## Study Questions

1. A feature has a 10 V lateral asymmetry over the last 200 nm, with w = 80 nm and 6 keV ions. Compute δθ and the resulting displacement at the bottom.

2. Using the random-walk model with ℓ = 0.4 µm and σ_δθ = 0.3 mrad, compute the 3σ twist for decks of 7, 8.4, and 10 µm.

3. The edge ring height falls 200 µm, with tilt sensitivity 0.05° per 100 µm. Compute the tilt and bottom displacement for an 8.4 µm deck. What ring lift restores it?

4. A wafer has 120 µm of residual bow after backside compensation. Compute the edge slope if it is spherical. If the edge is seated, what tilt remains from this cause?

5. Build the bottom-placement budget for a 10 µm deck by scaling each term in Section 12.5 with height. Which term grows most, and what joint pad CD would be needed with a 75 nm bottom CD?

---

**Previous Chapter:** [Chapter 11: Profile Control — Bow, Necking, Taper & Bottom CD](./11-profile-bow-taper.md)  
**Next Chapter:** [Chapter 13: Mask Selectivity, Landing & Loading Between Features](./13-mask-landing-loading.md)

---

**Chapter 12 Development Status:** Complete  
**Version:** 1.0
