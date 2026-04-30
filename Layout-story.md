Complete Poster Story — Project Moss

The Narrative Arc
The poster tells a single coherent scientific argument in three acts:
Act 1 (left column): Why are we here? A Mars-analog experiment produced unexpected spontaneous life on raw basalt. We want to understand where and why.
Act 2 (center column): How did we measure it, and what went wrong? Building a reliable imaging pipeline was non-trivial. The first lesson learned is that the obvious approach — color thresholding — fails badly.
Act 3 (right column): What did the hillslope shape tell us? The spatial pattern of moss is not random and not driven by "wettest wins." Topography predicts persistence through a bounded moisture optimum — the core scientific discovery.

Section by Section
Header
Title: Spontaneous Moss Colonization on Crushed Basalt: Imaging Pipeline, Color Reliability, and Topographic Controls on Persistence
The word "Spontaneous" is key — nobody planted this moss. It arrived on its own on a substrate that resembles Mars. That framing elevates the stakes immediately.

Column 1 — Introduction, Setup, Previous Work
Introduction
Biosphere 2's LEO Observatory is a precisely engineered 30 × 30 m hillslope covered in crushed basalt. The substrate is a Mars analog — same mineral composition, same lack of established soil. Despite this, moss and biological soil crusts colonized it across 330 m². The central question the poster poses: is this colonization random, or is it structured by hillslope geometry?
Research Questions (explicitly stated, answered at the end)
① Can we reliably map moss area from overhead imagery?
② Do topographic features predict where moss persists?
Stating these explicitly is deliberate — the conclusions circle back and answer them directly, giving the poster a closed logical loop that reviewers and professors appreciate.
Experimental Setup
The sensor-rich environment (1,800+ devices, 16 sensor columns, 5 cameras per slope, LiDAR DEM at 0.1 m resolution) establishes that this is not a simple field observation — it is a controlled laboratory system with extraordinary data density. This matters because it means the topographic analysis is grounded in high-quality spatial data, not approximations.
Previous Work
Two theoretical models are cited to give mathematical motivation:

Klausmeier (1999): Predicts spatially patterned vegetation from water redistribution on slopes — stripes and spots emerge from runoff dynamics.
Rietkerk (2002): Three-variable feedback model showing non-uniform biological structures arise from plant-water infiltration coupling.

These are not decorative citations. They establish the theoretical prediction that we are testing: topography and hydrology should jointly control biological patterning. Our work is the first direct empirical test of this on a controlled basalt system.

Column 2 — Methodology, Finding 01, Finding 02
Methodology — Image Pipeline (3 stages)
Stage 01 — Image Calibration
Each of the 5 cameras introduces radial lens distortion. This is corrected per-camera using intrinsic calibration parameters, then a perspective transform registers each frame to a common bath coordinate system. Without this step, cross-date comparisons are impossible because pixels don't correspond to the same physical location.
Stage 02 — Image Stitching
5 corrected frames per date are merged into a single mosaic via feature-point alignment (SIFT/homography). This produces one composite image covering the full 330 m² surface per acquisition date.
Stage 03 — Moss Proxy Extraction
A broad RGB/HSV color proxy is used rather than a narrow green threshold. This is a deliberate methodological choice: moss color shifts from yellow-green to vivid green across the season, so a narrow threshold would systematically miss early-season moss. A persistence mask then retains only pixels that are positive on ≥ 2 of the 3 analysis dates (Nov 3, Nov 22, Dec 7 — 2022). This is the primary response variable for all downstream analysis.
The bottom callout explains why persistence was chosen — it frames the next finding perfectly.

Finding 01 — Moss Is Spatially Persistent
Across all three dates the spatial footprint of moss is stable. The same regions are green in November and December. The strongest signal appears on the flanks and outer half of the hillslope, not in the deepest central drainage corridor, which remains dark and moss-poor throughout.
The November-to-December color intensification is seasonal greening of already-occupied regions, not new colonization of bare basalt. This is proven by showing the greening map is co-located with the persistent footprint — if new colonization were occurring, the greening map would show signal in previously bare areas.
Key statistics reported:

26.6% of cells stable on ≥ 2 dates
7.1% strong on all 3 dates
Median lateral offset from centerline: 3.7 m
Median trough depth of stable moss zone: 0.088 m (shallow to intermediate)


