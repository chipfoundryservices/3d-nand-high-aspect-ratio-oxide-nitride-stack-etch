# Appendix D: Process Windows & Lookup Tables

Lookup tables for the reference process and representative process windows. All values are illustrative and are given so that calculations in the chapters can be repeated quickly.

---

## D.1 Effective Rate vs. Rate Ratio (φ_ox = 0.44, R_ox = 330 nm/min)

```
ρ       R_N (nm/min)   R_eff (harmonic)   Arithmetic mean   Time in nitride
──────────────────────────────────────────────────────────────────────────────
1.00     330            330.0               330.0             56%
0.95     313.5          320.6               320.8             57%
0.91     300            312.5               313.2             58%
0.85     280.5          300.3               302.3             60%
0.80     264            289.5               293.0             61%
0.70     231            266.1               274.6             65%
0.60     198            240.3               256.1             68%
0.50     165            211.5               237.6             72%
```

---

## D.2 Rate and Time vs. Depth (Reference Hole: w̄ = 90 nm, A₀ = 90)

```
Depth (µm)   A      R (nm/min)   t (min)   Pair time (s)
─────────────────────────────────────────────────────────
 0.0          0      312.5         0.0       9.6
 1.0         11      278.2         3.4      10.8
 2.0         22      250.6         7.2      12.0
 3.0         33      228.0        11.4      13.2
 4.0         44      209.2        16.0      14.3
 5.0         56      193.2        20.9      15.5
 6.0         67      179.5        26.3      16.7
 7.0         78      167.6        32.1      17.9
 8.0         89      157.2        38.2      19.1
 8.4         93      153.7        40.6      19.5

(A computed as depth/w̄; the 8.4 µm row uses the rounded reference A = 93.)
```

---

## D.3 Rate and Time vs. Depth (Reference Slit: w̄ = 150 nm, A₀ = 120)

```
Depth (µm)   A      R (nm/min)   t (min)
───────────────────────────────────────────
 0.0          0      312.5         0.0
 2.0         13      281.2         6.8
 4.0         27      255.7        14.2
 6.0         40      234.4        22.4
 8.4         56      213.1        33.2
```

---

## D.4 Ion Pass Fraction (T_⊥ = 0.5 eV)

```
Round hole: f = 1 − exp(−E / (2 T_⊥ A²))

E (keV)    A = 56    A = 80    A = 93    A = 120   A = 150
───────────────────────────────────────────────────────────
  2         0.47      0.27      0.21      0.13      0.09
  3         0.62      0.37      0.29      0.19      0.12
  5         0.80      0.54      0.44      0.29      0.20
  8         0.92      0.71      0.60      0.43      0.30
 10         0.96      0.79      0.69      0.50      0.36
 15         0.99      0.90      0.82      0.65      0.49

Slot (1D): f = erf(θ_c / (σ_θ √2)),  θ_c = 1/A, σ_θ = √(T_⊥/E)

E (keV)    A = 40    A = 56    A = 80
──────────────────────────────────────
  2         0.89      0.74      0.57
  5         0.99      0.93      0.79
 10         1.00      0.99      0.92
```

---

## D.5 Neutral Transmission (Diffuse Walls, No Sticking)

```
A       Round hole W   Slot W    Ratio
───────────────────────────────────────
 20      0.059          0.156     2.6
 42      0.030          0.091     3.1
 56      0.023          0.074     3.2
 80      0.016          0.056     3.4
 93      0.014          0.050     3.6
```

(Monte Carlo, Appendix E.3. A = 80 values interpolated from the fits W_hole ≈ 1/(1 + 3A/4) and W_slot ≈ (ln A + 0.1)/A.)

---

## D.6 Reference Recipe Window (Illustrative)

```
Parameter            ME-1          ME-2          ME-3          LS
───────────────────────────────────────────────────────────────────────────
Pressure (mTorr)     15–25         15–25         10–20         15–25
Source (kW)          2.5–3.5       2.5–3.5       2.5–3.5       2.0–3.0
Bias (kW)            6–10          10–14         13–18         6–10
Energy (keV)         2.5–3.5       4–5           5–7           3–4
C₄F₆ (sccm)          35–55         30–50         20–40         40–60
CH₂F₂ (sccm)         15–25         20–30         28–42         0–5
O₂ (sccm)            25–35         30–40         25–35         10–20
NF₃ (sccm)           0–3           3–8           6–14          0
ρ_stack target       0.88–1.02     0.88–1.02     0.88–1.02     —
Chuck (°C)           10–30         10–30         10–30         10–30
```

---

## D.7 Specification Summary (Reference Hole)

```
Item                       Target / limit
──────────────────────────────────────────────
Landing recess             ≤ 30 nm
Top CD                     105 ± 3 nm (3σ)
Max CD (bow)               ≤ 115 nm
Bottom CD                  ≥ 70 nm
Layer modulation (etch)    ≤ 2 nm p-v
Bottom displacement        ≤ 25 nm (3σ twist)
Edge tilt                  ≤ 0.15° at 3 mm
Remaining mask             ≥ 300 nm at edge
Depth uniformity           3σ ≤ 3% before landing
Joint offset allowance     22.5 nm
```

---

## D.8 Per-Deck Limits (Reference Process)

```
Constraint      H_max (µm)   Main lever to raise it
─────────────────────────────────────────────────────────────────
Mask (edge)      8.0          Mask selectivity, less OE
Twist            8.7          Ion energy, charge relief
Time (45 min)    9.0          R₀, A₀ (cryo, pulsing)
Bottom CD        9.2          Lower-zone taper, ρ at depth
```

---

## D.9 Overetch and Recess

```
Random arrival σ (% of t)   7σ tail (min)   + systematic 1.2 min   Recess at S = 20
───────────────────────────────────────────────────────────────────────────────────
0.5%                         1.4             2.6 min                20 nm
0.7%                         2.0             3.2 min                25 nm
1.0% (ref.)                  2.8             4.0 min                31 nm
1.5%                         4.3             5.5 min                42 nm
```

---

## D.10 Twist vs. Deck Height (ℓ = 0.5 µm, σ_δθ = 0.4 mrad)

```
H (µm)    σ_x (nm)   3σ (nm)
────────────────────────────
 6.0       4.8        14
 7.0       6.0        18
 8.4       8.0        24
10.0      10.3        31
12.0      13.6        41
```

---

**Appendix D Version:** 1.0  
**Last Updated:** 2026-10-04
