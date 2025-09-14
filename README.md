# Spatial Chunking
Super simple repo for the algo that was used to group nearby OCR bounding boxes into coherent spatial chunks for downstream clustering and disclosure segmentation.

### The Algo
Computes pairwise gaps along X and Y (0 if boxes overlap on that axis), converts them to a gap distance (Euclidean), then runs HDBSCAN with a precomputed distance matrix. The cluster selection scale is picked from a small quantile of the off-diagonal distances for a sensible default.

### Practical notes

 - Normalize coordinates by page width/height for transfer across documents.
 - Plotting: OCR usually uses image coords (y increases downward) — invert the y-axis.
 - Scale: full pairwise distances are O(n^2); for very large n consider blocking/tiling or neighbor pruning before clustering.

 ### Setup/Dependencies

```python
! pip install matplotlib numpy scikit-learn pandas
```