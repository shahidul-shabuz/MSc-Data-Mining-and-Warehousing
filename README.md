# Data Mining and Warehousing — MSc Worked Solutions

Step-by-step solutions to the numerical problems in **CSE 6202: Data Mining and Warehousing** (M.Sc. in CSE, DUET), organized by lecture.

| | |
|---|---|
| **Course** | CSE 6202: Data Mining and Warehousing — M.Sc. in CSE, Dhaka University of Engineering & Technology (DUET) |
| **Semester** | 2nd semester |
| **Course teacher** | [Prof. Dr. Momotaz Begum](https://profile.duet.ac.bd/u/drmomotaz), Professor and Head, Department of Computer Science and Engineering, DUET |
| **Grade** | Result pending (expected 4 November 2026) |

## Contents

| # | Topic | Lecture | Worked problems |
|---|---|---|---|
| 01 | [Decision-tree attribute selection](notes/01-decision-tree-attribute-selection.md) | 2.2 | M1 Entropy · M2 Information gain · M3 Gain ratio (C4.5) · M4 Gini index (CART) |
| 02 | [Hierarchical and density-based clustering](notes/02-hierarchical-and-density-clustering.md) | 5 | M5 AGNES/DIANA · M6–M8 BIRCH clustering features · M9 Jaccard · M10 ROCK links · M11 DBSCAN |
| 03 | [Similarity and dissimilarity](notes/03-proximity-measures.md) | 7A | M12 Asymmetric binary · M13 Minkowski L1/L2 · M14 Cosine |
| 04 | [Frequent patterns and association rules](notes/04-frequent-patterns-and-association-rules.md) | 7B | M15 Support/confidence · M16–M17 Apriori · M18 Rule generation · M19–M20 DHP · M21 Transaction reduction · M22 FP-Growth · M23 ECLAT · M24 Lift |
| 05 | [Formula sheet](notes/05-formula-sheet.md) | — | Every formula used above, in one place |

Each solution states the question, writes out the formula, substitutes step by step, and ends with the answer and its interpretation.

## Highlights

- **Same answer, two algorithms.** FP-Growth (prefix tree) and ECLAT (vertical TID-sets) are solved on the same database and reach the same 13 frequent itemsets (M22, M23).
- **Why confidence misleads.** A "strong" rule (support 40%, confidence 67%) has lift 0.89, so the items are negatively correlated (M24).
- **Why links beat Jaccard.** On categorical transactions, Jaccard rates cross-cluster pairs higher than within-cluster pairs; ROCK's common-neighbour count separates them, 5 vs. 3 (M9, M10).
- **BIRCH from summaries only.** Centroid, radius and diameter are computed from ⟨N, LS, SS⟩ without the raw points, with the N(N − 1) diameter convention derived (M8).
- **DBSCAN by hand.** All 66 pairwise distances reduced to a squared-distance test, then core, border and noise points identified (M11).

## Past exam coverage (DUET 2023, CSE 6202)

| Question | Topic | Covered in |
|---|---|---|
| 1(c) | Frequent patterns by DHP | [04 · M19](notes/04-frequent-patterns-and-association-rules.md) |
| 3(c) | AGNES / DIANA dendrogram | [02 · M5](notes/02-hierarchical-and-density-clustering.md) |
| 4(a) | Clustering feature of Cluster 3 | [02 · M7](notes/02-hierarchical-and-density-clustering.md) |
| 4(c) | Apriori | [04 · M17](notes/04-frequent-patterns-and-association-rules.md) |
| 5(a) | ECLAT | [04 · M23](notes/04-frequent-patterns-and-association-rules.md) |
| 7(a) | Jaccard coefficient | [02 · M9](notes/02-hierarchical-and-density-clustering.md) |
| 7(b) | Asymmetric binary dissimilarity | [03 · M12](notes/03-proximity-measures.md) |
| 7(c) | FP-tree | [04 · M22](notes/04-frequent-patterns-and-association-rules.md) |

## Paper presentation

As part of the course, I presented:

> M. M. Jawad, R. Ahmed, I. S. Apan, T. H. Tomal, F. Haider, M. S. Hossain, M. F. A. Bhuiyan, "Benchmarking Large Language Models on Bangla Dialect Translation and Dialectal Sentiment Analysis," in *Proceedings of the Second Workshop on Bangla Language Processing (BLP-2025)*, pp. 322–337, Association for Computational Linguistics, 2025.

The paper introduces DIALTSA-BN, 600 annotated YouTube comments across four dialects (Chattogram, Barishal, Sylhet, Noakhali), and benchmarks LLMs on dialect-to-standard translation and sentiment analysis. Its key finding is that transliterating Bangla script into Latin characters substantially improves translation by closed-source models. This connects directly to my research interest in dialectal robustness for Bangla NLP.

## A note on preparation

These solutions were prepared from my course notes with the help of an AI assistant (Claude) and reviewed by me; all numerical answers were checked independently. Lecture slides and other course materials are not included, as they belong to their authors.

## Author

**Md Shahidul Islam Shabuz** — Assistant Professor, Dept. of CSE, RSTU; M.Sc. candidate, DUET
[Website](https://shahidul-shabuz.github.io/) · [Google Scholar](https://scholar.google.com/citations?user=VDtX90sAAAAJ&hl=en) · [ORCID](https://orcid.org/0009-0008-8271-888X)

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
