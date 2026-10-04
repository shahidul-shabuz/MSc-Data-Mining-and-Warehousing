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

A pure partition has Info = 0; a perfectly balanced two-class partition has Info = 1.

## M2. Information gain: choose the root

```text
Info_A(D) = Σ_j |D_j|/|D| · Info(D_j)          Gain(A) = Info(D) − Info_A(D)
```

**age:** youth (2 yes, 3 no), middle-aged (4, 0), senior (3, 2)

```text
Info_age(D) = 5/14 · 0.9710 + 4/14 · 0 + 5/14 · 0.9710 = 0.6935
Gain(age)   = 0.9403 − 0.6935 = 0.2467
```

**student:** yes (6, 1), no (3, 4)

```text
Info_student(D) = 7/14 · 0.5917 + 7/14 · 0.9852 = 0.7885      Gain = 0.1518
```

**credit_rating:** fair (6, 2), excellent (3, 3)

```text
Info_credit(D) = 8/14 · 0.8113 + 6/14 · 1.0 = 0.8922          Gain = 0.0481
```

**income:** high (2, 2), medium (4, 2), low (3, 1)

```text
Info_income(D) = 4/14 · 1.0 + 6/14 · 0.9183 + 4/14 · 0.8113 = 0.9111   Gain = 0.0292
```

| Attribute | Info_A(D) | Gain(A) |
|---|---:|---:|
| **age** | 0.6935 | **0.2467** |
| student | 0.7885 | 0.1518 |
| credit_rating | 0.8922 | 0.0481 |
| income | 0.9111 | 0.0292 |

**age** has the highest gain and becomes the root. The middle-aged branch is pure, so it becomes a leaf labelled *yes*.

*(Computing with rounded intermediate values gives 0.2468; the exact value is 0.2467.)*

## M3. Gain ratio (C4.5) for income

Information gain is biased toward attributes with many values. C4.5 normalizes by the **split information**, which depends only on partition sizes:

```text
SplitInfo_income(D) = −[ 4/14 log2(4/14) + 6/14 log2(6/14) + 4/14 log2(4/14) ]
                    = −[ −0.5164 − 0.5239 − 0.5164 ] = 1.5567

GainRatio(income) = 0.0292 / 1.5567 = 0.0188
```

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

Comparing all three binary splits of income: {low, medium} | {high} = 0.4429, {low, high} | {medium} = 0.4583, {medium, high} | {low} = 0.4500. The first has the **lowest** Gini, so it is the split CART would choose for this attribute.

For two classes, Gini ≤ 0.5 and Info ≤ 1, a quick sanity check on any hand calculation.
