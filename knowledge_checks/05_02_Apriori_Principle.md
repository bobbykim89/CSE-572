# KNOWLEDGE CHECK 
## 1. Which of the following statements are true about common strategies adopted by many association rule mining algorithms? (select all that apply)
- Generate itemsets whose support is greater or equal to minsup
  - Generating frequent itemsets only is not enough.
- Generate high confidence rules from each frequent itemset, where each rule is a binary partitioning of a frequent itemset
  - Generating strong rules only is not enough, we also need to generate all itemsets whose support is greater or equal to minsup

## 2. Which of the following statements are true regarding the apriori algorithm? (select all that apply)
- Algorithm needs to make an additional pass over dataset after selecting candidate item sets
- Algorithm eliminates all candidate itemsets whose support counts are less than minsup
- Algorithm terminates when there are no new frequent itemsets generated

##3. Which of the following statements are true regarding candidate generation and pruning? (select all that apply)
- Generates new candidate k-itemsets based on frequent (k-1) itemsets found in previous iteration.
- Eliminates some of candidate k-itemsets using support-based pruning strategy. 
  - For candidate generation and pruning generates new candidate k-itemsets based on the frequent (k-1)-itemsets, also eliminate some of the candidate k-itemsets using the support-based pruning strategy.

## 4. What does the apriori algorithm tell us? (select all that apply)
- Superset of itemsets that are not frequent are not frequent 
- Subsets of itemsets that are frequent are frequent 

## 5. Can we apply the apriori algorithm to confidence? 
- Not in the same way as with support but in a different way 
    - Correct! If a rule is not confident, then rules generated from the subset of its itemsets are also not confident 

## 6. Consider that we have a rule A → {B,C} and this rule is confident. What can you say about the rule {A,B} → C? 
- Confident
    - Correct! Confidence of the first rule (A → {B,C}) equals to (support of {ABC}/support of {A}. Confidence of the second rule ({A, B} → C) equals to (support of {ABC}/support of {A, B}). Since support of {A,B} is less than or equal to support of {A}, the second rule will have at least same level of confidence as the first rule.

$$ \frac{\sigma(A,B,C)}{\sigma(A)} \le \frac{\sigma(A,B,C)}{\sigma(A,B)} $$
$$ \sigma(A) \ge \sigma(A,B) $$

You divide by less when $\sigma(A,B)$ so the overall confidence is higher.

$\sigma(A,B,C)$ was already confident.

## 7. Consider that we have a rule A → {B,C} and this rule is confident. What can you say about the rule A → C?
- Confident
  - Confidence of the first rule (A → {B,C}) equals to (support of {ABC}/support of {A}. Confidence of the second rule ({A} → C) equals to (support of {AC}/support of {A}). Since support of {A,B,C} is less than or equal to support of {A,C}, the second rule will have at least same level of confidence as the first rule.

$$ \frac{\sigma(A,B,C)}{\sigma(A)} \le \frac{\sigma(A,C)}{\sigma(A)} $$

$\sigma(A,B,C)$ was already confident. $\sigma(A,B)$  will be equally or more confident.