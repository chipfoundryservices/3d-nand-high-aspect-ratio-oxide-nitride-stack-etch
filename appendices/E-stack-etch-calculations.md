# Appendix E: Stack-Etch Calculations

Derivations and worked calculations behind the models used in the chapters. Each section states the assumptions so that the method can be repeated with measured data.

---

## E.1 Effective Rate of a Periodic Stack

**Assumptions:** Each layer etches at its own rate; the front crosses layers in sequence; no interaction between layers.

```
Time per pair:   t_pair = d_ox/R_ox + d_N/R_N
Effective rate:  R_eff = p / t_pair = 1 / (φ_ox/R_ox + φ_N/R_N)

Sensitivity:     ∂ln R_eff / ∂ln R_i = (φ_i/R_i) / Σ_j (φ_j/R_j) = time fraction in film i
```

Worked example (reference): t_ox = 4.0 s, t_N = 5.6 s, t_pair = 9.6 s, R_eff = 312.5 nm/min, time fraction in nitride = 0.58.

**With interface transients** (rate relaxing as R(t) = R_ss[1 + (k − 1)e^(−t/τ_p)]):

```
Depth gained in a layer of duration t ≫ τ_p:  z = R_ss · t + (k − 1) τ_p R_ss
Layer time:  t_layer = (d − (k − 1) τ_p R_ss) / R_ss

Reference (τ_p = 1.5 s, k_N = 1.15, k_ox = 0.90):
  t_N  = (28 − 1.13)/5.00 = 5.38 s
  t_ox = (22 + 0.83)/5.50 = 4.15 s
  R_eff = 50 / 9.53 s = 315.0 nm/min; ρ_stack = 0.98
```

---

## E.2 ARDE Time Integral

**Assumptions:** R(A) = R₀/(1 + A/A₀) with A = z/w̄ and constant w̄.

```
dz/dt = R₀ / (1 + z/(w̄A₀))
dt = (1 + z/(w̄A₀)) dz / R₀
t(z) = (z + z²/(2w̄A₀)) / R₀  =  (w̄/R₀)(A + A²/(2A₀))
```

```
Hole: w̄ = 90 nm, R₀ = 312.5 nm/min, A₀ = 90 → w̄/R₀ = 0.288 min
  t(93) = 0.288 × (93 + 48.05) = 40.6 min

Slit: w̄ = 150 nm, A₀ = 120 → w̄/R₀ = 0.480 min
  t(56) = 0.480 × (56 + 13.07) = 33.2 min

Inverse (depth reached in time t):
  A(t) = A₀ [−1 + √(1 + 2t R₀/(w̄ A₀))]
  Hole at t = 20 min: A = 90 × (−1 + √(1 + 2 × 20 / (0.288 × 90))) = 53.5 → z = 4.8 µm
```

**Film-specific ARDE:** use R_ox(A) and R_N(A) with separate A₀ values, combine with E.1 at each A, and integrate dt = w̄ dA / R_eff(A) numerically.

---

## E.3 Neutral Transmission (Monte Carlo)

**Assumptions:** Free-molecular flow; cosine-law entry; diffuse (cosine) re-emission at every wall collision; no sticking; the bottom is an absorbing plane; the top is an open plane.

The values in Chapter 3 (Section 3.5.2) and Appendix D.5 come from a direct Monte Carlo of 10⁵ particles per case. A compact version follows:

