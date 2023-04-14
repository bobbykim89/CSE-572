# Knowledge check

### 1. Why do we need to use confidence and support together?
- *Support may occur simply by chance*
  - Support may occur by chance; we need confidence to measure the reliability of the inference made by a rule.

### 2. In rule mining, which types of rules we are interested in? 
- *A rule that has moderate support and high confidence*
### 3. Are there logical explanations for the rules mined from datasets?
- *Maybe, but we are not concerned.* 
  - Correct! Association rule mining does not care about the explanations.
### 4. Why isn't the brute force approach optimal for rule mining?
- *It is computationally expensive and also impractical for large datasets.*
  - Correct! Brute force approach has exponential grow.
### 5. True or False? A rule whose itemsets are frequent, always has high confidence.
- *False*
### 6. Given that there are d items in the data set, how many itemsets can be derived?
- $2^d$
  - Correct!. We can derive any choice of d or less items.

### 7. Given that there are d items in the data set, how many rules can be derived?
- $3^d-2^{d+1}+1$
