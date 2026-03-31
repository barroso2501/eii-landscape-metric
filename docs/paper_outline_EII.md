# Paper Outline: Edge Interception Index (EII)
## A Systematic Transect-Based Metric for Landscape Connectivity — Method and Application to the Brazilian Cerrado

**Status:** Working outline — not for submission  
**Target journal (preliminary):** Ecological Indicators  
**Last updated:** 2026-03-30 (rev. 3 — sections 3.1 and 3.3 finalized)

---

## Proposed Title

*"The Edge Interception Index: a systematic transect-based metric for landscape interface connectivity and its application to four decades of habitat dynamics in the Brazilian Cerrado"*

---

## Research Questions

**RQ1.** Does the Edge Interception Index (EII) provide information on habitat configuration that is not captured by within-cell area metrics alone?

**RQ2.** Do structural breaks in annual EII time series coincide with structural breaks in area metrics, and where — in space and in time — do they diverge across the Cerrado?

**RQ3.** How robust are EII estimates to grid configuration choices (shape, scale, and placement), and how sensitive are temporal patterns to the choice of sampling interval?

---

## Abstract (placeholder — write last)

*To be written after Results are complete. Structure: problem → method → data → key result → implication.*

---

## 1. Introduction

### 1.1 Opening problem
- Area-based metrics (proportion of natural habitat within spatial units) are the dominant tool for landscape monitoring at regional scales.
- Area alone does not capture interface connectivity: two cells with identical area proportions can differ fundamentally in how habitat is distributed relative to their boundaries.
- This gap is consequential for conservation planning, since habitat permeability at unit boundaries governs movement and dispersal at the landscape scale.

### 1.2 Existing approaches and their limitations
- FRAGSTATS-based metrics (patch area, edge density, shape indices): computed internally to each unit; do not measure cross-boundary permeability.
- Graph-based connectivity models (circuit theory, least-cost paths): powerful but computationally intensive, require species-specific parameterization, and do not scale easily to biome-wide time series.
- Linear transect methods in vegetation ecology (Canfield 1941; Levy & Madden 1933): well-established estimators of cover based on systematic line sampling; not previously applied at landscape scale to raster time series.

### 1.3 The proposed approach
- We propose reinterpreting the borders of a regular hexagonal grid as a spatially exhaustive set of systematic transects.
- Each border segment between adjacent cells constitutes a linear transect; contacts with natural habitat pixels along the transect define the Edge Interception Index (EII).
- This transposition of the line intercept method from vegetation ecology to landscape ecology provides a conceptually grounded, computationally efficient, and temporally replicable metric of interface connectivity.
- The hexagonal grid is particularly suited to this approach: six sides per cell sample six directions, providing greater directional isotropy than square grids (four sides, axial bias).

### 1.4 Study area and motivation
- The Brazilian Cerrado: one of the world's most threatened savanna biomes, subject to intense agricultural expansion over the past four decades.
- ~2 million km² with documented, non-stationary deforestation dynamics — distinct regimes separated by policy and market shifts.
- A biome-scale, annually resolved raster time series (MapBiomas, 30 m resolution, 1985–2024) provides an ideal test case for a new landscape metric.

### 1.5 Research questions
*(State RQ1, RQ2, RQ3 as formalized above.)*

### 1.6 Contributions
1. A formal transect-based metric of landscape interface connectivity derived from regular grids.
2. A biome-scale, four-decade characterization of Area–EII joint distributions and their structural breaks.
3. A systematic treatment of the Modifiable Areal Unit Problem (MAUP) as quantifiable sampling variance rather than an unavoidable limitation.

---

## 2. Background

### 2.1 The line intercept method in vegetation ecology
- Canfield (1941): foundational formulation of line intercept sampling for cover estimation.
- Statistical properties: unbiased estimator of cover under random or systematic placement.
- Transposition to landscape scale: border segments as systematic, spatially exhaustive transects.

### 2.2 The Modifiable Areal Unit Problem in landscape ecology
- Classical MAUP: scale effect and zoning effect.
- Existing treatments: typically acknowledged as a caveat, rarely quantified.
- Reframing: when the grid is treated as a sampling device, MAUP becomes sampling variance — a quantity that can be estimated and reported.