Finding 02 — Color Methods Are Unreliable
This is the pivot of the methodology story. A single irrigation event shifts moss color from yellow-green to vivid green within hours. A narrow fixed HSV/green threshold applied to a single date reports an apparent doubling of moss area after irrigation — without any real growth.
This finding justifies the entire multi-date persistence approach. It also carries a warning for any future student working with these images: never report single-date color area as a proxy for biomass or cover without accounting for hydration state.
The greening map at the bottom of this section reinforces Finding 01 — the greening signal overlaps perfectly with pre-existing moss zones, confirming the interpretation.

Column 3 — Finding 03, Model, Conclusions
Finding 03 — Topographic Controls on Moss Persistence
The central punchline of the entire poster is stated as a dark callout at the top of this column:
"Crucially — the wettest region is not the most favorable. Moss avoids the deepest drainage corridor."
This flips the naive expectation. The deepest, wettest part of the central trough is an exclusion zone — moss is consistently absent there. The stable moss habitat is displaced to off-center shoulder zones at shallow to intermediate trough depth.
Three lines of evidence support this, shown as figures:

Response curves (moss_response_curves.jpg): Moss proxy increases with lateral distance from centerline, peaks at intermediate trough depth (~0.4 m) then drops sharply. The non-monotone depth response is the key quantitative result — it directly refutes "wetter is better."
Zone heatmap (moss_zone_heatmap.jpg): Highest mean persistent moss at |x| > 3 m (off-centerline) and in the middle-to-lower slope. Confirms the spatial niche in 2D bath coordinates.
Cross-sections (moss_cross_sections.jpg): Four elevation profiles across the bath colored by moss proxy. Trough minima are repeatedly moss-poor; flanks are moss-rich. This is the clearest geometric test — it rules out 2D map overlay artifacts.

The five suppression mechanisms (excess saturation, surface flushing, sediment redistribution, mechanical instability, moisture-window limitation) explain why the trough is an exclusion zone. These are framed as hypotheses, not measurements, because direct soil moisture data is not yet available — an important epistemic distinction.

Logistic Suitability Ranking Model
To formalize the spatial structure, a logistic ranking model was fitted using topographic predictors:
logit P(M=1) = β₀ + βw·W − βf·F − γ(d − d₀)² + βt·T
Where:

W = wall proximity (βw = 1.286) — positive: shoulder zones near container walls are more favorable
F = log(1 + flow accumulation) (βf = 0.185) — negative: high flow decreases suitability
d = trough depth with quadratic term — non-monotone: peaks at d₀ = 0.407 m
T = soil thickness (βt = 0.146) — positive: thicker soil slightly more favorable

Performance: Training AUC = 0.724, spatial cross-validated AUC = 0.657. Moderate but meaningful — it correctly ranks regions from 7% to 48% stable-moss fraction across suitability deciles (shown in the calibration curve).
Two important caveats are stated explicitly on the slide:

This is a first-order ranking model, not a mechanistic law. Topographic variables act as proxies for moisture distribution; direct sensor integration remains future work.
The high wall proximity coefficient (βw = 1.29) is addressed: it likely reflects the container geometry stabilizing outer shoulders via lateral moisture retention, not a pure edge artifact.

Three figures support this section: observed moss zone, predicted probability map, and the calibration curve showing monotone increase across suitability deciles.

Conclusions
Structured to directly answer the two research questions posed at the opening:
QuestionAnswerQ1 — Can we reliably map moss?Yes — via multi-date persistence. Pipeline registers 5-camera mosaics; persistence mask suppresses irrigation artifacts.Q2 — Does topography predict it?Yes — as a first-order predictor. AUC 0.66–0.72. Topographic variables act as moisture proxies.
Plus three additional takeaways:

Core discovery: The wettest zone is the exclusion zone. Bounded moisture optimum.
Methodological lesson: Single-date color thresholding fails. Multi-date persistence is the only robust signal.
Mars implication: On Mars-analog basalt, pioneer biological colonizers preferentially occupy off-channel shoulder zones — not active drainage corridors.

Next steps listed at the bottom: soil moisture time-series in trough vs shoulder; saturation duration measurements; tracer experiments for flushing residence time; post-irrigation high-resolution surveys; CO₂ flux correlation with moss density (the respiration cycle goal mentioned from the beginning).
