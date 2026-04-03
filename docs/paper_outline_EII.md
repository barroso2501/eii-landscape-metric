# Paper Outline: Edge Interception Index (EII)
## A Systematic Transect-Based Metric for Landscape Connectivity — Method and Application to the Brazilian Cerrado

**Status:** Working outline — not for submission  
**Target journal (preliminary):** Ecological Indicators  
**Last updated:** 2026-04-02 (rev. 6 — frozen; segment decomposition formalized; gaps resolved)

---

## Proposed Title

**Primary option:**
*"The Edge Interception Index: recovering interface connectivity from the discarded boundaries of regular landscape grids"*

**Alternative:**
*"From area to interface: the Edge Interception Index as a low-cost connectivity complement to grid-based landscape monitoring"*

**Conservative fallback (original):**
*"The Edge Interception Index: a systematic transect-based metric for landscape interface connectivity and its application to four decades of habitat dynamics in the Brazilian Cerrado"*

*Note: title selection deferred to near-submission stage. Primary option is preferred for its directness and positioning.*

---

## Research Questions

**RQ1.** Does the Edge Interception Index — computed from the cell boundaries already present in any grid-based workflow — capture interface connectivity information not accessible to within-cell area metrics alone?

**RQ2.** How do Area and EII diverge in space and time across the study domain, and what landscape processes drive compositional-configurational divergence?

**RQ3.** How robust are EII estimates to grid configuration choices (shape, scale, and placement), and how sensitive are temporal patterns to the choice of sampling interval?

---

## Terminology note

Throughout this document, the term **"compositional-configurational divergence"** replaces earlier uses of "decoupling." Area and EII measure fundamentally distinct dimensions of landscape structure — composition (what is inside a cell) and interface connectivity (how permeable the cell boundary is). Divergence between them is not an anomaly but an informative signal about landscape state. The four quadrants of the Area × EII space are named accordingly:

| Quadrant | Area | EII | Landscape interpretation |
|---|---|---|---|
| Coupled-High | High | High | Intact: abundant interior habitat, connected interface |
| Coupled-Low | Low | Low | Degraded: scarce interior habitat, isolated interface |
| Type I | High | Low | Interior preserved, interface degraded |
| Type II | Low | High | Interior lost, interface still connected |

---

## Abstract (placeholder — write last)

*To be written after Results are complete. Structure: problem → method → data → key result → implication.*

---

## 1. Introduction

### 1.1 Opening hook — the discarded boundary
- Regular grids are widely used in landscape monitoring and analysis: area-based metrics of habitat cover, land-use change statistics, and biodiversity assessments are routinely computed by intersecting raster maps with grid cells and summarizing pixel values within each polygon.
- In every grid-based workflow, the cell boundary — the perimeter of each polygon — is computed as an intermediate geometric object and then discarded after the area calculation is complete.
- We argue that this discarded boundary contains ecologically independent information: treated as a systematic linear transect, the cell perimeter estimates the interface connectivity of each cell with its neighbors — a dimension of landscape configuration that no area-based summary of polygon interiors can capture.
- The computational cost of this additional step is negligible: the grid already exists, the perimeter extraction is a single geometric operation, and the raster sampling uses the same infrastructure as the area calculation.

### 1.2 What the boundary measures that area cannot
- Area metrics capture **composition**: what proportion of natural habitat exists within a spatial unit.
- The cell perimeter, treated as a transect, captures **interface connectivity**: how permeable the boundary of a spatial unit is to habitat continuity with neighboring units.
- Two cells with identical area proportions can differ fundamentally in interface connectivity — one may be embedded in a continuous habitat matrix while the other is already isolated by converted land on all sides. This distinction is invisible to area metrics but ecologically consequential for dispersal, gene flow, and ecosystem function.
- This compositional-configurational divergence is not an anomaly to explain but a signal to detect: it indicates that the two dimensions of landscape state are evolving at different rates, typically as a leading indicator of fragmentation dynamics.

### 1.3 Existing approaches and why they do not fill this gap
- FRAGSTATS-based metrics (patch area, edge density, shape indices): computed from patch mosaics rather than regular grids; do not provide per-cell interface estimates replicable across time series.
- Graph-based connectivity models (circuit theory, least-cost paths): powerful but computationally intensive, require species-specific parameterization, and do not scale easily to biome-wide annual time series.
- Edge density and contrast-weighted edge metrics: landscape-level summaries that do not produce cell-level interface estimates compatible with area metrics computed on the same grid.
- Linear transect methods in vegetation ecology (Canfield 1941; Levy & Madden 1933): well-established estimators of cover from systematic line sampling; their transposition to landscape-scale raster analysis has not been formalized.

### 1.4 The proposed approach
- We formalize the **Edge Interception Index (EII)**: the proportion of a cell's perimeter that intersects natural habitat in a binary raster.
- This is directly analogous to the line intercept method of vegetation ecology (Canfield 1941): the cell boundary is a systematic transect, each pixel contact with natural habitat is a "hit," and the hit rate estimates interface connectivity.
- The hexagonal grid is particularly suited to this approach: six border segments at 60° intervals provide near-isotropic directional sampling, compared to four segments at 90° intervals for square grids.
- EII adds a second column to any existing grid-based analysis: where the first column is area proportion (composition), the second is EII (interface connectivity). The joint distribution of these two columns characterizes landscape state across a two-dimensional space that neither metric spans alone.

