# Paper Outline: Edge Interception Index (EII)
## A Systematic Transect-Based Metric for Landscape Connectivity — Method and Application to the Brazilian Cerrado

**Status:** Working outline — not for submission  
**Target journal (preliminary):** Ecological Indicators  
**Last updated:** 2026-04-02 (rev. 5 — Introduction reframed around low-cost grid complement hook)

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
2. A demonstration that the cell boundary — already present in any grid analysis — contains ecologically independent information: compositional-configurational divergence between Area and EII is spatially structured (Moran's I > 0.09 in all years) and grows progressively over four decades of landscape transformation.
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
- MapBiomas Collection [X], 30 m resolution, 1985–2024.
- Binarization: natural vegetation (value 1) vs. non-natural (value 0); outside-domain pixels encoded as 255 (nodata).
- Annual time series: 40 raster layers.
- **Technical note on nodata encoding:** raster metadata declares nodata=0, but 0 = non-natural vegetation (valid data). All EII and Area calculations use nodata=255 to correctly include non-natural pixels in the denominator.
- Rationale for binary classification: focus on habitat presence/absence rather than vegetation type diversity.

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
- Correlation between $A_i(t)$ and $w_i(t)$ across cells and time periods.
- Distribution of $\delta_i(t)$: % cells near zero, widening of distribution over time.
- Frequency of Type I and Type II states across the time series.
- *Preliminary result: in 1985, 75.8% of cells had |δ| < 0.05; by 2024, this fell to 58.5% — the domain became progressively more heterogeneous in the composition-configuration space.*

### 4.2 Compositional-configurational divergence dynamics (RQ2)
- Annual flux of the four landscape states (1985–2024).
- *Preliminary result: Coupled-High declined from 91.5% to 57.6%; total Type I + Type II increased from 2.5% to 8.4%.*
- Temporal trend of δ: cauda negativa (P10) widening from −0.061 to −0.093; % cells with δ < 0 increasing from 41.8% to 46.9%.
- Moran's I: *significant in all 40 years (p < 0.01); I ranging from 0.094 to 0.136 — divergent states are spatially clustered throughout the series.*
- Cumulative divergence trace: cells ever in Type I or Type II state across the full series.

### 4.3 Domain-scale dynamics — snapshot analysis (RQ2)
- 5×5 Area × EII frequency matrices for anchored snapshots.
- Difference matrices between periods.

### 4.4 Grid configuration sensitivity (RQ3)
- Shape: HEX-20 vs. SQ-20 — three-dimensional comparison (convergence, estimator variance, isotropy).
- Scale: HEX-10 / HEX-20 / HEX-40 — negligible effect on aggregated distributions.
- Jitter: mean EII range < 0.005 across 25 realizations; CV < 0.003.

### 4.5 Temporal interval sensitivity (RQ3)
- Comparison of 5-year vs. 10-year snapshot matrices.

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

---

## 6. Conclusions

- The Edge Interception Index, grounded in the line intercept sampling theory of vegetation ecology, provides an efficient and interpretable metric of landscape interface connectivity from any binary raster time series.
- Area and EII capture complementary dimensions — composition and interface connectivity — and their divergence characterizes landscape states that area metrics cannot distinguish.
- Applied to 40 years of habitat dynamics in central Brazil, EII reveals a progressive widening of compositional-configurational divergence, spatially structured along active transformation frontiers (Moran's I significant in all years).
- MAUP effects are quantifiable as sampling variance (CV < 0.003) and the method is robust across shape, scale, and placement choices.

---

## Figures (planned)

| Figure | Content | Source |
|---|---|---|
| **Fig. 1** | Conceptual diagram: hexagonal cell, perimeter transect, pixel contacts, δ definition | Illustration |
| **Fig. 2** | Example cells in each quadrant of Area × EII space | MapBiomas tiles |
| **Fig. 3** | Annual flux of four landscape states (1985–2024) + cumulative divergence trace map | Sections 4.1, 4.2 |
| **Fig. 4** | Annual δ distribution: trend (mean ± IQR), violin for selected years | Section 4.2 |
| **Fig. 5** | Moran's I over time + spatial maps of Area, EII, and δ for 1985 and 2024 | Sections 4.2, 4.3 |
| **Fig. 6** | MAUP sensitivity: jitter stability, hex vs. square, scale comparison | Section 4.4 |

---

## Supplementary Material (planned)

- S1: Full 5×5 frequency matrices for all snapshot periods.
- S2: Temporal interval sensitivity (5-year vs. 10-year snapshots).
- S3: Change point detection parameter sensitivity.
- S4: Pipeline code and reproducibility documentation.

---

## References (key entries — not exhaustive)

- Canfield, R.H. (1941). Application of the line intercept method in sampling range vegetation. *Journal of Forestry*, 39(4), 388–394.
- Killick, R., Fearnhead, P., & Eckley, I.A. (2012). Optimal detection of changepoints with a linear computational cost. *Journal of the American Statistical Association*, 107(500), 1590–1598.
- Levy, E.B., & Madden, E.A. (1933). The point method of pasture analysis. *New Zealand Journal of Agriculture*, 46(5), 267–279.
- MapBiomas. (2024). Collection [X] of the Annual Land Use and Land Cover Maps of Brazil. *mapbiomas.org*.
- McGarigal, K., & Marks, B.J. (1995). *FRAGSTATS: Spatial Pattern Analysis Program for Quantifying Landscape Structure*. USDA Forest Service.
- Openshaw, S. (1984). *The Modifiable Areal Unit Problem*. Geo Books, Norwich.

---

*Document maintained as part of the EII project. Update after each analytical phase is completed.*
