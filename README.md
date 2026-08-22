# Landscape Line Intercept (LLI)
### A systematic transect-based metric for landscape interface connectivity

![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Phase%203%20Complete-green.svg)
[![DOI (concept)](https://zenodo.org/badge/1196502549.svg)](https://doi.org/10.5281/zenodo.19889630)
[![DOI (v1.0.1)](https://zenodo.org/badge/DOI/10.5281/zenodo.19889631.svg)](https://doi.org/10.5281/zenodo.19889631)

---

## Overview

The **Landscape Line Intercept (LLI)** is a landscape connectivity metric that reinterprets
the borders of a regular hexagonal grid as a spatially exhaustive set of systematic
transects — directly analogous to the line intercept method in vegetation ecology
(Canfield 1941). The proportion of each cell perimeter that intersects natural habitat
defines the LLI, providing a measure of **interface connectivity** complementary to
within-cell area metrics.

**Key distinction:** Area sampling (polygon interior) and line sampling (polygon
perimeter) are complementary estimators of landscape structure. Area estimates
*composition* (what is inside a cell); LLI estimates *interface connectivity* (how
permeable the cell boundary is to habitat continuity with neighbouring units). Their
joint distribution characterises landscape state more fully than either alone.

**Methodological lineage:** The LLI extends line intersect sampling (LIS; Ramezani &
Holm 2011) from an external probabilistic sampling strategy to an intrinsic, exhaustive
analytical structure. Rather than imposing transects externally to reduce data-collection
cost, the LLI treats the boundaries of a regular grid — already present in any grid-based
workflow — as a spatially exhaustive set of transects. Every boundary pixel is counted,
not sampled.

**Study domain:** Fixed rectangle of 1,500 × 1,500 km in central Brazil
(ESRI:102033 South America Albers Equal Area Conic), encompassing the core Cerrado,
southern Amazon arc of deforestation, northern Pantanal, and Cerrado–Caatinga
transition zone (~2.25 × 10⁶ km²).

**Input data:** MapBiomas Collection 10.1 binary rasters (natural vegetation vs.
non-natural land cover), 30 m resolution, 1985–2024 (annual). Effective analysis
period: **1986–2023** (38 years; boundary years excluded due to MapBiomas temporal
filtering artefacts).

**Primary grid:** Regular hexagonal, 20,000 ha (~15.2 km side length; ~54.4 km
perimeter), 11,500 cells.

---

## Conceptual basis

For each cell *i* at time *t*, two metrics are computed:

**Within-cell area** — proportion of natural habitat pixels inside the cell:

$$A_i(t) = \frac{\sum_{p \in C_i} \mathbf{1}[r_p(t) = 1]}{|C_i|}$$

**Landscape Line Intercept** — proportion of the cell perimeter intercepting natural
habitat:

$$w_i(t) = \frac{L_i^{\text{nat}}(t)}{P_i^{\text{obs}}(t)}$$

where $L_i^{\text{nat}}(t)$ is the count of perimeter pixels intercepting natural habitat
(value = 1), and $P_i^{\text{obs}}(t)$ is the total count of valid perimeter pixels
(nodata = 255 excluded).

**Compositional–configurational divergence** — signed difference between interface
connectivity and interior composition:

$$\delta_i(t) = w_i(t) - A_i(t)$$

- $\delta > 0$: interface more connected than interior composition suggests
- $\delta < 0$: interface more degraded than interior composition suggests
- $\delta \approx 0$: the two dimensions are aligned

**Four landscape states** in the Area × LLI space (threshold τ = 0.5):

| State | Area | LLI | Landscape interpretation |
|---|---|---|---|
| Concordant-High | ≥ 0.5 | ≥ 0.5 | Intact: abundant interior habitat, connected interface |
| Concordant-Low | < 0.5 | < 0.5 | Degraded: scarce interior, isolated interface |
| Type I | ≥ 0.5 | < 0.5 | Interior preserved, interface already degraded |
| Type II | < 0.5 | ≥ 0.5 | Interior largely lost, interface connectivity persists |

Type I and Type II cells are the *compositionally–configurationally divergent* states:
landscapes where area metrics alone would misrepresent connectivity status.

---

## Key results (effective analysis period 1986–2023)

**RQ1 — Informational complementarity:**
- Pearson r between LLI and Area: 0.960–0.966 across all 38 years (stable but not
  redundant: ~7% unexplained variance corresponds to ~800 cells/year where LLI
  carries independent structural information)
- Proportion of cells where |residual| > 0.10 (LLI substantially exceeds area
  prediction): doubled from **8.0% (1986) to 16.4% (2023)**
- Divergent cells (Type I + II combined): tripled from **2.8% (1986) to 8.2% (2023)**
- Spatial clustering of divergence: Moran's I = 0.094–0.136, significant in all
  38 years (p < 0.01, 99 permutations)

**RQ2 — Spatiotemporal divergence dynamics:**
- Concordant-High cells: 90.8% → 58.4% (−32.4 pp over 38 years)
- Negative tail of δ widened: P10 from −0.060 (1986) to −0.094 (2023); proportion
  of cells with δ < 0 increased from 41.7% to 47.0%
- Domain-level Pettitt test (series of first differences): single significant
  transition in rate of LLI decline detected in **2006** (K = 346, p < 0.001),
  coinciding with PPCDAm consolidation and Soy Moratorium — detected without
  auxiliary governance information
- Cell-level heterochrony (Mode A): primary break years span 1990–2020
  (median: 2000; SD: 6.0 years), documenting the progressive advance of the
  deforestation frontier across the domain

**RQ3 — MAUP sensitivity:**
- Zoning effect: mean domain-level LLI varies < 0.005 across 25 systematic grid
  realisations; **CV < 0.003**
- Scale effect: mean LLI difference < 0.001 across HEX-10, HEX-20, HEX-40
  (10,000–40,000 ha range)
- Shape effect: maximum cell-wise difference < 0.008 between HEX-20 and SQ-20
  across all quadrants of the 5×5 Area × LLI frequency matrix

---

## Repository structure

```
lli-landscape-metric/
├── notebooks/
│   ├── continuidade_refatorado.ipynb           # LLI extraction pipeline (primary)
│   ├── jitter_grid_generation.ipynb            # Generate 25 displacement grids (RQ3)
│   ├── phase1_sensitivity_analysis_v2.ipynb    # MAUP sensitivity: shape, scale, zoning
│   ├── phase2_annual_pipeline.ipynb            # Annual LLI + Area + δ time series
│   └── phase3_analyses.ipynb                   # Correlation, matrices, change-point,
│                                               # heterochrony, segment decomposition
├── data/
│   ├── lli_HEX20_annual.csv                    # LLI — 11,500 cells × 40 years
│   ├── area_HEX20_annual.csv                   # Area — 11,500 cells × 40 years
│   ├── annual_states.csv                       # Landscape state frequencies 1986–2023
│   ├── delta_annual_summary.csv                # δ = LLI − Area distribution by year
│   ├── moran_annual.csv                        # Moran's I for divergent states by year
│   └── indices_bordas_EIF_consolidado.csv      # Legacy OBS baseline dataset
├── docs/
│   ├── paper_outline_LLI.md                    # Full paper outline (revision 14)
│   └── analysis_roadmap_LLI.md                 # Analysis plan with status tracking
├── config/
│   └── config_template.py                      # Configuration template (edit paths here)
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
ruptures
```

Install all dependencies:

```bash
pip install rasterstats geopandas rasterio pandas numpy matplotlib libpysal esda ruptures
```

### Critical note on nodata encoding

MapBiomas binary rasters declare `nodata=0` in file metadata, but `0` encodes
non-natural vegetation — a valid value that **must** be counted in the denominator.
True outside-domain pixels are encoded as `255`. All notebooks use `nodata=255`
hardcoded. Do not override this without verifying the raster encoding. See Methods
Section 3.2 of the companion manuscript for full details.

### Running the pipeline

1. Clone this repository
2. Copy `config/config_template.py` to your working directory and edit paths
3. Open notebooks in order:
   - `continuidade_refatorado` → extracts LLI and Area for all annual rasters
   - `jitter_grid_generation` → generates 25 displacement realisations for RQ3
   - `phase1_sensitivity_analysis_v2` → MAUP sensitivity (shape, scale, zoning)
   - `phase2_annual_pipeline` → annual time series, δ, and state classification
   - `phase3_analyses` → correlation, 5×5 matrices, change-point detection,
     spatial heterochrony, segment decomposition
4. Edit **only the configuration cell** (Section 1) in each notebook
5. Run all cells sequentially — the checkpoint system allows safe interruption
   and resumption without reprocessing completed years

---

## Data

### Input (not included — available from MapBiomas)

- Annual binary rasters: natural vegetation (1) vs. non-natural (0), 30 m resolution,
  1985–2024
- Source: [MapBiomas Brazil](https://mapbiomas.org) — Collection 10.1
- Hexagonal and square grid shapefiles generated in ArcGIS Pro (Generate Tessellation)
  in ESRI:102033; domain rectangle lower-left (200,000; 1,700,000) m,
  upper-right (1,700,000; 3,200,000) m

### Output (included in `data/`)

| File | Description | Dimensions |
|---|---|---|
| `lli_HEX20_annual.csv` | LLI per cell per year | 11,500 × 41 |
| `area_HEX20_annual.csv` | Area per cell per year | 11,500 × 41 |
| `annual_states.csv` | Landscape state frequencies | 38 years × 10 cols |
| `delta_annual_summary.csv` | δ distribution statistics | 38 years × 11 cols |
| `moran_annual.csv` | Spatial autocorrelation of divergence | 38 years × 5 cols |

---

## Project status

| Phase | Description | Status |
|---|---|---|
| **Phase 1** | Grid configuration sensitivity (MAUP — RQ3) | ✅ Complete |
| **Phase 2** | Full annual time series 1985–2024 | ✅ Complete |
| **Phase 3** | Core analyses: correlation, matrices, change-point, heterochrony, segment decomposition | ✅ Complete |
| **Phase 4** | Final figures, manuscript submission, reproducibility package | 🔄 In progress |

**Manuscript status:** Near-complete draft under preparation for submission to
*Methods in Ecology and Evolution*. All sections drafted; pending final figure
revisions (LLI relabelling, north arrow/scale bar on maps), back matter, and
supplementary materials.

---

## Citation

If you use this code or data, please cite the versioned software archive:

> Barroso Ramos Neto, M. (2026). *lli-landscape-metric: Landscape Line Intercept (LLI)*
> (v1.0.1). Zenodo. https://doi.org/10.5281/zenodo.19889631

For the methodological framework, please also cite the companion manuscript
(in preparation):

> Barroso Ramos Neto, M. (in preparation). The Landscape Line Intercept: recovering
> interface connectivity from the discarded boundaries of regular landscape grids.
> *Methods in Ecology and Evolution*.

---

## References

Canfield, R. H. (1941). Application of the line interception method in sampling range
vegetation. *Journal of Forestry*, 39(4), 388–394.
https://doi.org/10.1093/jof/39.4.388

Ramezani, H., & Holm, S. (2011). Sample based estimation of landscape metrics; accuracy
of line intersect sampling for estimating edge density and Shannon's diversity index.
*Environmental and Ecological Statistics*, 18(1), 109–130.
https://doi.org/10.1007/s10651-009-0123-2

Souza Jr., C. M., et al. (2020). Reconstructing three decades of land use and land cover
changes in Brazilian biomes with Landsat archive and Earth Engine. *Remote Sensing*,
12(17), 2735. https://doi.org/10.3390/rs12172735

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

## Contact

**Mario Barroso Ramos Neto**
The Nature Conservancy
mario.barroso@tnc.org
ORCID: 0000-0001-5890-0536