### 1.5 Study area and motivation
- A fixed rectangular domain of 1,500 × 1,500 km in central Brazil, encompassing the core Cerrado, the southern Amazon deforestation frontier, the northern Pantanal, and the Cerrado–Caatinga transition zone.
- The Cerrado is one of the world's most threatened savanna biomes, subject to intense and documented agricultural expansion over the past four decades — providing the landscape configuration diversity and temporal dynamics required for a rigorous methodological evaluation.
- MapBiomas annual binary rasters (natural vs. non-natural vegetation, 30 m resolution, 1985–2024) provide the input data, enabling a 40-year annual assessment.

### 1.6 Research questions
*(State RQ1, RQ2, RQ3 as formalized above.)*

### 1.7 Contributions
1. A formal transect-based metric of landscape interface connectivity that adds negligible computational overhead to any existing grid-based workflow, grounded in the line intercept sampling theory of vegetation ecology.
2. A demonstration that the cell boundary — already present in any grid analysis — contains ecologically independent information: compositional-configurational divergence between Area and EII is spatially structured (Moran's I > 0.09 in all 38 years of the effective analysis period, 1986–2023) and grows progressively over four decades of landscape transformation.
3. A systematic treatment of the Modifiable Areal Unit Problem (MAUP) as quantifiable sampling variance: when the grid is treated as a sampling device rather than a spatial partition, MAUP becomes a property to characterize rather than a limitation to acknowledge.

---

## 2. Background

### 2.1 The line intercept method in vegetation ecology
- Canfield (1941): foundational formulation of line intercept sampling for cover estimation.
- Statistical properties: unbiased estimator of cover under random or systematic placement.
- Transposition to landscape scale: border segments as systematic, spatially exhaustive transects. The grid is not merely a spatial partition but a sampling device.

### 2.2 Composition vs. configuration in landscape ecology
- McGarigal & Marks (1995): foundational distinction between landscape composition (what is present) and configuration (how it is arranged spatially).
- Area metrics capture composition. EII captures configuration at the interface level.
- Gap: no existing metric simultaneously captures (a) systematic spatial coverage, (b) temporal replicability at annual resolution, and (c) interface-level configuration.

### 2.3 The Modifiable Areal Unit Problem in landscape ecology
- Classical MAUP: scale effect and zoning effect.
- Existing treatments: typically acknowledged as a caveat, rarely quantified.
- Reframing: when the grid is treated as a sampling device, MAUP becomes sampling variance — a quantity that can be estimated and reported.

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
- MapBiomas Collection 10.1 (Souza Jr. et al. 2020; MapBiomas 2026), 30 m resolution, 1985–2024.
- Binarization: natural vegetation (value 1) vs. non-natural (value 0); outside-domain pixels encoded as 255 (nodata).
- Annual time series: 40 raster layers available; **38 years used in primary analyses** (1986–2023; see below).
- **Technical note on nodata encoding:** raster metadata declares nodata=0, but 0 = non-natural vegetation (valid data). All EII and Area calculations use nodata=255 to correctly include non-natural pixels in the denominator.
- Rationale for binary classification: focus on habitat presence/absence rather than vegetation type diversity.

**Exclusion of boundary years (1985 and 2024):**

The MapBiomas post-classification filtering pipeline applies temporal moving-window filters (3-, 4-, and 5-year windows) to remove spurious transitions between land cover classes. At the boundaries of the time series, these windows operate with truncated information — years before 1985 and after 2024 do not exist — reducing filter effectiveness. Several correction rules are explicitly restricted to years 1986–2023 to avoid this artifact: *"These rules are applied only in the middle of the series (1986–2023) to avoid border years"* (MapBiomas 2026, ATBD Collection 10.1, Section 3.4.3.3). As a consequence, the 1985 and 2024 maps contain higher transitional noise relative to intermediate years.

Both years are retained in the dataset and their values are reported separately for reference, but primary analyses use the effective period **1986–2023 (38 annual maps)**. The values for 1985 and 2024 differ only marginally from their adjacent years (< 1 percentage point in all aggregated metrics), confirming that the exclusion does not introduce discontinuities in the reported trends.

### 3.3 Grid design

**Projection and domain:**
- All grids generated in ESRI:102033 (South America Albers Equal Area Conic), ensuring equal-area cells throughout the domain.
- Grid extent: the 1,500 × 1,500 km rectangular domain. All cells fully contained within the domain — no boundary clipping applied.

**Primary configuration — hexagonal grid, 20,000 ha:**
- Cell area: 20,000 ha (200 km²); side length: ~15.2 km; diagonal: ~26.2 km; actual cells: 11,500.
- Rationale for hexagonal geometry: six border segments at 0°, 60°, 120°, 180°, 240°, 300° provide near-isotropic directional sampling, compared to four segments at 0°, 90°, 180°, 270° for square grids.
- Rationale for 20,000 ha as primary scale: (1) ecologically interpretable as the watershed / small-municipality scale; (2) perimeter length (~54 km) provides sufficient pixel contacts for estimator stability; (3) alignment with territorial planning scales commonly used in Brazilian conservation policy.

**Scale sensitivity configurations:**

| Configuration | Cell area | Side length | Actual cells | Ecological scale |
|---|---|---|---|---|
| Fine | 10,000 ha | ~10.7 km | 22,842 | Property / forest fragment |
| **Primary** | **20,000 ha** | **~15.2 km** | **11,500** | **Watershed / small municipality** |
| Coarse | 40,000 ha | ~21.5 km | 5,822 | Regional mosaic / corridor |

- Scale ratio: ×2 in side length, ×4 in area between consecutive levels.
- Hexagonal grids do not nest perfectly across scales; scale comparisons are treated as independent configurations.

**Shape sensitivity configuration — square grid:**
- Cell area: 20,000 ha; side length: ~14.1 km; actual cells: 11,449.
- Note: equal area implies unequal perimeter (P_square ≈ 56.6 km vs. P_hexagon ≈ 54.4 km); reported explicitly (see Section 3.7.1).

### 3.4 EII formalization

**Within-cell area metric (composition):**

$$A_i(t) = \frac{\sum_{p \in C_i} \mathbf{1}[r_p(t) = 1]}{|C_i|}$$

where $C_i$ is the set of valid pixels within cell $i$, $r_p(t)$ is the binary raster value of pixel $p$ at time $t$, and $|C_i|$ is the total count of valid pixels. Computed using `zonal_stats` with `stats=['count','sum']` on polygon interiors (`all_touched=False`).

**Edge Interception Index — aggregated (interface connectivity):**

$$w_i(t) = \frac{L_i^{\text{nat}}(t)}{P_i^{\text{obs}}(t)}$$

where $L_i^{\text{nat}}(t)$ is the count of perimeter pixels intercepting natural habitat at time $t$, and $P_i^{\text{obs}}(t)$ is the total count of valid perimeter pixels. Computed using `zonal_stats` with `categorical=True`, `all_touched=True` on perimeter (boundary) geometries.

Both metrics $\in [0, 1]$.

**Critical note on computation and cell boundaries:**

The EII is computed from the cell's own perimeter intersecting the raster. It does not require the existence or state of neighboring cells — the raster provides pixel values independently of the grid topology. This has two important consequences:

1. *Border cells are treated identically to interior cells.* A cell at the edge of the study domain has the same six segments as an interior cell; each segment samples whatever pixel values exist in the raster at that location. No completeness correction or exclusion is required.

2. *The calculation is independent, but adjacent results are structurally correlated.* Although each cell's EII is computed independently, neighboring cells sample adjacent (and partially overlapping) sets of raster pixels along their shared boundary. This structural correlation must be accounted for in spatial autocorrelation analyses (see Section 3.9).

**EII decomposed by segment:**

Each hexagonal cell has six border segments at fixed orientations: 0°, 60°, 120°, 180°, 240°, 300°. The EII can be decomposed into a vector of six component values:

$$\mathbf{w}_i(t) = [w_{i1}(t),\ w_{i2}(t),\ w_{i3}(t),\ w_{i4}(t),\ w_{i5}(t),\ w_{i6}(t)]$$

where $w_{ij}(t) \in [0,1]$ is the proportion of segment $j$ of cell $i$ intercepting natural habitat at time $t$.

The aggregated EII is the length-weighted mean of the six components (equivalent to the ratio of total natural contacts to total valid perimeter pixels). For hexagonal cells with equal side lengths, this reduces to the arithmetic mean:

$$w_i(t) = \frac{1}{6} \sum_{j=1}^{6} w_{ij}(t)$$

The **total interface connectivity** — the sum of the six components — has a distinct geometric interpretation:

$$\Sigma w_i(t) = \sum_{j=1}^{6} w_{ij}(t) \in [0, 6]$$

This represents the total length of connected interface expressed in units of full segments: a cell with $\Sigma w_i = 4.8$ has the equivalent of 4.8 fully connected sides, regardless of how that connectivity is distributed across the six directions. The aggregated EII relates to the total by $w_i = \Sigma w_i / 6$.

**Five geometric properties of the segment vector:**

| Property | Formula | Interpretation |
|---|---|---|
| 1. Total connectivity | $\Sigma w_i = \sum_j w_{ij}$ | Total connected interface in segment units [0, 6] |
| 2. Mean connectivity | $\bar{w}_i = \Sigma w_i / 6$ | Aggregated EII [0, 1] |
| 3. Isotropy | $\text{SD}(w_{ij})$ | Low = isotropic; high = directional connectivity |
| 4. Directional gradient | $w_{ij} - w_{i,j+3}$ | Connectivity asymmetry between opposite sides (3 pairs) |
| 5. Topological role | $N_k = \sum_j \mathbf{1}[w_{ij} > \tau]$ | Number of functionally connected sides above threshold $\tau$ |

Properties 3 and 4 are analysed in Section 3.11 (segment decomposition analysis). Property 5 connects to graph-theoretic characterization of cells (hub, corridor, dead-end, isolate) — reserved for future work.

**Connection to the line intercept method:**
- Each of the six border segments constitutes a systematic transect.
- Each pixel contact with natural habitat is a "hit."
- $w_{ij}(t)$ is the hit rate along segment $j$ — directly analogous to the cover estimator of Canfield (1941).
- The six segments at 60° intervals provide near-isotropic directional sampling of the landscape around each cell.

**Compositional-configurational divergence:**

$$\delta_i(t) = w_i(t) - A_i(t)$$

$\delta_i > 0$: interface more connected than interior composition suggests.  
$\delta_i < 0$: interface more degraded than interior composition suggests.  
$\delta_i = 0$: composition and interface connectivity aligned.

### 3.5 Annual time series construction
- EII and Area computed for all 40 years (1985–2024): two matrices of dimensions 11,500 cells × 40 years.

### 3.6 Temporal interval selection and sensitivity
- Primary analysis: annual resolution (1985–2024).
- Snapshot analysis: intervals anchored to documented deforestation regimes:
  - 1985 (baseline), 1995, 2004 (historical peak deforestation), 2012 (new Forest Code), 2020, 2024.
- Sensitivity test: comparison of results under 5-year vs. 10-year snapshot intervals.

### 3.7 Sensitivity to grid configuration (MAUP)

**3.7.1 Shape effect: hexagon vs. square**

Comparison structured across three explicit dimensions:

- **Dimension 1 — Aggregated distribution convergence:** 5×5 Area × EII matrices compared between HEX-20 and SQ-20. *Result (preliminary): maximum difference < 0.008 across all quadrants in both 1985 and 2020.*
- **Dimension 2 — Estimator variance per unit area:** CV of EII compared between HEX-20 and SQ-20. *Result (preliminary): CV_hex < CV_sq, consistent with hexagon's superior isoperimetric efficiency.*
- **Dimension 3 — Directional isotropy:** hexagon samples 6 × 60° directions; square samples 4 × 90° directions. Analytical argument — no additional empirical test required.

**3.7.2 Scale effect: multi-resolution comparison**
- EII and Area distributions compared across HEX-10, HEX-20, HEX-40.
- *Result (preliminary): mean EII differs by < 0.001 across scales in both 1985 and 2020; scale effect on aggregated distributions is negligible.*

**3.7.3 Zoning effect: systematic grid displacement**
- 25 realizations: 8 directions × 3 distances (1/6, 1/3, 1/2 of side length) + original.
- *Result (preliminary): mean EII varies by < 0.005 across 25 realizations; CV across realizations < 0.003. EII estimates are highly robust to grid placement.*

### 3.8 Change point detection
- Algorithm: PELT (Killick et al. 2012) applied independently to each cell's annual EII and Area series.
- Implementation: Python `ruptures` library; penalty parameter via BIC.
- Output: year(s) of structural break per cell for EII ($t^*_w$) and Area ($t^*_A$); temporal lag $\Delta_i = t^*_w - t^*_A$.
- **Status:** Planned analysis — not yet executed. Results will appear in Section 4.5 when complete. This is the only remaining Phase 3 analysis that requires substantial computation (11,500 independent time series). See roadmap step 3.5.

### 3.9 Spatial autocorrelation of compositional-configurational divergence

**Variable selection — why divergence and not EII directly:**

Although the EII of each cell is computed independently from its own perimeter (see Section 3.4), neighboring cells sample adjacent and partially overlapping sets of raster pixels along their shared boundary segment. This creates structural spatial correlation in the EII values of adjacent cells — even in a random landscape, neighboring cells would show similar EII values simply because they sample the same pixels from opposite sides of the same boundary.

Computing Moran's I directly on EII would therefore produce inflated autocorrelation coefficients that reflect geometric overlap in the sampling design rather than true spatial clustering of landscape states. This is a consequence of the shared-boundary property of the hexagonal grid, not of any ecological pattern.

The compositional-configurational divergence $\delta_i(t) = w_i(t) - A_i(t)$ is not subject to this artifact. The divergence between interface connectivity and interior composition depends on the specific arrangement of habitat relative to both the interior and the boundary of each individual cell. Two neighboring cells may have similar EII values (because they share boundary pixels) but very different divergence values (because their interior compositions differ independently). Moran's I on the divergence variable tests whether cells in similar landscape states — where composition and interface connectivity are misaligned — tend to be spatially clustered, which is the ecologically relevant question and is free from the structural correlation artifact.

**Implementation:**
- Variable: binary classification — divergent (Type I or Type II = 1) vs. coupled (Coupled-High or Coupled-Low = 0) per cell per year.
- Spatial weights: Queen contiguity (cells sharing at least one vertex), row-standardized.
- Test: Global Moran's I with 99 permutations for significance assessment.
- Applied annually to the full 1985–2024 series.

**Additional outputs:**
- Moran's I time series: trend in spatial clustering of divergence over 40 years.
- Cumulative divergence trace: cells ever in Type I or Type II state across the full series (binary map and % years in divergent state per cell).

### 3.10 Continuous divergence analysis (δ)
- Annual distribution of $\delta_i(t)$ across cells.
- Metrics: mean, median, SD, P10, P25, P75, P90; % cells with δ < 0, δ > 0, |δ| < 0.05.

### 3.11 Segment decomposition analysis

This analysis uses the six individual segment values $w_{ij}$ rather than the aggregated EII. It characterizes the **directional structure of interface connectivity** for each cell, independently of the area metric.

**3.11.1 — Connectivity anisotropy (Property 3)**

For each cell $i$ and year $t$:

$$\text{Aniso}_i(t) = \text{SD}(w_{i1}, w_{i2}, w_{i3}, w_{i4}, w_{i5}, w_{i6})$$

- $\text{Aniso}_i = 0$: all six sides have identical connectivity — perfectly isotropic cell.
- High $\text{Aniso}_i$: connectivity is concentrated in specific directions — the cell lies at a directional landscape feature (corridor, edge, ecotone).

Outputs:
- Spatial map of mean anisotropy per cell across the full series.
- Annual mean anisotropy for the domain — temporal trend.
- Cells with persistently high anisotropy across years identify stable directional landscape features.

**3.11.2 — Directional gradients (Property 4)**

The six segments of a hexagon form three pairs of geometrically opposite sides. Each pair defines a directional axis. For each axis $k \in \{1, 2, 3\}$:

$$G_{ik}(t) = w_{ij}(t) - w_{i,j+3}(t)$$

where $j$ and $j+3$ are opposite segments on axis $k$.

- $G_{ik} > 0$: connectivity higher on the "positive" side of axis $k$ than on the opposite side.
- $G_{ik} = 0$: symmetric connectivity along axis $k$.
- $G_{ik} < 0$: connectivity higher on the "negative" side.

The direction of maximum gradient identifies the **orientation of the connectivity transition** at each cell — for example, a cell at an active deforestation front advancing from south to north would show $G_{i,\text{N-S}} < 0$ (connectivity declining towards the south).

Outputs:
- Three gradient maps per year (one per axis).
- Vector field of dominant gradient direction per cell — reveals large-scale orientation of transformation fronts.
- Temporal change in gradient magnitude: cells where gradients intensify over time are at advancing transformation frontiers.

**Note on independence from Area:**

Both analyses (3.11.1 and 3.11.2) use exclusively the six segment values $w_{ij}$ with no reference to the within-cell area metric $A_i$. They characterize the geometric structure of interface connectivity as an independent dimension of landscape state — consistent with the goal of demonstrating the informational value of the EII beyond its relationship with composition metrics.

---

## 4. Results

### 4.1 EII as a complementary information source (RQ1)

**EII × Area correlation:**
- Pearson r stable at 0.960–0.966 across all 38 years (1986–2023); Spearman ρ follows closely.
- R² ranges from 0.922 (1986) to 0.933 (peak ~2000–2004) to 0.928 (2023) — Area explains ~92–93% of variance in EII throughout the series.
- Variance in EII not explained by Area (1−R²): 7.7% in 1986, minimum ~6.7% in 2000–2004, 7.2% in 2023. The U-shaped trajectory is ecologically interpretable: at peak conversion (2000–2005), cells losing area were losing EII proportionally; before and after, the relationship is more heterogeneous.
- With N=11,500 cells, 7% unexplained variance represents ~800 cells per year where EII carries information structurally distinct from Area.

**Residual analysis:**

| Year | Residual SD | \|resid\| > 0.05 | \|resid\| > 0.10 |
|---|---|---|---|
| 1986 | 0.053 | 24.1% of cells | 8.0% of cells |
| 2023 | 0.074 | 41.0% of cells | 16.4% of cells |

Cells where EII provides substantial additional information (|residual| > 0.10) doubled from 8% to 16% between 1986 and 2023 — direct evidence that the informational value of EII relative to Area grew over the study period as landscape heterogeneity increased.

**Divergence distribution:**
- In 1986, 75.4% of cells had |δ| < 0.05; by 2023, this fell to 58.7% — the domain became progressively more heterogeneous in the composition-configuration space.
- Frequency of Type I and Type II states grew from 2.8% (1986) to 8.2% (2023).

### 4.2 Compositional-configurational divergence dynamics (RQ2)
- Annual flux of the four landscape states (1986–2023).
- *Preliminary result (1986→2023): Coupled-High declined from 90.8% to 58.4%; Coupled-Low increased from 6.5% to 33.4%; total Type I + Type II increased from 2.8% to 8.2%.*
- Temporal trend of δ: negative tail (P10) widening from −0.060 (1986) to −0.094 (2023); % cells with δ < 0 increasing from 41.7% to 47.0%.
- Moran's I: *significant in all 38 years of the effective period (p < 0.01); I ranging from 0.094 to 0.136 — divergent states are spatially clustered throughout the series.*
- Cumulative divergence trace: cells ever in Type I or Type II state across the full series.

### 4.3 Domain-scale dynamics — snapshot analysis (RQ2)

**5×5 Area × EII frequency matrices — observed results:**

| Year | Coupled-High (80-100% both) | Coupled-Low (0-40% both) | Diagonal mass | Off-diagonal |
|---|---|---|---|---|
| 1986 | 69.8% | ~0.7% | ~88% | ~12% |
| 1995 | ~56.1% | ~1.3% | ~82% | ~18% |
| 2004 | ~63.5% | ~3.0% | ~80% | ~20% |
| 2012 | ~37.7% | ~4.1% | ~72% | ~28% |
| 2020 | ~33.4% | ~5.3% | ~68% | ~32% |
| 2023 | ~30.7% | ~6.5% | ~67% | ~33% |

*Note: full 5×5 matrices with all 25 cell values available in Supplementary S1.*

The dominant pattern is a progressive shift of mass from the top-right corner (Coupled-High — intact landscape) toward the bottom-left (Coupled-Low — degraded landscape) and toward off-diagonal cells (compositional-configurational divergence). The 2004 matrix shows a transient concentration pattern during peak conversion, followed by continued redistribution toward lower ranges.

**Difference matrices between consecutive periods:**
- 1986→1995: largest losses in Coupled-High; first appearance of off-diagonal mass.
- 1995→2004: continuation of mass transfer toward intermediate and lower bins.
- 2004→2012: acceleration — off-diagonal mass and Coupled-Low grow substantially.
- 2012→2020 and 2020→2023: slower rate of change, consistent with post-PPCDAM landscape stabilization.

**Temporal interval sensitivity:**
Snapshot years 1986 and 2023 are identical under both 5-year and 10-year sampling schemes (by definition). The intermediate trajectories are consistent across sampling intervals — the choice of 5-year vs. 10-year snapshots does not materially alter the interpretation of matrix evolution. Reported in Supplementary S2.

### 4.4 Grid configuration sensitivity (RQ3)
- Shape: HEX-20 vs. SQ-20 — three-dimensional comparison (convergence, estimator variance, isotropy).
- Scale: HEX-10 / HEX-20 / HEX-40 — negligible effect on aggregated distributions.
- Jitter: mean EII range < 0.005 across 25 realizations; CV < 0.003.

### 4.5 Change point detection — EII structural breaks (RQ2)

**Algorithm and parameterization:**
PELT applied to EII annual series only (Paper 1 scope). Two modes run in parallel:
- *Mode A:* Binseg with n_bkps=1 — identifies the single dominant structural break per cell. Used for spatial mapping and temporal characterization of the primary rupture event.
- *Mode B:* Pelt with pen=3.0 — detects multiple breaks automatically. Penalty selected empirically from sensitivity analysis on a 500-cell subsample: pen=1.5 over-segments (45% of cells with 3+ breaks); pen=6.0 artificially converges toward Mode A (75% with 1 break); pen=3.0 produces a naturally balanced distribution (14% with 0 breaks, 34% with 1, 50% with 2, 2% with 3+), appropriately separating structural breaks from noise in EII series with variance range 0.001–0.04.

**Study domain context:**
The 1,500 × 1,500 km rectangular domain encompasses approximately 50% Cerrado and 50% Amazon (specifically the arc of deforestation), with marginal areas of Pantanal and Caatinga. The landscape dynamics observed therefore reflect both Cerrado agricultural frontier expansion and Amazon deforestation, with documented policy interventions (PPCDAM, launched 2004; Soy Moratorium, 2006) operating primarily on the Amazon portion of the domain.

**Mode A results — primary structural break:**
- Valid cells: 11,500 (all cells — no NaN in dataset)
- Changepoint year range: 1990–2020; median: 2000; mean: 2003
- ΔEII (after − before): mean = −0.141; cells with decline: ~88%
- Distribution by period:

| Period | Cells | % | ΔEII mean | % negative |
|---|---|---|---|---|
| 1990–1994 | 222 | 1.9% | — | — |
| 1995–1999 | 1,992 | 17.3% | −0.171 | 89% |
| 2000–2004 | 3,660 | 31.8% | −0.177 | 88% |
| 2005–2009 | 2,551 | 22.2% | −0.174 | 94% |
| 2010–2014 | 2,558 | 22.2% | −0.059 | 52% |
| 2015–2019 | 458 | 4.0% | −0.060 | 83% |
| 2020–2023 | 78 | 0.7% | −0.055 | 90% |

**Mode B results — multiple break structure:**
- 0 breaks: ~14% of cells (stable connectivity throughout series — concentrated in protected areas and already-converted landscapes with no margin for further decline)
- 1 break: ~34% of cells
- 2 breaks: ~50% of cells (dominant pattern — consistent with two distinct pulses of landscape pressure)
- 3+ breaks: ~2% of cells

**Ecological interpretation:**

*Temporal pattern:* The peak of structural breaks in EII falls between 1995 and 2009 (71% of all breaks), coinciding with the documented period of maximum deforestation rates in both the Cerrado and the Amazon arc of deforestation. The sharp attenuation in break intensity after 2010 — with ΔEII declining from −0.177 to −0.059 and the proportion of negative breaks falling from 88–94% to 52% in the 2010–2014 period — is consistent with the policy effects of the Amazon Deforestation Prevention Plan (PPCDAM, 2004) and the Soy Moratorium (2006), which substantially reduced deforestation rates in the Amazon portion of the domain. The 52% negative rate in 2010–2014 (vs. 88–94% before) represents the quantitative signature of this policy-driven transition.

*Spatial pattern:* The ΔEII spatial map shows near-zero values in protected areas and indigenous territories (connectivity unchanged) and strongly negative values along documented deforestation frontiers. The small number of cells with positive ΔEII (EII increase after break) is concentrated in the Pantanal margin, where hydrological dynamics produced areas of vegetation gain as water bodies contracted and were recolonized by native vegetation — a distinct ecological process unrelated to agricultural conversion.

*Two-pulse structure:* The dominance of 2-break cells in Mode B is ecologically interpretable as two successive pulses of landscape pressure: an earlier pulse (1995–2005, high-intensity conversion) and a later pulse (2005–2015, consolidation of agricultural frontier or new fronts in MATOPIBA), separated by a period of slower transformation following policy interventions.

*EII as an independent detector:* These temporal and spatial patterns were detected exclusively from the EII time series, without auxiliary information on governance, policy, or land use regulation. The concordance with independently documented deforestation history constitutes an external ecological validation of the metric.

### 4.6 Segment decomposition — anisotropy and directional gradients (RQ1)
- **Relationship to RQ1:** treated as an exploratory extension of RQ1. The segment decomposition characterizes the internal structure of the EII independently of the area metric — demonstrating additional informational dimensions of the EII beyond the aggregated scalar. It does not constitute a separate RQ but substantially deepens the answer to RQ1.
- **Threshold note:** the 0.5 threshold used throughout the state classification (Sections 4.1–4.2) is provisional. Sensitivity to this threshold will be reported in Supplementary S2.
- **Note on anchor years:** spatial maps use 1985 and 2024 (full dataset range); temporal statistics use 1986–2023 (effective analysis period). Maps of 1985 and 2024 are interpretable but may contain residual classification noise due to truncated temporal filters (see Section 3.2).

**4.6.1 — Connectivity anisotropy**

- For each cell and year: $\text{Aniso}_i(t) = \text{SD}(w_{i1},...,w_{i6})$.
- *Observed result — temporal trend (1986–2023):* mean anisotropy increased monotonically from 0.086 (1986) to 0.143 (2023), a 66% increase. The P25 grew 13-fold (0.006 → 0.072), indicating that cells which were nearly isotropic in 1986 developed substantial directional asymmetry by 2023. The IQR widened throughout, reflecting increasing landscape heterogeneity in the connectivity structure.
- *Observed result — spatial pattern (2024 map):* cells with low anisotropy (near zero) co-locate with protected areas and indigenous territories — where habitat is preserved on all sides of the cell and connectivity is isotropic. Cells with high anisotropy (SD > 0.25) concentrate at the boundaries of these protected areas — where one or more sides face a converted matrix while opposite sides remain connected. This spatial co-location with known conservation boundaries constitutes an independent ecological validation of the segment decomposition method: the metric identifies ecotones and transition zones without any auxiliary spatial information.

**4.6.2 — Directional gradients**

- Three gradient maps per year (E-W, NE-SW, NW-SE axes); dominant gradient direction per cell.
- *Observed result — temporal evolution:* gradient magnitude increased substantially between 1985 and 2024 across all three axes. Scale of dominant gradients expanded from ±0.4 (1985) to ±0.6 (2024), reflecting intensification of directional asymmetry as landscape conversion advanced. In 1985, gradient patterns were sparse and dispersed — the landscape was relatively homogeneous. By 2005, spatially coherent clusters emerged with protected areas visible as low-gradient islands. By 2024, the spatial structure was consolidated with large contiguous blocks of directionally biased cells.
- *Observed result — directional dominance:* the NE-SW axis (60°–240°) consistently shows the strongest gradients across years — coherent with the known northeast-to-southwest orientation of the agricultural expansion frontier in the MATOPIBA region. The E-W axis shows weaker and more fragmented patterns. This directional signature is detected exclusively from the six segment values, without any auxiliary information about deforestation vectors.
- *Observed result — protected area signature:* large white blocks (near-zero gradients in all axes) in 2005 and 2024 maps correspond to protected areas and indigenous territories. Their boundaries are sharply delineated by the gradient maps — a second independent spatial validation of the segment decomposition.

**Pipeline validation note:**

The segment-level EII (mean of six components) differs from the full-perimeter EII (Phase 2) by a mean of 0.003 ± 0.005 across all cells and years. This systematic offset is explained by the double-counting of the six vertex pixels — one per hexagonal vertex — which are captured by both adjacent segments when geometries are computed separately. This is a known geometric property of the decomposition, documented here for reproducibility. The full-perimeter EII (Phase 2) is used as the primary aggregated metric throughout the paper; segment values are used exclusively for directional analyses (Sections 4.6.1 and 4.6.2).

### 4.7 Temporal interval sensitivity (RQ3)
- Snapshot years 1986 and 2023 are identical under both 5-year and 10-year sampling intervals by definition. Intermediate trajectories are consistent across schemes — the choice of sampling interval does not materially alter the interpretation of Area × EII matrix evolution. Full comparison reported in Supplementary S2.

---

## 5. Discussion

### 5.1 EII as a compositional-configurational divergence detector
- Area and EII measure different dimensions of landscape structure: composition (interior) and interface connectivity (boundary). Their divergence is not anomalous but informative.
- Type I cells (high area, low EII): interior habitat preserved but boundary isolation already advanced — potential matrix-surrounded remnants.
- Type II cells (low area, high EII): interior largely converted but still embedded in a connected matrix — landscapes in early-stage conversion.
- Both types increase over time and are spatially clustered (Moran's I > 0.09 throughout), confirming that divergence is not noise but a structured spatial signal associated with active transformation frontiers.

### 5.2 The δ signal and its ecological interpretation
- The negative tail of the δ distribution widens progressively — interface connectivity degrades faster than interior area in a growing fraction of cells.
- Hypothesis: edge-in conversion dynamics produce Type I states as the leading edge of fragmentation, before interior loss is detectable by area metrics.
- This positions EII as an early-configuration indicator complementary to area metrics.

### 5.3 MAUP reframed as sampling variance
- The grid as a sampling device: spatial uncertainty is quantifiable (CV < 0.003 across 25 jitter realizations) and ecologically interpretable.
- Regions of high jitter instability — if present — would locate abrupt landscape boundaries, not methodological artifacts.
- Hexagonal grids are preferable to square grids: lower estimator variance per unit area, greater directional isotropy.

### 5.4 Methodological scope and transferability
- Raster-agnostic: applicable to any binary habitat map at any resolution.
- Scalable: checkpoint-based pipeline processes 40 annual rasters in a single run.
- Limitations: EII measures perimeter-level connectivity, not functional connectivity; does not account for species-specific dispersal; requires hardcoded nodata handling when raster metadata encoding is ambiguous.

### 5.5 Connections to existing literature
- Relationship to composition/configuration distinction (McGarigal & Marks 1995): Area = composition estimator; EII = configuration estimator at interface level.
- Relationship to edge density metrics (FRAGSTATS): EII is boundary-referenced and cell-scale rather than patch-referenced and landscape-scale.
- Relationship to graph-based connectivity: EII weights ($w_{ij}$) can serve directly as edge weights in a spatial graph — future work.

### 5.6 The segment vector as a directional landscape descriptor
- The decomposition of EII into six directional components reveals information not available in the aggregated scalar: anisotropy identifies cells at directional landscape features (corridors, ecotones, advancing frontiers); directional gradients locate and orient active transformation zones.
- These properties are intrinsic to the hexagonal geometry — they emerge from the six fixed orientations of the border segments and require no additional parameterization.
- The segment vector implicitly defines a spatial graph on the landscape: cells are nodes, shared boundaries are edges, and the component EII values are natural edge weights. This graph is latent in any hexagonal grid analysis; the segment decomposition makes it explicit.
- Connection to future work: the full graph-theoretic analysis (connected components, betweenness, corridor identification) is reserved for Paper 2.

---

## 6. Conclusions

- The Edge Interception Index, grounded in the line intercept sampling theory of vegetation ecology, provides an efficient and interpretable metric of landscape interface connectivity from any binary raster time series.
- Area and EII capture complementary dimensions — composition and interface connectivity — and their divergence characterizes landscape states that area metrics cannot distinguish.
- Applied to 38 years of habitat dynamics in central Brazil (1986–2023), EII reveals a progressive widening of compositional-configurational divergence, spatially structured along active transformation frontiers (Moran's I significant in all years, I = 0.094–0.136).
- MAUP effects are quantifiable as sampling variance (CV < 0.003) and the method is robust across shape, scale, and placement choices.

---

## Figures (planned)

| Figure | Content | Source |
|---|---|---|
| **Fig. 1** | Conceptual diagram: hexagonal cell, perimeter as transect, six segments, pixel contacts, δ definition | Illustration |
| **Fig. 2** | Example cells in each of the four quadrants of Area × EII space | MapBiomas tiles |
| **Fig. 3** | Annual flux of four landscape states (1985–2024) + cumulative divergence trace map | Sections 4.1, 4.2 |
| **Fig. 4** | Annual δ distribution: trend (mean ± IQR), violin for selected years | Section 4.2 |
| **Fig. 5** | Moran's I over time + spatial maps of Area, EII, and δ for 1985 and 2024 | Sections 4.2, 4.3 |
| **Fig. 6** | MAUP sensitivity: jitter stability, hex vs. square, scale comparison | Section 4.4 |
| **Fig. 7** | Segment decomposition: anisotropy map + directional gradient vector field | Section 4.6 |

---

## Supplementary Material (planned)

- S1: Full 5×5 frequency matrices for all snapshot periods.
- S2: Threshold sensitivity (0.5 midpoint vs. quantile-based classification) for state assignments.
- S3: Change point detection parameter sensitivity (BIC penalty variants).
- S4: Pipeline code and reproducibility documentation.

---

## Status at freeze

**FROZEN — 2026-04-03 (final)**
**Effective analysis period:** 1986–2023 (38 years; 1985 and 2024 excluded per MapBiomas ATBD Section 3.4.3.3)
**All analyses complete:**
- Phase 1: MAUP sensitivity (shape, scale, jitter)
- Phase 2: Annual EII + Area time series, divergence analysis (δ, states, Moran's I)
- Phase 3: Segment decomposition (anisotropy, directional gradients), change point detection (Mode A + B, penalty sensitivity)
- Closing analyses: EII × Area correlation, 5×5 frequency matrices, temporal interval sensitivity

**Pending before submission (writing and figures only):**
- Sections 3.x Methods writing (priority: 3.4 EII formalization)
- Publication-quality figures (Figs. 1–7)
- Abstract (write last)

**Open parameter:** divergence threshold (0.5 provisional; sensitivity reported in Supplementary S2).

---

## References (key entries — not exhaustive)

- Canfield, R.H. (1941). Application of the line intercept method in sampling range vegetation. *Journal of Forestry*, 39(4), 388–394.
- Killick, R., Fearnhead, P., & Eckley, I.A. (2012). Optimal detection of changepoints with a linear computational cost. *Journal of the American Statistical Association*, 107(500), 1590–1598.
- Levy, E.B., & Madden, E.A. (1933). The point method of pasture analysis. *New Zealand Journal of Agriculture*, 46(5), 267–279.
- MapBiomas. (2026). *Algorithm Theoretical Basis Document (ATBD) — MapBiomas Collection 10.1, Version 1*. February 2026. mapbiomas.org.
- MapBiomas. (2024). Collection 10.1 of the Annual Land Use and Land Cover Maps of Brazil. *mapbiomas.org*.
- McGarigal, K., & Marks, B.J. (1995). *FRAGSTATS: Spatial Pattern Analysis Program for Quantifying Landscape Structure*. USDA Forest Service.
- Openshaw, S. (1984). *The Modifiable Areal Unit Problem*. Geo Books, Norwich.
- Souza Jr., C.M. et al. (2020). Reconstructing three decades of land use and land cover changes in Brazilian biomes with Landsat archive and Earth Engine. *Remote Sensing*, 12(17), 2735.

---

*Document maintained as part of the EII project. Update after each analytical phase is completed.*
