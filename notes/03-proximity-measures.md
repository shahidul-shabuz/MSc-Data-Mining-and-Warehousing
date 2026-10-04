# 03 — Measuring Similarity and Dissimilarity

> Lecture 7A · Problems M12–M14

## Reference formulas

| Data type | Measure |
|---|---|
| Nominal | `d(i, j) = (p − m) / p`, where m = matching attributes and p = total attributes |
| Symmetric binary | `d = (r + s) / (q + r + s + t)` |
| Asymmetric binary | `d = (r + s) / (q + r + s)` (0–0 matches ignored); Jaccard `sim = q / (q + r + s)` |
| Interval-scaled | Standardize first: `z = (x − m) / s`, with s the **mean absolute deviation** (more robust to outliers than the standard deviation) |
| Ordinal | Map rank r ∈ {1..M} to `z = (r − 1)/(M − 1)`, then treat as interval-scaled |
| Numeric vectors | Minkowski `d = (Σ |x_f − y_f|^h)^(1/h)` |
| Documents | Cosine `cos(x, y) = x·y / (‖x‖ ‖y‖)` |

Contingency counts for binary objects i and j: **q** = both 1, **r** = i is 1 and j is 0, **s** = i is 0 and j is 1, **t** = both 0.

---

## M12. Asymmetric binary dissimilarity (2023 exam, Q7b)

| Name | Gender | Fever | Cough | Test-1 | Test-2 | Test-3 | Test-4 |
|---|---|---|---|---|---|---|---|
| Jack | M | Y | N | P | N | N | N |
| Mary | F | Y | N | P | N | P | N |
| Jim | M | Y | P | N | N | N | N |

Gender is **symmetric**, so it is excluded. The other six attributes are asymmetric binary; encode Y/P = 1 and N = 0:

```text
Jack = (1, 0, 1, 0, 0, 0)    Mary = (1, 0, 1, 0, 1, 0)    Jim = (1, 1, 0, 0, 0, 0)
```

| Pair | q | r | s | d = (r+s)/(q+r+s) |
|---|---:|---:|---:|---:|
| Jack, Mary | 2 | 0 | 1 | 1/3 = **0.33** |
| Jack, Jim | 1 | 1 | 1 | 2/3 = **0.67** |
| Jim, Mary | 1 | 1 | 2 | 3/4 = **0.75** |

**Answer:** d(Jack, Mary) = 0.33, d(Jack, Jim) = 0.67, d(Jim, Mary) = 0.75. Jack and Mary are the most similar, so they are the most likely to have the same condition; Jim and Mary are the least alike. Two patients both testing negative (t) carries no information here, which is why t is left out.

## M13. Minkowski distance: L1 and L2

A **metric** satisfies positive definiteness, symmetry and the triangle inequality. For x1(1,2), x2(3,5), x3(2,0), x4(4,5):

| Pair | Δ | L1 (Manhattan) | L2 (Euclidean) |
|---|---|---:|---:|
| x2, x1 | (2, 3) | 5 | √13 = 3.61 |
| x3, x1 | (1, 2) | 3 | √5 = 2.24 |
| x3, x2 | (1, 5) | 6 | √26 = 5.10 |
| x4, x1 | (3, 3) | 6 | √18 = 4.24 |
| x4, x2 | (1, 0) | 1 | 1.00 |
| x4, x3 | (2, 5) | 7 | √29 = 5.39 |

```text
L1    x1  x2  x3  x4          L2     x1    x2    x3    x4
x1     0                      x1     0
x2     5   0                  x2   3.61    0
x3     3   6   0              x3   2.24  5.10    0
x4     6   1   7   0          x4   4.24  1.00  5.39    0
```

**Answer:** the two matrices above. The closest pair is x2–x4, and the farthest is x3–x4. Note that `L2 ≤ L1` always, and `h → ∞` gives the supremum distance `max_f |x_f − y_f|`.

## M14. Cosine similarity between documents

```text
d1 = (5, 0, 3, 0, 2, 0, 0, 2, 0, 0)        d2 = (3, 0, 2, 0, 1, 1, 0, 1, 0, 1)

d1 · d2 = 15 + 6 + 2 + 2 = 25
‖d1‖ = √(25 + 9 + 4 + 4) = √42 = 6.481
‖d2‖ = √(9 + 4 + 1 + 1 + 1 + 1) = √17 = 4.123

cos(d1, d2) = 25 / (6.481 × 4.123) = 0.94
```

**Answer:** cos(d1, d2) = 0.94. The documents are highly similar. Cosine measures **direction**, not length, so a short and a long document on the same topic still score high.
