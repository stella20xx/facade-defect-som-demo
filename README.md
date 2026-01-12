# Unsupervised Facade Defect and Stain Analysis with SOM

Label-free detection and intra-defect analysis of facade defects
(cracks, stains, contamination) using pixel-level Self-Organizing Maps (SOM).

This demo shows how RGB images of building envelopes can be segmented
into clean surface, major cracks, minor cracks, and stain regions without
any manual pixel labels, while also revealing variations *inside* each
defect (e.g., darker cores or moisture-rich zones).

See the full slide deck in
[`docs/facade_som_defect_demo.pdf`](docs/facade_som_defect_demo.pdf).

---

## Problem

- Facade inspection is often done visually, or with supervised models
  that need dense pixel annotations.
- Small cracks, stains, and surface contamination can be hard to detect
  against textured backgrounds.
- Goal: **detect cracks and stains on building envelopes, and analyze
  their internal patterns, in a fully unsupervised way.**

---

## Data

- RGB photos of exterior walls and coatings:
  - major structural cracks,
  - minor / hairline cracks on textured backgrounds,
  - surface stains and contamination patches.
- No pixel-level labels are used.

---

## Method (SOM-based pixel-level clustering)

1. **Physics/appearance-aware features**

   Each pixel is mapped into a multi-dimensional feature vector capturing:

   - hue and grayscale intensity,
   - local contrast and edge strength,
   - texture thinness and neighborhood statistics.

2. **PCA + SOM clustering**

   - PCA reduces feature dimension.
   - A Self-Organizing Map (SOM) is trained to obtain a small number of
     interpretable clusters (e.g., clean wall, major crack, minor crack,
     stain core, stain periphery).

3. **Binary masks and intra-defect analysis**

   - For cracks, the SOM map is thresholded to extract binary crack
     masks without manual labeling.
   - For stains, clusters are grouped into **primary stain** and
     **secondary / core zones**, highlighting darker or moisture-rich
     regions inside the defect.
   - Radar / feature-attribution plots (see PDF) show how each cluster
     differs in hue, intensity, contrast, and thinness.

Key properties:

- **Fully unsupervised:** no manual pixel labels are needed.
- **Interpretable:** cluster-level feature profiles explain why SOM
  separates crack vs background or stain core vs periphery.
- **Generalizable:** the same pipeline can be extended to mold growth,
  efflorescence, rust streaks, and other facade contaminants.

---

## Results (see PDF)

Highlights from `docs/facade_som_defect_demo.pdf`:

- Major cracks are detected with strong edge/contrast features and clean
  separation from the wall background.
- Minor cracks on textured surfaces are isolated as a dedicated cluster,
  supporting severity assessment.
- Surface stains are decomposed into core and peripheral regions,
  revealing patterns related to moisture ingress or contamination sources.

---

## Status

This repository currently serves as a **documentation/demo hub** for the
facade SOM pipeline. Code and runnable notebooks will be added as the
framework is cleaned and released.
# facade-defect-som-demo