```python
import numpy as np
rng = np.random.default_rng(1)

def cosine_dirs(n):
    u, phi = rng.random(n), 2*np.pi*rng.random(n)
    s, c = np.sqrt(u), np.sqrt(1 - u)          # sin, cos of polar angle
    return np.stack([s*np.cos(phi), s*np.sin(phi), c], 1)  # about +z

def slot(A, n=100_000):                         # width 1, depth A, infinite length
    p = np.stack([rng.random(n) - 0.5, np.zeros(n), np.zeros(n)], 1)
    d = cosine_dirs(n); alive = np.ones(n, bool); hit = np.zeros(n, bool)
    while alive.any():
        i = np.where(alive)[0]; P, D = p[i], d[i]
        tw = np.where(D[:,0] > 0, (0.5 - P[:,0]) / np.where(D[:,0] > 0, D[:,0], 1),
             np.where(D[:,0] < 0, (-0.5 - P[:,0]) / np.where(D[:,0] < 0, D[:,0], -1), np.inf))
        tt = np.where(D[:,2] < 0, -P[:,2] / np.where(D[:,2] < 0, D[:,2], -1), np.inf)
        tb = np.where(D[:,2] > 0, (A - P[:,2]) / np.where(D[:,2] > 0, D[:,2], 1), np.inf)
        tm = np.minimum(tw, np.minimum(tt, tb))
        top, bot = tt <= tm, (tb <= tm) & ~(tt <= tm)
        hit[i[bot]] = True; alive[i[top | bot]] = False
        w = ~(top | bot); j = i[w]
        if j.size == 0: continue
        Pn = P[w] + tm[w, None] * D[w]
        loc = cosine_dirs(j.size); sgn = -np.sign(Pn[:,0])  # inward wall normal
        d[j] = np.stack([loc[:,2]*sgn, loc[:,1], loc[:,0]], 1); p[j] = Pn
    return hit.mean()
```

The round-hole version uses the same loop with a cylinder intersection and a local frame built on the inward radial normal.

```
Results (10⁵ particles each; statistical error ≈ ±0.0005 at W = 0.05):

  A      W_hole (MC)   1/(1 + 3A/4)   W_slot (MC)   (ln A + 0.1)/A
─────────────────────────────────────────────────────────────────────
  20     0.059          0.063           0.156         0.155
  42     0.030          0.031           0.091         0.091
  56     0.023          0.023           0.074         0.074
  93     0.014          0.014           0.050         0.050
```

The hole results agree with the long-tube Clausing form. The slot fit (ln A + 0.1)/A is an empirical fit to these results over A = 20–93 and should not be extrapolated far outside that range.

---

## E.4 Ion Pass Fraction and Required Energy

```
σ_θ = √(T_⊥/E),  θ_c = 1/A

Round hole:  f = 1 − exp(−θ_c²/(2σ_θ²)) = 1 − exp(−E/(2T_⊥A²))
             E_req = 2 T_⊥ A² ln[1/(1 − f)]
Slot:        f = erf(θ_c/(σ_θ√2))
             E_req = 2 T_⊥ A² [erf⁻¹(f)]²
```

**IED averaging (arcsine distribution):** with E(φ) = V̄ + V₁ sin φ and φ uniform, f̄ = ⟨1 − exp(−E(φ)/(2T_⊥A²))⟩. For V̄ = 5 kV, V₁ = 4.5 kV, A = 93, T_⊥ = 0.5 eV: f̄ = 0.40 versus 0.44 for a monoenergetic beam.

**Product generation per hole (top):** hole top area 8.66×10⁻¹¹ cm² × 312.5 nm/min = 4.51×10⁻¹⁷ cm³/s; mean Si density 0.44 × 2.21×10²² + 0.56 × 3.60×10²² = 2.99×10²² cm⁻³ → 1.3×10⁶ Si atoms/s.

---

## E.5 Stoney Bow and Stress Balance

```
σ_stack = φ_ox σ_ox + φ_N σ_N = 0.44(−200) + 0.56(+100) = −32 MPa

κ = 6 σ_f t_f / (M_s t_s²);  δ = κ r²/2
  t_f = 8.4 µm: κ = 0.0149 m⁻¹, δ = 168 µm
  t_f = 16.8 µm: δ = 336 µm

Balancing nitride stress: σ_N = −φ_ox σ_ox / φ_N = +157 MPa
```

---

## E.6 Plate Flattening and Electrostatic Clamping

