# Spotify_analyze
Product-Analytics Mini Project — Spotify Listening Data

This repo contains a compact, reproducible analysis pipeline built around a public “Spotify songs” dataset.
It cleans raw records, runs EDA, derives product metrics, and demonstrates a lightweight A/B-testing workflow for two concrete hypotheses about ranking and content length.

**Data prep**: schema harmonization, type fixes, de-duplication, removal of obvious outliers, handling missing values.
**Inputs (examples in `data/`):**
- `jla_mub_synth.csv`: `z, mu_obs, sigma_mu`
- `hz_synth.csv`: `z, H_obs, sigma_H` (km/s/Mpc)
- `bao_synth.csv`: `z, Dv_over_rd, sigma` (dimensionless)в

**EDA (notebook):**
- `Popularity by release year (mean/median) with yearly volume plot to avoid sample-size bias`;
- `Track count by year; average duration by era (<1980 / 1980–2009 / 2010+)`;
- `Mode (major/minor) distribution by genre; valence heat-map (genre × mood bins)`;
- `Hit analysis (popularity≥70) by genre/subgenre across eras (60–80, 80–90, 90–00, 00–10, 10–20)`.

**Metrics** used in tests: average listened time, completion rate (CNR = listened_ms / duration_ms), early-skip rate (<30s), hit-share.

**Hypotheses under test**
G1: “Placing tracks in top editorial slots (1–5) inflates engagement vs slots 6–10.”
G2: “Among top-slot items, very long tracks (>4 min) increase early-skip rate.”

**Experiment design (simulated)**: random user-level assignment to control/treatment, optional stratification by historical popularity/era; power check; A/A sanity.
Inference: Welch’s t-test and Mann–Whitney U; non-parametric bootstrap CIs; Benjamini–Hochberg FDR; optional CUPED for variance reduction.

**Outputs**: clear plots, per-metric test tables (effect size, CI, p-values, power), and brief interpretation cells ready for a report.

**Stack**: Python (pandas, NumPy, SciPy, statsmodels, scikit-learn for stratification & bootstrap), matplotlib / seaborn, Jupyter.
Everything runs from the notebook; no external services required.
