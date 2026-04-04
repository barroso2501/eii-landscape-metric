# Analysis Roadmap — Edge Interception Index (EII) Paper
## Ordered sequence of analyses, inputs, outputs, and dependencies

**Status:** Active planning document  
**Last updated:** 2026-04-02 (rev. 3 — Phases 1 and 2 complete; results recorded)

---

## Finalized configuration decisions

| Parameter | Decision |
|---|---|
| Study domain | Rectangle 1,500 × 1,500 km, ESRI:102033 (Albers Equal Area Conic) |
| Domain corners | SW (200,000; 1,700,000) m — NE (1,700,000; 3,200,000) m |
| Primary grid | Hexagonal, 20,000 ha (~15.2 km side), 11,500 cells |
| Scale sensitivity | 10,000 ha (22,842 cells) / 20,000 ha / 40,000 ha (5,822 cells) |
| Shape sensitivity | Square, 20,000 ha (11,449 cells) |
| Border cells | None — all cells fully contained within rectangular domain |
| CRS | ESRI:102033 throughout |
| Nodata handling | nodata=255 hardcoded for both EII and Area (raster metadata declares nodata=0, which is valid non-natural vegetation data) |

---

## Overview

Four sequential phases. Phases 1 and 2 are complete. Phase 3 is in progress.
Complexity: 🟢 Low / 🟡 Medium / 🔴 High.

---

## Phase 1 — Grid Generation and Configuration ✅ COMPLETE

### 1.0 — Generate all grids ✅
- **Actual outputs:** hex_10000ha.shp (22,842 cells), hex_20000ha.shp (11,500 cells), hex_40000ha.shp (5,822 cells), sq_20000ha.shp (11,449 cells)
- **Tool used:** ArcGIS Pro — Generate Tessellation
- **CRS:** ESRI:102033

### 1.1 — Shape comparison: hexagon vs. square ✅
- **Actual result:** Maximum difference between HEX-20 and SQ-20 matrices < 0.008 in all quadrants (1985 and 2020). CV_hex ≈ CV_sq (difference < 0.001). Distributions practically identical at biome scale.
- **Conclusion:** Method robust to shape choice. Hexagonal grid preferred on theoretical grounds (isotropy) but not empirically necessary at this scale.

### 1.2 — Scale sensitivity ✅
- **Actual result:** Mean EII differs by < 0.001 across HEX-10, HEX-20, HEX-40 in both years. Scale effect on aggregated distributions is negligible within the tested range.
- **Conclusion:** HEX-20 confirmed as primary configuration. Results stable across scales.

### 1.3 — Jitter (zoning sensitivity) ✅
- **Design:** 25 realizations (8 directions × 3 distances + original); displacements: 2,533 / 5,066 / 7,598 m.
- **Actual result:** Mean EII range across 25 realizations < 0.005 in both years. CV across realizations < 0.003.
- **Conclusion:** EII estimates are highly robust to grid placement. Method passes MAUP test.

---

## Phase 2 — Full Annual Time Series ✅ COMPLETE

### 2.1 — Run EII and Area pipeline for all years ✅
- **Actual output:** eii_HEX20_annual.csv and area_HEX20_annual.csv — 11,500 cells × 40 years (1985–2024).
- **Key finding:** EII mean declined from 0.858 (1985) to 0.643 (2024); Area mean declined from 0.859 to 0.644.

### 2.2 — Assemble paired dataset and compute divergence metrics ✅
- **Actual outputs:** eii_area_HEX20_annual.csv, annual_states.csv, delta_annual_summary.csv, moran_annual.csv
- **Key results:**

**Annual state dynamics (1985 → 2024):**
| State | 1985 | 2024 | Change |
|---|---|---|---|
| Concordant-High | 91.5% | 57.6% | −33.9 pp |
| Concordant-Low | 6.0% | 34.1% | +28.0 pp |
| Type I (high area, low EII) | 0.9% | 4.2% | +3.3 pp |
| Type II (low area, high EII) | 1.6% | 4.1% | +2.5 pp |
| Total divergent (I + II) | 2.5% | 8.4% | +5.8 pp |

**Delta (EII − Area) dynamics (1985 → 2024):**
| Metric | 1985 | 2024 |
|---|---|---|
| P10 (negative tail) | −0.061 | −0.093 |
| SD | 0.054 | 0.076 |
| % cells with δ < 0 | 41.8% | 46.9% |
| % cells with |δ| < 0.05 | 75.8% | 58.5% |

**Moran's I (divergent states):** Significant in all 40 years (p < 0.01); I = 0.094–0.136; z-scores 16–26. Divergent cells are spatially clustered throughout the series.

---

## Phase 3 — Core Analyses 🔄 IN PROGRESS

