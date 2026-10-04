# Appendix B: Chemistry & Reaction Data

Reaction pathways, model parameters, and optical-emission data for ON-stack etch. Kinetic and sensitivity values are representative; extract your own from stack measurements in your chamber (Appendix C).

---

## B.1 Net Etch Reactions

### B.1.1 Silicon Dioxide

```
SiO₂ + 2 CF₂ (ads) + ions        → SiF₄ + 2 CO
SiO₂ + CF₄-type F supply + ions  → SiF₄ + CO₂ / COF₂
SiO₂ + 4 HF (ads, cryo) + ions   → SiF₄ + 2 H₂O
```

Oxygen leaves with carbon, so the oxide consumes polymer at the front.

### B.1.2 Silicon Nitride

```
Si₃N₄ + CF_x + H + ions          → SiF₄ + HCN / FCN / N₂
Si₃N₄ + F (radical) + ions       → SiF₄ + N₂ / NF_x (minor)
Si₃N₄ + 16 HF (cryo, no ions)    → 3 SiF₄ + 4 NH₄F  →  (NH₄)₂SiF₆ (solid, ammonium
                                                       fluorosilicate) on the surface
```

Ammonium fluorosilicate sublimes at about 100 °C and above. At cryogenic wafer temperatures it must be removed by ion bombardment (Chapter 4, Section 4.6.3).

### B.1.3 Mask (Amorphous Carbon)

```
C + O → CO          (O₂, oxide-released O)
C + 2F → CF₂ ...    (F-rich mixtures; NF₃)
C + ions → sputtered C (physical)
```

### B.1.4 Landing Materials

```
Poly-Si + F → SiF₄            (slow under heavy fluorocarbon polymer)
W + 6F → WF₆ (volatile)       (suppressed by polymer; avoid F-rich mixes)
Al₂O₃ + F → AlF₃ (involatile) (very high selectivity stop)
```

---

## B.2 Polymer-Thickness Etch Model

```
R = R_bare · exp(−T_p / λ_p)

Parameter                     Oxide            Nitride
─────────────────────────────────────────────────────────
Steady-state T_p (HAR ME)     1.0–2.0 nm       1.5–3.0 nm
λ_p                           1–2 nm           1–2 nm
```

Interface transient (Chapter 3, Section 3.3), illustrative:

```
τ_p (top of feature)          1.5 s
k entering nitride            1.15
k entering oxide              0.90
Extra depth per interface     (k − 1) · τ_p · R_ss
```

---

## B.3 Rate-Matching Matrix (Illustrative)

Per +10% of each gas's reference flow (or of bias power):

```
Knob          ΔR_ox     ΔR_N     ΔR_mask
─────────────────────────────────────────
C₄F₆           −1%       −3%      −4%
CH₂F₂           0%       +4%      −1%
O₂             +1%       +4%      +6%
NF₃            +2%       +3%      +3%
Bias power     +4%       +4%      +5%
```

Temperature (conventional range, per +1 K): R_ox +0.10%, R_N +0.25%, ρ +0.0014, bow +0.3 nm, mask erosion +0.2%.

---

## B.4 Effective Rate and ARDE

```
R_eff = 1 / (φ_ox/R_ox + φ_N/R_N)

R_eff(A) = R_eff,0 / (1 + A/A₀)
  A₀ = 90 (round hole), 120 (slit), reference R_eff,0 = 312.5 nm/min

Film-specific ARDE (illustrative): A₀,ox = 100, A₀,N = 82
  ρ(A) = 0.909 × (1 + A/100) / (1 + A/82)

  A      ρ
───────────
  0     0.91
 30     0.87
 60     0.84
 93     0.82
```

---

## B.5 Adsorption Data

```
Langmuir:  θ = Kp/(1 + Kp),   K ∝ exp(E_ads / k_B T)

d ln K/dT = −E_ads / (k_B T²)

E_ads (eV)   T = 293 K    T = 243 K    T = 213 K       (per K)
──────────────────────────────────────────────────────────────
0.25          −3.4%        −4.9%        −6.4%
0.35          −4.7%        −6.9%        −9.0%
0.45          −6.1%        −8.8%        −11.5%

K(213 K)/K(293 K) for E_ads = 0.35 eV: ≈ 180
```

---

## B.6 Sticking and Wall Loss

```
Species              Wall-loss probability s     Decay length λ = w̄/√(3s)
                     (polymer-covered wall)      at w̄ = 90 nm
──────────────────────────────────────────────────────────────────────────
F                    0.01–0.1                    165–520 nm
CF₂                  0.01–0.05                   230–520 nm
CF, C₂F₄ fragments   0.05–0.3                    95–230 nm
O                    0.01–0.1                    165–520 nm
HF (cold surfaces)   adsorbs reversibly;         surface transport; effective
                     s_eff ~10⁻⁴–10⁻³            λ 1.6–5.2 µm
O₂, N₂, Ar           ~0                          Clausing-limited only
```

---

## B.7 Optical Emission Lines

```
Species   Wavelength (nm)          Source in ON etch         Use
───────────────────────────────────────────────────────────────────────────────
CO        451, 483, 520 (Å bands)  Oxide etch, mask          Oxide/mask products
O         777, 845                 O₂ feed, oxide            Polymer balance
CN        388                      Nitride etch              Nitride front;
                                                             pair-frequency signal
N₂        337                      Nitride etch              Nitride front
SiF       440                      Si-containing etch        Landing transition
F         704                      Free fluorine             Actinometry vs. Ar 750
CF₂       250–320 (bands)          Fluorocarbon feed         Polymer precursor
H         656 (Hα)                 HFC, H₂, nitride H        Hydrogen balance
Ar        750, 811                 Diluent                   Actinometer
```

---

## B.8 Product Budget (Reference, Bottom of Hole Etch)

```
Si atoms removed at feature bottoms     7.0×10¹⁷ s⁻¹
C atoms removed from the mask           3.6×10¹⁸ s⁻¹
Feed gas throughput (300 sccm)          1.3×10²⁰ s⁻¹
SiF₄ fraction of gas throughput         ≈ 0.5%
```

---

**Appendix B Version:** 1.0  
**Last Updated:** 2026-10-04
