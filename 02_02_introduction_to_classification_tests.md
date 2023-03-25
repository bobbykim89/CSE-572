# Introduction to classification tests

## Decision trees

Training set is set of data objects
one of attributes is class attributes.

#### Q) What is the aim of classification?

- To take the class attributes and express it as function of other attributes in the given data matrix

### Decision tree example

- Express class attributes function of refund, marriage status, and taxable income
- Class attributes is `cheat` or `no cheat`

There could be more than 1 tree to express data

**Root node:** Has 0 incoming edges, and has 0 or more outgoing edges.
**Internal node:** Has 1 incoming edge, and has two or more outgoing edges.
**Leaf node:** Has 1 incoming edge, and has no outgoing edges.

### Hunt's algorithm

Let D be the set of Training regords that reach a node t
**General Procedure:**

- if D, contains records that belongs the same class y, then t is a leaf node labeled as y
- If D, is an empty set, then t is a leaf node labeled by the default class y.
- If D contains records that belongs to more than one class, use an attribute test to split the data into smaller subsets. Recursively apply the procedure to each subset.

Hunt's algorithm is the general structure that decision trees take to learn fro a a training data set. Which node do we choose as root?

1. Determine the attributes
2. How to split attributes (In objective way with mathematical reasons)

**Greedy strategy:** Split the records based on an attribute test that optimizes certain criterion

- Issues:
  - Determine how to split the records
    1. How to specify the attribure test condition?
    2. How to determine the best split?
  - Determine when to stop splitting

---

## Test conditions

#### Depends on attribute types:

- Nominal
- Ordinal
- Continuous

#### Depends on number of ways to split

- 2-way split
- Multi-way split

**Multi-way split**

- Use as many partitions as distinct values

**Binary split**

- Divide values into two subsets
- need to find optimal partitioning

### SPlit based on conrtinuous attributes

**Discretization to form an ordinal categorial attribute**

- Static
- Dynamic

**Binary decision: (A < v) or(A >= v)**

- Consider all possible splits and finds the best cut
- Can be more computationally intensive

**In order to get homogeneous sets, do we want a high oe low degree of impurity?**

- A) We want a low degree of impurity

---

## Introduction to measures of node impurity

**Q) Heuristically speaking, is it better for nodes to have more impurity or less impurity?**

- A) Less impurity is generally because then the determination would lean toward a particular class.
- Might work, but might not.

**Measure of node Impurity**

- Gini Index
- Entropy
- Misclassification error

**Gain:** Measure of impurity.
Gain = M_0 - M_12 vs M_0 - M_34

### How to find the best split?

**According to the lecture, how is gain used to determine the best split?**

---

## Measure of Impurity: GINI

Gini index for given node t:

```
GINI(t) = 1 - SUM([p(j|t)]^2, over all)

** is the relative frequency of the class j, given that the node is t.
```

**Maximum**

```
(1 - 1/n_c)
** n_c = # of classes
```

when records ar equally distributed among all classes, implying least interesting information

**Minimum**

```
(0.0)
```

when all records belongs to one class, implying most interesting information

Examples for computing GINI

**1.**

| C_1 | C_2 |
| --- | --- |
| 0   | 6   |

P(C_1) = 0/6 = 0
P(C_2) = 6/6 = 1
GINI = 1 - P(C_1) - P(C_2) = 1 - 0 - 1 = 0

**2.**

| C_1 | C_2 |
| --- | --- |
| 2   | 4   |

P(C_1) = 2/6
P(C_2) = 4/6
GINI = 1 - (2/6)^2 - (4/6)^2 = 0.44

### Splitting based on GINI

#### Used in CART, SLIQ, SPRINT

- When node p is sprint into k partitions (children), the quality of split is computed as,

```
GINI_split = SUM((n_i/n)*GINI(i))
```

**Example** Binary attributes: COmputing GINI index
Using attribute A

