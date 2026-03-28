# Measuring Orbital and Spin Periods of a Cataclysmic Variable Star
### Time-Series Analysis & Spectral Estimation | Durham University AstroLab

---

## Overview

End-to-end quantitative analysis of optical photometry data from the Durham University rooftop telescopes, recovering two independent periodic signals from an astrophysical binary system (MU Camelopardalis) and validating the results against published literature values.

Both the orbital period (**4.722 ± 0.053 hr**) and white dwarf spin period (**1186.8 ± 0.7 s**) were recovered to within **0.3σ** of accepted values from a 1.36-day observational baseline.

---

## Technical Skills

- **Spectral estimation** — Lomb-Scargle periodogram applied to unevenly sampled time-series data; two-pass frequency grid strategy (broad survey → precision zoom) with 10,000-point resolution
- **Monte Carlo methods** — Bootstrap resampling (N = 3,000 iterations) for non-parametric uncertainty quantification on peak frequency estimates
- **Statistical inference** — False alarm probability (FAP) thresholds via the Baluev analytical approximation; Gaussian validation of bootstrap distributions; σ-discrepancy quantification against literature
- **Signal processing** — Nyquist frequency limits, frequency resolution theory (Δf ≈ 1/T), alias identification and verification from inter-observation gaps
- **Error propagation** — Full analytical chain: Poisson photon-noise → magnitude uncertainty → flux uncertainty → frequency uncertainty → period uncertainty via first-order Taylor expansion
- **Data pipeline** — Aperture photometry (AstroImageJ), magnitude-to-flux conversion, multi-telescope dataset combination with consistent Nyquist constraints
- **Python** — `astropy`, `numpy`, `pandas`, `matplotlib`, `scipy.stats`; publication-quality figure production

---

## Why This Matters for Quantitative Finance

The core methods here map directly onto quantitative research problems:

| Astrophysics | Finance Equivalent |
|---|---|
| Lomb-Scargle periodogram on irregular data | Spectral analysis of irregularly sampled financial time series |
| Bootstrap uncertainty on peak frequency | Non-parametric confidence intervals on strategy parameters |
| False alarm probability threshold | Statistical significance testing to avoid overfitting |
| Alias detection from data gaps | Spurious signal identification in noisy market data |
| Two-pass frequency search | Coarse-to-fine hyperparameter search |

---

## Repository Structure

```
├── lombscargle_final.ipynb   # Full analysis notebook
├── DATACOMBO.dat             # Combined East-16 + Draco-2 photometry dataset
├── figures/
│   ├── fig1_lightcurve.pdf
│   ├── fig2_periodogram.pdf
│   └── fig3_bootstrap_histograms.pdf
├── results_figures.py        # Publication-quality figure generation
└── Cataclysmic_Variables.pdf # Full lab report
```

---

## Robustness & Validation

Every analytical decision was stress-tested:

**Signal validity** — Both detected peaks exceed the 1% FAP threshold by a large margin, ruling out noise as the source. Reference star light curves showed no correlated variability, confirming the signals are intrinsic to the target.

**Alias verification** — The 22-hour inter-night gap creates alias frequencies at f₀ ± 1.08 cycles/day. Both the orbital and spin peaks were explicitly checked against their expected alias positions — no coincidences found.

**Uncertainty method** — Standard peak-width uncertainty is bounded below by the frequency resolution (~0.74 cycles/day regardless of signal strength). The bootstrap instead measures how much the peak actually moves under resampling, yielding σ_orb = 0.057 and σ_spin = 0.045 cycles/day — both finer than the resolution limit, consistent with high signal-to-noise centroid localisation.

**Dataset selection** — The 2022 datasets were excluded not arbitrarily, but because a 3-year temporal gap would place alias frequencies at f₀ ± 0.001 cycles/day, making real and spurious peaks indistinguishable. This is documented and quantified in the report.

**Consistency check** — The measured Pspin/Porb ratio of 0.070 falls within the 0.01–0.1 range typical of intermediate polars in the Ritter & Kolb catalogue, providing an independent physical sanity check on both results.

---

## Key Lessons

- **Irregular sampling is not a problem to eliminate — it is a property to model correctly.** The Lomb-Scargle method handles gaps analytically; interpolation or imputation would introduce artificial frequencies.
- **Uncertainty quantification requires understanding your estimator.** The bootstrap was chosen over peak-width methods because the latter conflates frequency resolution with measurement precision — a subtle but important distinction.
- **Every detected signal needs a null hypothesis test.** FAP thresholds and alias checks are not optional steps — without them, a peak is not a result.
- **Combining datasets requires consistency in the sampling properties**, not just the signal. Mixing exposure times changes the Nyquist limit and contaminates the power spectrum in ways that are hard to diagnose after the fact.

---

## Results Summary

| Quantity | Measured | Literature | Discrepancy |
|---|---|---|---|
| f_orb (cycles/day) | 5.082 ± 0.057 | 5.099 | 0.30σ |
| P_orb (hr) | 4.722 ± 0.053 | 4.707 | 0.29σ |
| f_spin (cycles/day) | 72.798 ± 0.045 | 72.789 | 0.22σ |
| P_spin (s) | 1186.8 ± 0.7 | 1187 | 0.01σ |

---

*Durham University — L2 Lab Skills & Electronics — 2026*