### 2.3 Landscape metrics and connectivity
- Brief review of area metrics (proportion of natural habitat) and their widespread use.
- Brief review of edge and boundary metrics (edge density, contrast-weighted edge).
- Gap: no metric simultaneously captures (a) systematic spatial coverage, (b) temporal replicability at annual resolution, and (c) interface-level connectivity.

---

## 3. Methods

### 3.1 Study area
- The study domain is a fixed rectangular area of 1,500 × 1,500 km (2.25 × 10⁶ km²) in the South America Albers Equal Area Conic projection (ESRI:102033; central meridian −60°W; standard parallels −5° and −42°; datum SAD69).
- Domain coordinates (projected): lower-left (200,000; 1,700,000) m — upper-right (1,700,000; 3,200,000) m.
- The domain encompasses: the core Brazilian Cerrado; the southern Amazon deforestation frontier (arc of deforestation); the northern Pantanal; and the Cerrado–Caatinga transition zone.
- A fixed rectangular domain was deliberately chosen to ensure all grid cells are geometrically complete across all tested configurations, eliminating clipping-induced confounding from boundary irregularities.
- Ecological justification: the domain covers the full gradient of land-use intensity documented in central Brazil over the study period — from consolidated agricultural areas in the north (MATOPIBA region) to more preserved savannas in the center and south — providing the landscape configuration diversity required for a rigorous methodological evaluation.
- All input raster data (MapBiomas, 1985–2024) provide complete coverage of the domain.

### 3.2 Input data
- MapBiomas Collection [X], 30 m resolution, 1985–2024.
- Binarization: natural vegetation (class 1) vs. non-natural (class 0).
- Annual time series: 40 raster layers per analysis unit.
- Rationale for binary classification: focus on habitat presence/absence rather than vegetation type diversity.

### 3.3 Grid design

**Projection and domain:**
- All grids generated in ESRI:102033 (South America Albers Equal Area Conic), ensuring equal-area cells throughout the domain.
- Grid extent: the 1,500 × 1,500 km rectangular domain defined in Section 3.1. All cells are fully contained within the domain — no boundary clipping applied.

**Primary configuration — hexagonal grid, 20,000 ha:**
- Cell area: 20,000 ha (200 km²); side length: ~15.2 km; diagonal: ~26.2 km.
- Number of cells: ~11,250.
- Rationale for hexagonal geometry: six border segments at 0°, 60°, 120°, 180°, 240°, 300° provide near-isotropic directional sampling, compared to four segments at 0°, 90°, 180°, 270° for square grids.
- Rationale for 20,000 ha as primary scale: (1) ecologically interpretable as the watershed / small-municipality scale, where EII measures inter-unit connectivity at a functionally coherent resolution; (2) perimeter length (~54 km) provides sufficient pixel contacts for estimator stability; (3) alignment with territorial planning scales commonly used in Brazilian conservation policy.

**Scale sensitivity configurations:**

| Configuration | Cell area | Side length | Approx. cells | Ecological scale |
|---|---|---|---|---|
| Fine | 10,000 ha | ~10.7 km | ~22,500 | Property / forest fragment |
| **Primary** | **20,000 ha** | **~15.2 km** | **~11,250** | **Watershed / small municipality** |
| Coarse | 40,000 ha | ~21.5 km | ~5,625 | Regional mosaic / corridor |

- Scale ratio: ×2 in side length, ×4 in area between consecutive levels — a geometrically consistent hierarchy.
- The three scales bracket the range identified by prior landscape ecology studies as most informative for savanna fragmentation dynamics (5,000–50,000 ha).
- Hexagonal grids do not nest perfectly across scales (unlike square grids); scale comparisons are therefore treated as independent configurations, not a hierarchical decomposition.

**Shape sensitivity configuration — square grid:**
- Cell area: 20,000 ha (equivalent to primary hexagonal); side length: ~14.14 km.
- Used exclusively for shape comparison in Section 3.7.1; not used as a primary analysis configuration.
- Note: equal area implies unequal perimeter (P_square ≈ 56.6 km vs. P_hexagon ≈ 54.4 km); this difference is treated as a known property and reported explicitly (see Section 3.7.1).

### 3.4 EII formalization
**Within-cell area metric:**

