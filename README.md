# Landscape Line Intercept (LLI)
### A systematic transect-based metric for landscape interface continuity

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status: Phase 3 — Core Analyses](https://img.shields.io/badge/Status-Phase%203%20In%20Progress-orange)]()
[![DOI](https://zenodo.org/badge/1196502549.svg)](https://doi.org/10.5281/zenodo.19889630)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19889631.svg)]
(https://doi.org/10.5281/zenodo.19889631)
``

---

## Overview

The **Landscape Line Intercept (LLI)** is a landscape connectivity metric that reinterprets
the borders of a regular hexagonal grid as a spatially exhaustive set of systematic
transects — directly analogous to the line intercept method in vegetation ecology
(Canfield 1941). The proportion of each cell perimeter that intersects natural habitat
defines the EII, providing a measure of **interface connectivity** complementary to
within-cell area metrics.

**Key distinction:** Area sampling (polygon interior) and line sampling (polygon
perimeter) are complementary estimators of landscape structure. Area estimates
*composition* (what is inside a cell); EII estimates *interface connectivity* (how
permeable the cell boundary is). Their joint distribution characterizes landscape
state more fully than either alone.

**Study domain:** Fixed rectangle of 1,500 × 1,500 km in central Brazil
(ESRI:102033 Albers Equal Area Conic), encompassing the core Cerrado, southern Amazon
deforestation frontier, northern Pantanal, and Cerrado–Caatinga transition zone.

**Input data:** MapBiomas binary rasters (natural vegetation vs. non-natural), 30 m
resolution, 1985–2024 (annual)

**Primary grid:** Hexagonal, 20,000 ha (~15.2 km side), 11,500 cells

---

## Conceptual basis

For each cell *i* at time *t*, two metrics are computed:

**Within-cell area** — proportion of natural habitat pixels inside the cell:

$$A_i(t) = \frac{\sum_{p \in C_i} \mathbf{1}[r_p(t) = 1]}{|C_i|}$$

**Edge Interception Index** — proportion of the cell perimeter intercepting natural
habitat:

$$w_i(t) = \frac{L_i^{\text{nat}}(t)}{P_i^{\text{obs}}(t)}$$

**Continuous divergence** — difference between interface connectivity and interior
composition:

$$\delta_i(t) = w_i(t) - A_i(t)$$

$\delta > 0$: interface more connected than interior composition suggests
$\delta < 0$: interface more degraded than interior composition suggests

The four landscape states in the Area × EII space:

| State | Area | EII | Interpretation |
|---|---|---|---|
| Coupled-High | High | High | Intact: abundant interior habitat, connected interface |
| Coupled-Low | Low | Low | Degraded: scarce interior habitat, isolated interface |
| Type I | High | Low | Interior preserved, interface degraded |
| Type II | Low | High | Interior lost, interface still connected |

---

## Key results (Phases 1–2 complete)

**Grid configuration sensitivity (Phase 1):**
- EII estimates are robust to grid placement: mean range < 0.005 across 25 jitter
  realizations; CV < 0.003
- Scale effect negligible: mean EII differs < 0.001 across 10,000 / 20,000 / 40,000 ha
- Shape effect negligible at biome scale: HEX-20 and SQ-20 distributions differ < 0.008

**Annual time series 1985–2024 (Phase 2):**
- EII mean declined from 0.858 (1985) to 0.643 (2024); Area mean from 0.859 to 0.644
- Coupled-High cells: 91.5% → 57.6% (−33.9 pp over 40 years)
- Divergent cells (Type I + II): 2.5% → 8.4%; spatially clustered in all years
  (Moran's I = 0.094–0.136, p < 0.01 throughout)
- Negative tail of δ widened: P10 from −0.061 to −0.093; % cells with |δ| < 0.05
  fell from 75.8% to 58.5%

---

## Repository structure

```
eii-landscape-metric/
├── notebooks/
│   ├── continuidade_refatorado.ipynb        # Original EII extraction pipeline
│   ├── jitter_grid_generation.ipynb         # Generate 25 jitter grids
│   ├── phase1_sensitivity_analysis_v2.ipynb # MAUP sensitivity (shape, scale, jitter)
│   └── phase2_annual_pipeline.ipynb         # Annual EII + Area + divergence analysis
├── data/
│   ├── indices_bordas_EIF_consolidado.csv   # OBS baseline dataset (legacy)
│   ├── eii_HEX20_annual.csv                 # EII — 11,500 cells × 40 years
│   ├── area_HEX20_annual.csv                # Area — 11,500 cells × 40 years
│   ├── annual_states.csv                    # Landscape state frequencies 1985–2024
│   ├── delta_annual_summary.csv             # δ = EII − Area distribution by year
│   └── moran_annual.csv                     # Moran's I for divergent states by year
├── docs/
│   ├── paper_outline_EII.md                 # Full paper outline with results
│   ├── analysis_roadmap_EII.md              # Analysis plan with status tracking
│   └── jitter_realizations_summary.csv      # 25 jitter grid specifications
├── config/
│   └── config_template.py                   # Configuration template
├── .gitignore
├── LICENSE
└── README.md
```

---

## Getting started

### Requirements

```
Python >= 3.10
rasterstats
geopandas
rasterio
pandas
numpy
matplotlib
libpysal
esda
```

Install all dependencies:

```bash
pip install rasterstats geopandas rasterio pandas numpy matplotlib libpysal esda
```

### Critical note on nodata encoding

MapBiomas binary rasters declare `nodata=0` in file metadata, but `0` encodes
non-natural vegetation — a valid value that must be counted in the denominator.
True outside-domain pixels are encoded as `255`. All notebooks use `nodata=255`
hardcoded. Do not override this without verifying the raster encoding.

### Running the pipeline

1. Clone this repository
2. Copy `config/config_template.py` and edit paths
3. Open notebooks in order: `continuidade_refatorado` → `jitter_grid_generation`
   → `phase1_sensitivity_analysis_v2` → `phase2_annual_pipeline`
4. Edit only the configuration cell (Section 1) in each notebook
5. Run all cells sequentially — checkpoint system allows safe interruption and
   resumption

---

## Data

### Input (not included — available from MapBiomas)

- Binary rasters: natural vegetation (1) vs. non-natural (0), 30 m resolution
- Hexagonal and square grid shapefiles generated in ArcGIS Pro (Generate Tessellation)
  using the domain rectangle defined in ESRI:102033
- Source: [MapBiomas Brazil](https://mapbiomas.org)

### Output (included in `data/`)

| File | Description | Dimensions |
|---|---|---|
| `eii_HEX20_annual.csv` | EII per cell per year | 11,500 × 41 |
| `area_HEX20_annual.csv` | Area per cell per year | 11,500 × 41 |
| `annual_states.csv` | Landscape state frequencies | 40 years × 10 cols |
| `delta_annual_summary.csv` | δ distribution statistics | 40 years × 11 cols |
| `moran_annual.csv` | Spatial autocorrelation of divergence | 40 years × 5 cols |

---

## Project status

| Phase | Description | Status |
|---|---|---|
| **Phase 1** | Grid configuration sensitivity (MAUP) | ✅ Complete |
| **Phase 2** | Full annual time series (1985–2024) | ✅ Complete |
| **Phase 3** | Core analyses (correlation, matrices, maps, changepoints) | 🔄 In progress |
| **Phase 4** | Final figures, Methods writing, reproducibility package | 🔲 Pending |

See [`docs/analysis_roadmap_EII.md`](docs/analysis_roadmap_EII.md) for the
step-by-step plan with status tracking.

---

## Citation

If you use this code or data, please cite:

> Barroso et al. (in preparation). *The Edge Interception Index: a systematic
> transect-based metric for landscape interface connectivity and its application
> to four decades of habitat dynamics in central Brazil.*

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---



## Contact

**Mario Barroso**  
The Nature Conservancy
```

---

**Passo 4.** No final da página, em **"Commit changes"**, escreva:
```
Write full README with method description and repository structure
