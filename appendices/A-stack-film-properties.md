# Appendix A: Stack Film, Mask & Gas Properties

Reference properties of the materials in an ON-stack etch. Values are representative of PECVD stack films and common HAR process materials. Where a range is given, the reference value used in this book is listed separately. Measure the actual films in your process before using these numbers quantitatively.

---

## A.1 Stack Oxide (PECVD SiO₂)

```
Property                          Range                  Reference value
─────────────────────────────────────────────────────────────────────────────
Thickness per layer               18–30 nm               22 nm
Density                           2.15–2.25 g/cm³        2.20 g/cm³
Refractive index (633 nm)         1.45–1.47              1.46
Hydrogen content                  1–5 at% (Si–OH, H₂O)   3 at%
Dielectric constant               4.0–4.2                4.0
Film stress                       −100 to −300 MPa       −200 MPa (compressive)
Wet etch rate, 100:1 HF           3–6× thermal oxide     10 nm/min (4× thermal)
Atom density                      —                      6.6×10²² cm⁻³
Si density                        —                      2.21×10²² cm⁻³
Thermal conductivity              1.0–1.4 W/m·K          1.2 W/m·K
Open-area etch rate (ref. ME)     —                      330 nm/min
```

---

## A.2 Stack Nitride (PECVD Si₃N₄ / SiN_x:H)

```
Property                          Range                  Reference value
─────────────────────────────────────────────────────────────────────────────
Thickness per layer               22–35 nm               28 nm
Density                           2.5–2.85 g/cm³         2.80 g/cm³
Refractive index (633 nm)         1.90–2.05              1.98
Hydrogen content                  12–25 at% (Si–H, N–H)  18 at%
Si/N ratio                        0.75–0.90              0.80
Dielectric constant               6.5–7.5                7.0
Film stress                       −300 to +400 MPa       +100 MPa (tensile)
                                  (tunable)
Wet etch rate, 100:1 HF           1–3× LPCVD nitride     0.7 nm/min
Hot H₃PO₄ etch rate (160 °C)      3–8 nm/min             5 nm/min
Atom density                      —                      8.4×10²² cm⁻³
Si density                        —                      3.60×10²² cm⁻³
Thermal conductivity              1.5–3 W/m·K            2 W/m·K
Open-area etch rate (ref. ME)     —                      300 nm/min
```

### A.2.1 Composition Sensitivities (Illustrative)

```
∂R_N/∂[H]      ≈ +1.5% per at% H
∂R_N/∂ρ        ≈ −1.2% per 0.01 g/cm³
Stress vs. [H] Lower H (denser) → more tensile
FTIR markers   Si–H stretch ~2170 cm⁻¹; N–H stretch ~3350 cm⁻¹
```

---

## A.3 Stack-Level Reference Values

```
Pair pitch p                       50 nm
Oxide fraction φ_ox                0.44
Nitride fraction φ_N               0.56
Pairs per deck                     160
Deck height H_deck                 8.4 µm (8.0 µm of pairs + 0.4 µm overhead)
Total ON stack (2 decks + IDL)     ≈ 17.2 µm
Effective open-area rate R_eff,0   312.5 nm/min (harmonic mean)
Rate ratio ρ (blanket)             0.91
Net stack stress                   −32 MPa
Effective permittivity ε_∥ / ε_⊥    5.68 / 5.26
Wafer bow (Stoney, 775 µm Si)      168 µm per deck, 336 µm for two decks
                                   (uncompensated)
```

---

## A.4 Non-Periodic Layers

```
Layer                     Material                 Thickness (ref.)   Notes
──────────────────────────────────────────────────────────────────────────────────────
Cap oxide                 PECVD/TEOS SiO₂          200 nm             Faster than stack
Inter-deck layer (IDL)    SiO₂ (or SiO₂/poly)      400 nm             Joint region
Bottom buffer             SiO₂                     50 nm              —
Landing layer (holes)     Doped poly-Si            ≥ 60 nm            S ≈ 20 in LS step
Source stack (slits)      Poly / oxide / nitride / 150–300 nm         Replacement source
                          poly                                         variants
TAC landing pad           W (or Cu)                —                  S ≈ 20–50
```

---

## A.5 Hard Mask Materials

```
Material                  Density (g/cm³)  Stress (MPa)    Relative erosion   Notes
                                                           (a-C = 1.0)
──────────────────────────────────────────────────────────────────────────────────────────
Amorphous carbon (a-C)    1.6–1.9          −100 to −400    1.0                Reference;
                                                                              2.4 µm
High-density a-C          1.9–2.1          −300 to −800    0.75–0.9           Opaque;
                                                                              alignment
Boron-doped carbon        1.9–2.2          −500 to −1000   0.5–0.7            Strip
                                                                              chemistry
SiON cap                  2.0–2.3          —               —                  50 nm;
                                                                              litho/ARC
Atom density (a-C ref.)   ~9×10²² C/cm³
Reference erosion         45 nm/min in main etch
```

---

## A.6 Process Gases

```
Gas      M (g/mol)   Role in ON etch                            Notes
──────────────────────────────────────────────────────────────────────────────────
C₄F₆     162.0       Polymerizer; mask and wall protection      Low F/C (1.5)
C₄F₈     200.0       Polymerizer (weaker than C₄F₆)             F/C 2.0
CH₂F₂     52.0       H source; raises nitride rate              Hydrofluorocarbon
CHF₃      70.0       F and H source                             F/C 3.0
CF₄       88.0       F source                                   F/C 4.0
O₂        32.0       Polymer removal; raises ρ                  Erodes a-C
NF₃       71.0       F source; declogging                       Erodes a-C
Ar        39.9       Diluent; ion flux                          Actinometer
HF        20.0       Etchant in cryogenic chemistry             Adsorbs on cold
                                                                surfaces
H₂         2.0       H source                                   Forms HF in situ
He         4.0       Backside cooling                           Not a process gas
```

---

## A.7 Ion and Plasma Reference Values

```
Mean ion energy (ref.)                5 keV
Transverse temperature T_⊥            0.5 eV → σ_θ = 10 mrad
Ion power to the wafer                4.0 kW (of 12 kW bias)
Ion current                           0.80 A (1.13 mA/cm²)
Ion flux                              7.1×10¹⁵ cm⁻² s⁻¹
Heat flux (total)                     6.3 W/cm²
Electron density at sheath edge       5×10¹⁰ cm⁻³
Electron temperature                  3 eV
Sheath thickness (4 kV)               ≈ 10 mm
Gas density at 20 mTorr, 300 K        6.4×10¹⁴ cm⁻³
Residence time                        14 ms (300 sccm, 2.7 L)
```

---

## A.8 Substrate and Chuck

```
Silicon wafer thickness              775 µm
Biaxial modulus Si(100)              180 GPa
Young's modulus / Poisson (plate)    130 GPa / 0.28
Flexural rigidity D                  5.47 N·m
Si thermal conductivity              130 W/m·K (300 K)
Si ρc                                1.63 MJ/m³·K (ρ 2330 kg/m³, c 700 J/kg·K)
Backside He (20 Torr) conductance    ≈ 2,500 W/m²·K (illustrative)
ESC ceramic                          Al₂O₃ / AlN, ~30 W/m·K
Wafer thermal time constant          ≈ 0.5 s
```

---

**Appendix A Version:** 1.0  
**Last Updated:** 2026-10-04