$$A_i(t) = \frac{\sum_{p \in C_i} \mathbf{1}[r_p(t) = 1]}{|C_i|}$$

where $C_i$ is the set of pixels within cell $i$, $r_p(t)$ is the raster value of pixel $p$ at time $t$, and $|C_i|$ is the total number of valid pixels.

**Edge Interception Index (EII):**

$$w_i(t) = \frac{L_i^{\text{nat}}(t)}{P_i^{\text{obs}}(t)}$$

where $L_i^{\text{nat}}(t)$ is the length (in pixels) of the cell perimeter that intersects natural habitat at time $t$, and $P_i^{\text{obs}}(t)$ is the total observable perimeter length (excluding pixels with nodata values).

- $w_i(t) \in [0, 1]$: 0 = perimeter entirely surrounded by non-natural pixels; 1 = perimeter entirely surrounded by natural habitat.
- For border cells of the study domain: $P_i^{\text{obs}} < P_i$ (total perimeter); completeness ratio $P_i^{\text{obs}} / P_i$ is reported as a data quality flag.
- Computational implementation: perimeter geometries extracted from hexagonal polygons via boundary conversion; zonal statistics computed with `all_touched=True` (essential for linear geometries) using `rasterstats`.

**Connection to the line intercept method:**
- Each border segment is a systematic transect.
- Each pixel contact with natural habitat is a "hit."
- $w_i(t)$ is thus the hit rate along the perimeter transect — directly analogous to the cover estimator of Canfield (1941).

### 3.5 Annual time series construction
- EII computed for all years 1985–2024: 40 annual layers × 19,183 cells.
- Area metric ($A_i$) computed for the same period (already available).
- Output: two matrices of dimensions 19,183 × 40.

### 3.6 Temporal interval selection and sensitivity
- Primary analysis: annual resolution (1985–2024).
- Change point detection applied to annual series (see Section 3.8).
- Snapshot analysis: intervals anchored to documented deforestation regimes in the Cerrado:
  - 1985 (baseline)
  - 1995 (pre-Soy Moratorium era)
  - 2004 (historical peak deforestation)
  - 2012 (new Brazilian Forest Code)
  - 2020 (end of monitoring period)
- Sensitivity test: comparison of results under 5-year vs. 10-year snapshot intervals to demonstrate stability of aggregated distributions.

### 3.7 Sensitivity to grid configuration (MAUP)
**3.7.1 Shape effect: hexagon vs. square**

*Design rationale:* Comparing hexagonal and square grids at equivalent cell area introduces a known geometric confound: equal area implies unequal perimeter length, since the hexagon is isoperimetrically more efficient than the square (P_hex ≈ 0.93 × P_sq for equal area). Rather than treating this as a flaw to eliminate, the comparison is structured to separate three distinct dimensions of shape effect:

- **Dimension 1 — Aggregated distribution convergence** (primary test)
  - Square grid generated at equivalent cell area to the hexagonal grid.
  - EII computed under both configurations for 1985 and 2020.
  - Comparison: aggregated 5×5 Area × EII frequency matrices and their difference.
  - Expected result: if distributions converge, the method is robust to shape choice at the biome scale.

- **Dimension 2 — Estimator variance per unit area** (statistical argument)
  - Coefficient of variation (CV) of EII computed across cells for both geometries.
  - Expected result: hexagonal grid produces lower CV than square grid for equivalent area, reflecting its shorter perimeter relative to area and its superior isoperimetric efficiency.
  - This difference in variance is a property of the geometry, not a bias — it constitutes a statistical argument for preferring the hexagonal configuration.

- **Dimension 3 — Directional isotropy** (theoretical argument, no additional empirical test required)
  - Hexagon: 6 border segments at 0°, 60°, 120°, 180°, 240°, 300° — approximately isotropic.
  - Square: 4 border segments at 0°, 90°, 180°, 270° — axially biased.
  - Consequence: square grids systematically undersample diagonal landscape features (e.g., rivers, roads, ecotones oriented at 45°).
  - This property is documentable analytically; empirical demonstration is optional (e.g., by comparing EII values for landscape features of known orientation).

