# 05 — Formula Sheet

All formulas used in the worked problems, grouped by topic.

## Decision trees ([01](01-decision-tree-attribute-selection.md))

| Measure | Formula |
|---|---|
| Entropy | `Info(D) = −Σ_i p_i log2 p_i` |
| Expected information | `Info_A(D) = Σ_j (|D_j|/|D|) · Info(D_j)` |
| Information gain (ID3) | `Gain(A) = Info(D) − Info_A(D)` |
| Split information | `SplitInfo_A(D) = −Σ_j (|D_j|/|D|) log2(|D_j|/|D|)` |
| Gain ratio (C4.5) | `GainRatio(A) = Gain(A) / SplitInfo_A(D)` |
| Gini index (CART) | `Gini(D) = 1 − Σ_i p_i²` |
| Gini of a binary split | `Gini_A(D) = (|D1|/|D|) Gini(D1) + (|D2|/|D|) Gini(D2)` |
| Number of binary splits | `2^(k−1) − 1` for a k-valued attribute |

## Clustering ([02](02-hierarchical-and-density-clustering.md))

| Measure | Formula |
|---|---|
| Single / complete link | `d_min = min ‖p − p'‖`,  `d_max = max ‖p − p'‖` over p ∈ Cᵢ, p' ∈ Cⱼ |
| Mean / average link | `d_mean = ‖mᵢ − mⱼ‖`,  `d_avg = (1/(nᵢnⱼ)) Σ Σ ‖p − p'‖` |
| Dendrogram levels | `n − 1` merges for n objects |
| Clustering feature | `CF = ⟨N, LS, SS⟩`,  `LS = Σ xᵢ`,  `SS = Σ xᵢ²` |
| Additivity | `CF(C1 ∪ C2) = CF1 + CF2` |
| Centroid | `x0 = LS / N` |
| Radius | `R = √( SS/N − (LS/N)² )`, summed over dimensions |
| Diameter | `D = √( (2N·SS − 2·LS²) / (N(N − 1)) )`, summed over dimensions |
| Jaccard | `sim(Tᵢ, Tⱼ) = |Tᵢ ∩ Tⱼ| / |Tᵢ ∪ Tⱼ|` |
| ROCK link | `link(Tᵢ, Tⱼ) = |N(Tᵢ) ∩ N(Tⱼ)|`, neighbours if `sim ≥ θ` |
| DBSCAN core point | `|N_ε(p)| ≥ MinPts`, with `N_ε(p) = {q : d(p, q) ≤ ε}` (p included) |
| Squared-distance shortcut | `d ≤ ε ⇔ Δx² + Δy² ≤ ε²` |

## Similarity and dissimilarity ([03](03-proximity-measures.md))

| Measure | Formula |
|---|---|
| Nominal | `d(i, j) = (p − m) / p` |
| Symmetric binary | `d = (r + s) / (q + r + s + t)` |
| Asymmetric binary | `d = (r + s) / (q + r + s)` |
| Mean absolute deviation | `s_f = (1/n) Σ |x_if − m_f|` |
| z-score | `z_if = (x_if − m_f) / s_f` |
| Ordinal mapping | `z_if = (r_if − 1) / (M_f − 1)` |
| Minkowski | `d(i, j) = (Σ_f |x_if − x_jf|^h)^(1/h)`; h = 1 Manhattan, h = 2 Euclidean, h → ∞ supremum |
| Cosine | `cos(d1, d2) = (d1 · d2) / (‖d1‖ ‖d2‖)` |

## Frequent patterns ([04](04-frequent-patterns-and-association-rules.md))

| Measure | Formula |
|---|---|
| Support | `support(X ⇒ Y) = P(X ∪ Y)` |
| Confidence | `confidence(X ⇒ Y) = support_count(X ∪ Y) / support_count(X)` |
| Rules per itemset | `2^k − 2` for a k-itemset |
| DHP hash (course example) | `h(x, y) = (10·order(x) + order(y)) mod 7` |
| ECLAT support | `support(X ∪ Y) = |TID(X) ∩ TID(Y)|` |
| Lift | `Lift(A, B) = P(A ∪ B) / (P(A) P(B))`; > 1 positive, < 1 negative, = 1 independent |