### 3.1 — Area–EII correlation and independence (RQ1) 🔲
- **Input:** Paired annual dataset (2.2).
- **Output:** Pearson/Spearman correlation per year; residual distribution; variance decomposition.
- **Complexity:** 🟢 Low

### 3.2 — Landscape state classification (RQ1) ✅ (data available)
- **Status:** annual_states.csv produced in Phase 2. Needs formal statistical summary for paper.
- **Pending:** threshold sensitivity test (0.5 midpoint vs. quantile-based).

### 3.3 — 5×5 frequency matrix analysis — snapshots (RQ2) 🔲
- **Input:** Paired dataset; snapshot years: 1985, 1995, 2004, 2012, 2020, 2024.
- **Output:** Six 5×5 matrices; difference matrices between periods.
- **Complexity:** 🟢 Low

### 3.4 — Spatial maps (RQ2) 🔲
- **Input:** Paired dataset; HEX-20 shapefile.
- **Output:** Choropleth maps of Area, EII, and δ for selected years; cumulative divergence trace map.
- **Complexity:** 🟡 Medium
- **Note:** cumulative_decoupling_trace.shp already generated in Phase 2 — use as base for Fig. 5.

### 3.5 — Change point detection: EII and Area (RQ2) 🔲
- **Input:** Paired annual dataset.
- **Algorithm:** PELT (ruptures library); penalty via BIC.
- **Output:** Structural break years per cell for EII and Area; temporal lag Δᵢ = t*_w − t*_A; spatial map of Δᵢ.
- **Complexity:** 🔴 High
- **Notes:** 11,500 series × 40 observations each. Vectorize with numpy before looping.

### 3.6 — Temporal interval sensitivity (RQ3) 🔲
- **Input:** Paired annual dataset.
- **Output:** 5×5 matrices at 5-year vs. 10-year intervals; comparison.
- **Complexity:** 🟢 Low

---

## Phase 4 — Synthesis and Documentation 🔲 PENDING

### 4.1 — Final figures
- Fig. 1: Conceptual diagram (illustration)
- Fig. 2: Example cells in each quadrant
- Fig. 3: Annual state flux + cumulative trace map
- Fig. 4: Delta distribution — trend and violin
- Fig. 5: Moran's I over time + spatial maps
- Fig. 6: MAUP sensitivity panels

### 4.2 — Methods section writing
- Priority: Section 3.4 (EII formalization with δ definition)
- Then: Sections 3.7 (MAUP), 3.9 (spatial autocorrelation), 3.10 (δ analysis)

### 4.3 — Reproducibility package
- requirements.txt or environment.yml
- README step-by-step
- Zenodo deposit of derived datasets

---

## Summary Table

| Step | Phase | Status | RQ | Deliverable |
|---|---|---|---|---|
| 1.0 Grid generation | 1 | ✅ | — | 4 shapefiles |
| 1.1 Shape comparison | 1 | ✅ | RQ3 | Fig. 6 |
| 1.2 Scale sensitivity | 1 | ✅ | RQ3 | Fig. 6 |
| 1.3 Jitter (MAUP) | 1 | ✅ | RQ3 | Fig. 6 |
| 2.1 Full EII+Area pipeline | 2 | ✅ | — | Core dataset |
| 2.2 Paired dataset + divergence | 2 | ✅ | RQ1, RQ2 | annual_states, delta, moran |
| 3.1 Correlation | 3 | 🔲 | RQ1 | Section 4.1 |
| 3.2 State classification | 3 | 🔄 | RQ1 | Fig. 3 |
| 3.3 Frequency matrices | 3 | 🔲 | RQ2 | Fig. 3 |
| 3.4 Spatial maps | 3 | 🔲 | RQ2 | Fig. 5 |
| 3.5 Change point detection | 3 | 🔲 | RQ2 | Fig. 5 |
| 3.6 Temporal sensitivity | 3 | 🔲 | RQ3 | Supp. S2 |
| 4.1 Final figures | 4 | 🔲 | — | Figs. 1–6 |
| 4.2 Methods writing | 4 | 🔲 | — | Sections 3.x |
| 4.3 Reproducibility | 4 | 🔲 | — | Supp. S4 |

---

## Pending decisions

| Decision | Status | Notes |
|---|---|---|
| Target cell size | ✅ 20,000 ha primary | |
| Grid shape | ✅ Hexagonal primary | |
| Study domain | ✅ 1,500 × 1,500 km, ESRI:102033 | |
| Snapshot years | ✅ 1985, 1995, 2004, 2012, 2020, 2024 | |
| Divergence threshold | 🔲 Open — 0.5 vs. quantile-based | Decide before step 3.2 formal analysis |
| Changepoint penalty | 🔲 Open — BIC default | Decide before step 3.5 |
| Target journal | 🔲 Ecological Indicators (preliminary) | Confirm before submission |

---

*Update this document after each analytical step is completed. Record actual outputs, deviations from plan, and decisions made.*