*Reporting strategy:* The three dimensions are presented in sequence in Section 4.4, moving from empirical (Dimensions 1–2) to theoretical (Dimension 3). The conclusion is that the hexagonal grid is preferable on all three grounds, while the method remains robust to shape choice at the level of aggregated distributions.

**3.7.2 Scale effect: multi-resolution comparison**
- EII computed for [2–3 cell sizes] within hexagonal geometry.
- Assessment: how does the Area × EII distribution change with scale?
- Criterion for scale selection: stability of estimator (coefficient of variation across cells as a function of perimeter length).

**3.7.3 Zoning effect: systematic grid displacement**
- 24 displaced realizations: 8 directions × 3 distances (1/6, 1/3, 1/2 of cell side length) + original grid = 25 realizations total.
- For each realization: compute EII; aggregate to 5×5 Area × EII frequency matrix.
- Output: mean matrix (central estimate), standard deviation matrix (sampling uncertainty), coefficient of variation per cell (spatial instability map).
- Interpretation: cells with high CV across realizations are located at abrupt landscape boundaries — a substantively informative, not merely methodological, result.

### 3.8 Change point detection
- Algorithm: PELT (Pruned Exact Linear Time; Killick et al. 2012) applied independently to each cell's annual EII and annual Area series.
- Implementation: Python `ruptures` library; penalty parameter selected via BIC.
- Output per cell: year(s) of structural break in EII ($t^*_w$) and in Area ($t^*_A$).
- Derived variable: temporal lag $\delta_i = t^*_w - t^*_A$ (positive = EII changes before Area; negative = Area changes before EII).
- Aggregation: frequency distribution of $\delta$ across cells; spatial map of $\delta$.

### 3.9 Area × EII joint distribution analysis
- Discretization: both $A_i$ and $w_i$ binned into five 20% classes → 5×5 frequency matrix per time period.
- Metrics derived from the matrix:
  - Total mass in diagonal quadrants (coupled states) vs. off-diagonal (decoupled states).
  - Difference matrices between periods: identifies states gaining or losing mass.
- Decoupling typology:
  - Type I (High Area, Low EII): habitat interior preserved but interface degraded.
  - Type II (Low Area, High EII): interior lost but interface still connected.

---

## 4. Results

### 4.1 EII as an independent information source (RQ1)
- Correlation between $A_i(t)$ and $w_i(t)$ across cells and time periods.
- Residual analysis: cells where EII deviates substantially from area-predicted values.
- Frequency of decoupled states (Type I and Type II) across the time series.
- Key figure: scatter plot Area × EII for two contrasting periods (e.g., 1985 and 2020) with decoupling quadrants highlighted.

### 4.2 Structural breaks and temporal divergence (RQ2)
- Distribution of changepoint years for EII and Area across cells.
- Frequency distribution of temporal lag $\delta_i$.
- Proportion of cells where EII changepoint precedes Area changepoint (potential early-warning signal).
- Spatial map of $\delta_i$ across the Cerrado — regional patterns of lead/lag.
- Narrative: which landscape processes (deforestation frontier, agricultural consolidation) are associated with each lag pattern?

### 4.3 Biome-scale dynamics (RQ2 — snapshot analysis)
- 5×5 Area × EII frequency matrices for anchored snapshots (1985, 1995, 2004, 2012, 2020).
- Difference matrices between periods.
- Interpretation: which states gained and lost mass in each deforestation regime?

### 4.4 Grid configuration sensitivity (RQ3)
- Hexagon vs. square: comparison of aggregated 5×5 matrices; quantification of directional bias in square grid.
- Scale sensitivity: how Area × EII distributions shift across cell sizes.
- Jitter analysis: mean, SD, and CV of EII across 25 grid realizations. Spatial map of CV.
- Summary statement: EII estimates are robust to grid placement within [X]% displacement; instability concentrates at landscape transition zones.

### 4.5 Temporal interval sensitivity (RQ3)
- Comparison of 5-year vs. 10-year snapshot matrices.
- Demonstration that aggregated distributions are stable under alternative interval choices.

---

## 5. Discussion

### 5.1 What EII reveals that area does not
- Decoupled states are not rare: frequency of Type I and Type II across the Cerrado and through time.
- Ecological interpretation: Type I cells may represent matrix-surrounded remnants where interior habitat persists but connectivity is already severed; Type II cells may represent landscapes in early-stage conversion where interface is still functional.
- Implications for reserve design and biological corridor planning.

