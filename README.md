# SAPM Monte Carlo — Plastics / Thermodynamic Degradation Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Plastics (Thermodynamic Degradation Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **6.67** |
| β_W mean | 6.98 |
| β_W std | 2.08 |
| **90% CI** | **[4.2, 10.8]** |
| 99% CI | [3.5, 13.3] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$4,332.7B/yr** |
| Π (revenue) | $650.0B/yr |

**β_W = 6.67** means the plastics industry destroys **$6.67 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-plastics.git
cd sapm-mc-plastics
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 6.67` and `ΔW median : $4,332.7B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_health_microplastics | $1,496.5B | [$746.3B, $2,992.2B] | Lognormal |
| C2_climate_ghg | $224.9B | [$149.7B, $300.5B] | Normal |
| C3_ocean_ecosystem | $1,498.9B | [$726.2B, $3,097.2B] | Lognormal |
| C4_waste_management | $120.1B | [$71.9B, $199.7B] | Lognormal |
| C5_environmental_justice | $349.1B | [$188.9B, $646.9B] | Lognormal |
| C6_governance_capture | $499.5B | [$312.8B, $799.9B] | Lognormal |
| **Total ΔW** | **$4,332.7B** | **[$2,727.4B, $7,046.3B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.1820%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Plastics (Thermodynamic Degradation Floor)*.
> GitHub: epostnieks/sapm-mc-plastics.
> https://github.com/epostnieks/sapm-mc-plastics
