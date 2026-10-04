# 01 — Attribute Selection in Decision-Tree Induction

> Lecture 2.2 · Problems M1–M4

A decision tree is grown top-down by repeatedly choosing the attribute that best separates the classes. The three classic measures are **information gain** (ID3), **gain ratio** (C4.5) and the **Gini index** (CART).

## Dataset: `buy_computer` (14 tuples, 9 yes / 5 no)

| RID | age | income | student | credit_rating | buy_computer |
|---:|---|---|---|---|---|
| 1 | youth | high | no | fair | no |
| 2 | youth | high | no | excellent | no |
| 3 | middle-aged | high | no | fair | yes |
| 4 | senior | medium | no | fair | yes |
| 5 | senior | low | yes | fair | yes |
| 6 | senior | low | yes | excellent | no |
| 7 | middle-aged | low | yes | excellent | yes |
| 8 | youth | medium | no | fair | no |
| 9 | youth | low | yes | fair | yes |
| 10 | senior | medium | yes | fair | yes |
| 11 | youth | medium | yes | excellent | yes |
| 12 | middle-aged | medium | no | excellent | yes |
| 13 | middle-aged | high | yes | fair | yes |
| 14 | senior | medium | no | excellent | no |

---

## M1. Entropy Info(D)

```text
Info(D) = −Σ_i p_i log2 p_i
        = −[ 9/14 · log2(9/14) + 5/14 · log2(5/14) ]
        = −[ 0.6429 × (−0.6374) + 0.3571 × (−1.4855) ]
        = 0.9403 bits
```

**Answer:** Info(D) = 0.9403 bits.

A pure partition has Info = 0; a perfectly balanced two-class partition has Info = 1.

## M2. Information gain: choose the root

```text
Info_A(D) = Σ_j |D_j|/|D| · Info(D_j)          Gain(A) = Info(D) − Info_A(D)
```

**Attribute age:** youth 5 rows (2 yes, 3 no), middle-aged 4 rows (4 yes, 0 no), senior 5 rows (3 yes, 2 no)

```text
Info(youth)  = −[ 2/5 log2(2/5) + 3/5 log2(3/5) ] = −[ 0.4(−1.3219) + 0.6(−0.7370) ] = 0.9710
Info(middle) = −[ 4/4 log2(4/4) ] = 0                                   (pure partition)
Info(senior) = −[ 3/5 log2(3/5) + 2/5 log2(2/5) ] = 0.9710

Info_age(D) = 5/14 (0.9710) + 4/14 (0) + 5/14 (0.9710) = 0.3468 + 0 + 0.3468 = 0.6935
Gain(age)   = 0.9403 − 0.6935 = 0.2467
```

**Attribute student:** yes 7 rows (6 yes, 1 no), no 7 rows (3 yes, 4 no)

```text
Info(student=yes) = −[ 6/7 log2(6/7) + 1/7 log2(1/7) ] = −[ 0.8571(−0.2224) + 0.1429(−2.8074) ] = 0.5917
Info(student=no)  = −[ 3/7 log2(3/7) + 4/7 log2(4/7) ] = −[ 0.4286(−1.2224) + 0.5714(−0.8074) ] = 0.9852

Info_student(D) = 7/14 (0.5917) + 7/14 (0.9852) = 0.2959 + 0.4926 = 0.7885
Gain(student)   = 0.9403 − 0.7885 = 0.1518
```

**Attribute credit_rating:** fair 8 rows (6 yes, 2 no), excellent 6 rows (3 yes, 3 no)

```text
Info(fair)      = −[ 6/8 log2(6/8) + 2/8 log2(2/8) ] = −[ 0.75(−0.4150) + 0.25(−2) ] = 0.8113
Info(excellent) = −[ 3/6 log2(3/6) + 3/6 log2(3/6) ] = 1.0000                  (balanced)

Info_credit(D)       = 8/14 (0.8113) + 6/14 (1.0000) = 0.4636 + 0.4286 = 0.8922
Gain(credit_rating)  = 0.9403 − 0.8922 = 0.0481
```

