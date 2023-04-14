# Association rule mining
## Introduction
- In association rule mining, whatever rule we extract from the data doesn't have any practical explanation (we don’t care). 
- So, this rule is from the data and it's a core property of only the data.
- For example buying bread+milk together may be only property for data of location 1.
- So maybe bread does not make money but if you don’t sell bread milk sales drop. So you keep both.

## Format
antecedent &rarr; consequent
- **Itemset**: a collection of one or more items {milk, bread}
- k-itemset: and itemset that contains k items {beer, diapers, milk} 3-item
- **support count**: frequency of occurrence of an itemset. $\sigma$({milk,bread,diaper})=2
- **support**: fractions of the transactions that contain the itemset s({milk,bread,diaper})=2/5


We only want to look at frequent itemsets.

**Frequent itemset happens when support ≥ some minsup threshold**

**Association rule**: an implication expression of the form X&rarr;Y where X and Y are itemsets
{milk,diaper}={beer}

## Rule evaluation metrics
We only care if this rule is frequent/significant enough. 
- **Support (s)** : fraction of transactions that contain X and Y
  - May occur simply by chance
$$ support \ s(X\rightarrow Y)=\frac{\sigma(X\cup Y)}{N}=\frac{2}{5}=0.4  $$
- **Confidence (c)** : measures how often items in Y appear in transactions that contain X
  - Measures the reliability of the inference made by a rule
$$ confidence \ c(X\rightarrow Y)=\frac{\sigma(X\cup Y)}{\sigma(X)}=\frac{2}{3}=0.67  $$

We need both rules for association mining.

## Association rule mining task
Given a set of transactions T, the goal of the association rule is to find all the rules having:
$$support \ge minsup \ threshold$$
$$confidence \ge minconf \ threshold$$


## Brute force approach:
1. List all possible association rules
2. Compute support and confidence for each
3. Prune rules that fail either

COMPUTATIONALLY PROHIBITIVE, total no of rules is large: 
$$R=3^d-2^{d+1}+1$$
Example: if d=6 then R = 602, it is massive and will increase exponentially

## Frequent itemset generation:
If rules generated from same itemset, then they will have same support, but different confidence.
We can have a method that can separate the support and confidence. So we can first look at support and then look at confidence. 
1. ***Frequent itemset generation***: We look at items with highest support… exceeding the min tolerance
    - Reduce number of candidate itemset (apriori principle)
    - Reduce number of comparisons (advanced data structures)
2.	***Rule generation***: from this itemset we can look at their confidence and find the one with high confidence.

It is still exponential though.