```
Uniform pressure to deflect a simply supported plate by δ at the centre:
  q = δ · 64 D (1 + ν) / [a⁴ (5 + ν)],   D = E t³ / [12(1 − ν²)]
  E = 130 GPa, ν = 0.28, t = 775 µm, a = 150 mm → D = 5.47 N·m
  δ = 336 µm → q = 56 Pa

Coulomb clamping across a gap g:
  P(g) = ε₀ V² / [2 (g + d/ε_r)²]
  V = 2 kV, d/ε_r = 30 µm: P(5 µm) = 14.5 kPa; P(336 µm) = 132 Pa; P(600 µm) = 45 Pa
Crossover (P = q(δ)) ≈ 450 µm
```

---

## E.7 Twist as a Random Walk of Direction

**Assumptions:** The feature advances in steps of length ℓ; each step adds an independent angular deflection with rms σ_δθ; angles are small.

```
Angle after n steps:          θ_n = Σ_{i≤n} δθ_i → Var(θ_n) = n σ_δθ²
Displacement after N steps:   x_N = ℓ Σ_{n=1..N} θ_n
Var(x_N) = ℓ² σ_δθ² Σ_n Σ_m min(n, m) = ℓ² σ_δθ² N(N + 1)(2N + 1)/6 ≈ ℓ² σ_δθ² N³/3

σ_x ≈ σ_δθ ℓ N^(3/2) / √3

Reference: ℓ = 0.5 µm, σ_δθ = 0.4 mrad, N = 16.8 → σ_x = 8.0 nm (3σ = 24 nm)

Deflection from a lateral field (impulse approximation):
  δθ ≈ (ΔV / 2V_i)(L/w);  L ≈ w → δθ ≈ ΔV/(2V_i)
  ΔV = 4 V, V_i = 5 kV → 0.4 mrad
```

---

## E.8 OES Pair-Signal Damping

**Assumptions:** The single-front signal is periodic in depth with period p; front depths across the wafer are Gaussian with standard deviation σ_z.

```
Fundamental component of the summed signal:
  S₁ ∝ ∫ e^(i 2π z/p) N(z; z̄, σ_z) dz = e^(i 2π z̄/p) · exp(−2π² σ_z²/p²)

M = exp(−2π² σ_z²/p²)

M = 1/e when σ_z = p/(π√2) = 0.225 p
  p = 50 nm → σ_z = 11.3 nm; with σ_z = 0.015 z → z = 750 nm
  p = 40 nm → σ_z = 9.0 nm  → z = 600 nm
```

---

## E.9 Overetch, Recess, and Feed-Forward

```
Overetch = systematic spread + n_σ · σ_random · t_ME
  n_σ for a per-feature miss probability P: n_σ ≈ Φ⁻¹(1 − P)
  P = 10⁻¹² → n_σ ≈ 7.0

Recess_max = t_OE · R_bottom / S

Feed-forward from stack thickness (ARDE):
  Δt = ΔH / R(A_end)  (not ΔH/R_avg)
  ΔH = 84 nm, R(A_end) = 153.7 nm/min → Δt = 0.55 min (1.35%)
```

---

## E.10 Per-Deck Limits

```
Time:       solve (w̄/R₀)(A + A²/2A₀) = t_max                      → A_max, H = A_max w̄
Mask:       r_m (t + t_OE)(1 + e_edge) + T_min ≤ T_mask             → t_max → H
Bottom CD:  CD_top − 2α₁z₁ − 2α₂(H − z₁) ≥ CD_min                 → H
Twist:      3 σ_δθ ℓ (H/ℓ)^(3/2)/√3 ≤ budget                       → H

Reference results: mask 8.0 µm, twist 8.7 µm, time 9.0 µm, bottom CD 9.2 µm
```

---

## E.11 Cost per Chamber-Minute and Chamber Count

```
Cost/min = Capex / (years × 525,600 × uptime) + consumables per pass / etch minutes
  $5.0M, 5 yr, 85% → $2.24/min; consumables $34.3 / 45.1 min = $0.76/min → $3.0/min

Chambers = WSPM × chamber-minutes per wafer / (60 × 730 × uptime)
  50,000 × 220 / (60 × 620.5) ≈ 296
```

---

**Appendix E Version:** 1.0  
**Last Updated:** 2026-10-04