**Attribute income:** high 4 rows (2 yes, 2 no), medium 6 rows (4 yes, 2 no), low 4 rows (3 yes, 1 no)

```text
Info(high)   = 1.0000                                                     (balanced)
Info(medium) = −[ 4/6 log2(4/6) + 2/6 log2(2/6) ] = −[ 0.6667(−0.5850) + 0.3333(−1.5850) ] = 0.9183
Info(low)    = −[ 3/4 log2(3/4) + 1/4 log2(1/4) ] = 0.8113

Info_income(D) = 4/14 (1) + 6/14 (0.9183) + 4/14 (0.8113) = 0.2857 + 0.3936 + 0.2318 = 0.9111
Gain(income)   = 0.9403 − 0.9111 = 0.0292
```

| Attribute | Info_A(D) | Gain(A) |
|---|---:|---:|
| **age** | 0.6935 | **0.2467** |
| student | 0.7885 | 0.1518 |
| credit_rating | 0.8922 | 0.0481 |
| income | 0.9111 | 0.0292 |

**Answer:** **age** has the highest gain and becomes the root. The middle-aged branch is pure, so it becomes a leaf labelled *yes*.

*(Computing with rounded intermediate values gives 0.2468; the exact value is 0.2467.)*

## M3. Gain ratio (C4.5) for income

Information gain is biased toward attributes with many values. C4.5 normalizes by the **split information**, which depends only on partition sizes:

```text
SplitInfo_income(D) = −[ 4/14 log2(4/14) + 6/14 log2(6/14) + 4/14 log2(4/14) ]
                    = −[ −0.5164 − 0.5239 − 0.5164 ] = 1.5567

GainRatio(income) = 0.0292 / 1.5567 = 0.0188
```

**Answer:** SplitInfo_income(D) = 1.5567 bits and GainRatio(income) = 0.0188. (A smaller split-information value of 0.926 would give 0.031, but substituting the actual partition sizes 4, 6 and 4 gives 1.5567.)

## M4. Gini index (CART)

```text
Gini(D) = 1 − Σ p_i² = 1 − [ (9/14)² + (5/14)² ] = 1 − [0.4133 + 0.1276] = 0.4592
```

CART builds binary trees, so a k-valued attribute is tested as `2^(k−1) − 1` binary splits; for income (k = 3) that is 3 splits. For income ∈ {low, medium} vs. {high}:

```text
D1 = {low, medium}: 10 tuples (7 yes, 3 no)   Gini(D1) = 1 − (0.7² + 0.3²) = 0.420
D2 = {high}:         4 tuples (2 yes, 2 no)   Gini(D2) = 1 − (0.5² + 0.5²) = 0.500

Gini_income(D) = 10/14 · 0.420 + 4/14 · 0.500 = 0.4429
```

The other two binary splits of income:

```text
{low, high} vs {medium}:  D1 = 8 tuples (5 yes, 3 no)  Gini = 1 − (0.625² + 0.375²) = 0.4688
                          D2 = 6 tuples (4 yes, 2 no)  Gini = 1 − (0.667² + 0.333²) = 0.4444
                          Gini = 8/14 (0.4688) + 6/14 (0.4444) = 0.4583

{medium, high} vs {low}:  D1 = 10 tuples (6 yes, 4 no) Gini = 1 − (0.6² + 0.4²) = 0.4800
                          D2 = 4 tuples (3 yes, 1 no)  Gini = 1 − (0.75² + 0.25²) = 0.3750
                          Gini = 10/14 (0.4800) + 4/14 (0.3750) = 0.4500
```

| Binary split of income | Gini_income(D) |
|---|---:|
| **{low, medium} vs {high}** | **0.4429** |
| {medium, high} vs {low} | 0.4500 |
| {low, high} vs {medium} | 0.4583 |

**Answer:** Gini(D) = 0.4592. The split {low, medium} vs {high} has the **lowest** Gini (0.4429), so it is the best binary split on income. The reduction in impurity is `ΔGini = 0.4592 − 0.4429 = 0.0163`.

For two classes, Gini ≤ 0.5 and Info ≤ 1, a quick sanity check on any hand calculation.