```
GINI(N_1) = 1 - (4/7)^2 - (3/7)^2 = 0.489
GINI(N_2) = 1 - (2/5)^2 - (3/5)^2 = 0.48
Weighted GINI index for the split = (7/12)*0.489 + (5/12)*0.48 = 0.486
```

Using attribute B

```
GINI(N_1) = 1 - (1/5)^2 - (4/5)^2 = 0.32
GINI(N_2) = 1 - (5/7)^2 - (2/7)^2 = 0.408
Weighted GINI index for the split = (5/12)*0.32 + (7/12)*0.408 = 0.37
```

- So it will be better choice to use B

### Continuous attributes, computing GINI index

1. Count unique values
2. Use threshold

**Q) WHen we are dealing with continuous attributes, how do we determine what threshold to use in order to compute the GINI index?**

- A) WE must try many thresholds at random.

---

## Measure of node impurity: Entropy

### Alternative splitting criteria based on INFO

```
Entropy(t) = - SUM(p(j|t)log_2(p(j|t)))
** Shannon's entropy
```

**Q) Entropy is a metric for impurity, even though measuring entropy is not technically possible. In the context of data analysis, however, what does the entropy metric attempt to capture?**

- A) The rancomness in data

#### Examples for computing Entropy

| C_1 | C_2 |
| --- | --- |
| 2   | 4   |

```
P(C_1) = 2/6
P(C_2) = 4/6
Entropy = -(2/6)log_2(2/6) - (4/6)log_2(4/6) = 0.92
```

### Splitting Criteria based on Classification error

```
ERROR(t) = 1 -  MAX(P(i|t))
```

| C_1 | C_2 |
| --- | --- |
| 2   | 4   |

P(C_1) = 2 / 6
P(C_2) = 4 / 6
ERROR = 1 - MAX (2/6, 4/6) = 1 - 4/6 = 1/3

### Comparison among aplitting Criteria

- GINI, Entropy and Misclassification error all has same P.
- Entropy increases faster than other two
- Distinguish kind of balanced data, Probably use GINI index

**Q) Which definition best describes gain?**

- A) It is the information contained in the parent minus the sum of the weighted information contained in the nodes

### Gain

```
DELTA = I(parent) - SUM((N(v_j)/N) * I(v_j))
```

### Gain ratio

- Impurity measures like GINI index and entropy tend to favor attributes that have a lorge number of distinct values
- Results in a large number of partitions, which are small, but pure
- If the number of records associated with each partition is very small, it is difficult to make reliable predictions

```
GainRATIO_split = GAIN_split / SplitINFO
SplitINFO = - SUM((n_i / n) * log(n-I / n))
```

**Q) WHich definition best describes splitINFO**

- It is the information contained in the split

#### SplitINFO Illustration: Case 1

- Parent node has 10 records
- Case 2: Consider 2 partitions containing 4 and 6 records
  - SplitINFO =
  - When SplitINFO is close to 1 it is good.

---

## Introduction to classification tasks: Stopping criteria for tree induction

- Stop expanding a node when all the records belong to the same class
- Stop expanding a node when all the records have similar attribute values.
- Early termination (to be discussed later)

**Q) Which reason best explains why we need to establish stopping criteria for tree induction**

- A) If the tree does not have stopping criteria, then it will overfit to the training data.
  - If stopping criteria are not defined for tree induction, then the tree will continue until it has leaf nodes that correspond to each and every data point. This means the decision tree will not be able to classify test data unless is exactly the same as the training data, which would defeat the purpose of having test data.

### Decision tree based classification: advantages

- Inexpensive to construct
- Extremely fast at classifying unknown records
- Easy to interpret for small-sized trees
- Accuracy is comparable to other classification techniques for many simple data sets

**Example: C4.5**

- Simple depth-first construction
- Uses information gain
- Sorts continuous attributes at each node
- Needs entire data to fit in memory
- Unsuitable for large databases
- Uses entropy
