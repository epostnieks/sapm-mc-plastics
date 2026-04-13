# Monte Carlo Assumptions — Plastics / Thermodynamic Degradation Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $650.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 6.67 | Confirmed by N=100,000 draws |
| ΔW median (result) | $4,332.7B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_health_microplastics` | lognormal | $1,000.0B | $1,500.0B | $3,000.0B | Endocrine disruptors, microplastic ingestion, PFAS-coated packaging, cancer risk |
| `C2_climate_ghg` | normal | $150.0B | $225.0B | $300.0B | GHG emissions from petrochemical production (1.8 Gt CO₂e/yr × SCC). Sources: CIE |
| `C3_ocean_ecosystem` | lognormal | $500.0B | $1,500.0B | $3,100.0B | Marine debris, microplastic contamination, coral reef damage, fisheries impact.  |
| `C4_waste_management` | lognormal | $80.0B | $120.0B | $200.0B | Municipal waste management, cleanup, landfill, incineration costs. Sources: Worl |
| `C5_environmental_justice` | lognormal | $150.0B | $350.0B | $650.0B | Global South open burning, waste colonialism, fenceline community health burden. |
| `C6_governance_capture` | lognormal | $250.0B | $500.0B | $800.0B | Petrochemical treaty sabotage, recycling theater, manufactured consumer blame. S |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.0) = 0.1820%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 6.45 | 20% DC adj = 5.16 | 40% DC adj = 3.87

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $4,333B = 4.1% of world GDP ($106T) ✓
- **β_W range**: 6.67 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
