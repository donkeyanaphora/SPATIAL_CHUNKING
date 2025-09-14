# Spatial Chunking

Super simple repo for the algo that was used to group nearby OCR bounding boxes into coherent spatial chunks for downstream clustering and disclosure segmentation.

## What it does
- **Input:** N×4 array of axis-aligned boxes [x0, y0, x1, y1] (ideally normalized to [0,1]).
- **Output:** integer cluster labels per box (-1 = noise) suitable for grouping and post-processing.

## How it works (brief)
- Compute pairwise **axis gaps** (0 when boxes overlap on that axis).
- Convert gaps to a **gap distance** (Euclidean; Manhattan also works).
- Cluster with **HDBSCAN** using a precomputed distance matrix.  
  Use a low quantile (e.g., **5–10%**) of off-diagonal distances as a sensible cluster_selection_epsilon.


## Practical notes
- **Normalize coordinates** by page width/height for portability across documents.
- **Plotting:** OCR coords are usually top-left origin—remember to invert the y-axis in Matplotlib.
- **Scale:** pairwise distances are O(N²). For very large N, block/tilize pages or prune to nearby neighbors first.
- **Variants:** Easily tweaked to affinity measure e.g. A = (1-dx)*(1-dy)

## Install
```bash
pip install numpy pandas matplotlib hdbscan
```

## Usage
- [View on GitHub](https://github.com/donkeyanaphora/SPATIAL_CHUNKING/blob/main/spatial_segmentation.ipynb)
- [View on nbviewer](https://nbviewer.org/github/donkeyanaphora/SPATIAL_CHUNKING/blob/main/spatial_segmentation.ipynb)
- [Open In Colab](https://colab.research.google.com/github/donkeyanaphora/SPATIAL_CHUNKING/blob/main/spatial_segmentation.ipynb)