### 5.2 EII as a temporal early-warning indicator
- Discussion of cells where EII changepoint precedes Area changepoint.
- Hypothesis: interface degradation precedes interior loss in landscapes subject to edge-in conversion dynamics.
- Limitations: change point detection with 40 annual observations; sensitivity to algorithm parameterization.

### 5.3 MAUP reframed as sampling variance
- Contrast with classical treatment of MAUP as limitation.
- The grid as a sampling device: spatial uncertainty is quantifiable and ecologically interpretable.
- Regions of high jitter CV as indicators of landscape transition zones — an output, not a flaw.
- Hexagonal grids as preferred geometry for transect-based connectivity metrics.

### 5.4 Methodological scope and transferability
- The method is raster-agnostic: applicable to any binary habitat map at any resolution.
- Scalability: computationally efficient pipeline with checkpoint architecture; applicable to continental-scale analyses.
- Limitations: EII measures perimeter-level connectivity, not patch-level or functional connectivity; does not account for species dispersal abilities; border cells require completeness correction.

### 5.5 Connections to existing literature
- Relationship to edge density metrics (FRAGSTATS): EII is a boundary-referenced, not patch-referenced, metric.
- Relationship to graph-based connectivity: EII weights ($w_{ij}$) can be used directly as edge weights in a spatial graph — connection to future work.
- Relationship to percolation theory: high-EII cells form percolating corridors; threshold behavior warrants future investigation.

---

## 6. Conclusions

- The Edge Interception Index, derived from the line intercept method of vegetation ecology, provides a computationally efficient and ecologically interpretable metric of landscape interface connectivity.
- Applied to the Cerrado over four decades, EII reveals decoupling states — particularly interface degradation preceding area loss — that area-based metrics fail to detect.
- MAUP effects are quantifiable as sampling variance and are ecologically informative.
- The method is transferable to any binary raster time series and scalable to continental extents.

---

## Figures (planned)

| Figure | Content | Source analysis |
|---|---|---|
| **Fig. 1** | Conceptual diagram: hexagonal cell, perimeter as transect, pixel contacts | Illustration |
| **Fig. 2** | Example cells showing Area × EII decoupling (visual tiles) | MapBiomas tiles |
| **Fig. 3** | Area × EII scatter + 5×5 matrices for 1985 and 2020 + difference matrix | Section 4.1, 4.3 |
| **Fig. 4** | Maps of $A_i$, $w_i$, and decoupling type across the Cerrado | Section 4.3 |
| **Fig. 5** | Changepoint analysis: distribution of $\delta_i$; spatial map of lead/lag | Section 4.2 |
| **Fig. 6** | MAUP sensitivity: jitter CV map; hex vs. square comparison; scale comparison | Section 4.4 |

---

## Supplementary Material (planned)

- S1: Full 5×5 frequency matrices for all 5 snapshot periods.
- S2: Temporal interval sensitivity (5-year vs. 10-year snapshots).
- S3: Change point detection parameter sensitivity.
- S4: Pipeline code and reproducibility documentation.

---

## References (key entries — not exhaustive)

- Canfield, R.H. (1941). Application of the line intercept method in sampling range vegetation. *Journal of Forestry*, 39(4), 388–394.
- Killick, R., Fearnhead, P., & Eckley, I.A. (2012). Optimal detection of changepoints with a linear computational cost. *Journal of the American Statistical Association*, 107(500), 1590–1598.
- Levy, E.B., & Madden, E.A. (1933). The point method of pasture analysis. *New Zealand Journal of Agriculture*, 46(5), 267–279.
- MapBiomas. (2024). Collection [X] of the Annual Land Use and Land Cover Maps of Brazil. *mapbiomas.org*.
- McGarigal, K., et al. (2012). *FRAGSTATS v4: Spatial Pattern Analysis Program for Categorical and Continuous Maps*. University of Massachusetts.
- Openshaw, S. (1984). *The Modifiable Areal Unit Problem*. Geo Books, Norwich.

---

*Document maintained as part of the EII project. Update after each analytical phase is completed.*
