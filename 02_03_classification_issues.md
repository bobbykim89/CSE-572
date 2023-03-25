# Classification Issues

## Practical issues with classification

- Underfitting
- Overfitting
- Costs of classification

### Underfitting and overfitting: Errors

- **Training error / re-submission error:**
  - Number of errors committed o training records
- **Generalization Error:**
  - Expected error of the model on previously unseen records

### Underfitting and overfitting: good model

- Low training error and low generalization error
- Training error can be reduced by increasing the model complexity (having more nodes, but it doesn't mean that you will redice low generalization error.)
- Model that fit training data too well can have poor generalization error because it's a model that is learning the noise.

**Overfitting:** A model that fits the training data too well can have poorer generalization error than a model with higher training error.

### Underfitting and overfitting: Training errors

- Training error for a complex tree is 0, but test error is large as tree may contain nodes that accidently fit some noise points in the training data.
- Nodes do not generalize well to the test examples and can degrade the performance of the tree.

### Notes on overfitting

- Overfitting results in decision trees that are **more complex** than necessary.
- Training error **no longer provides a good estimate** of ghow well the tree will perform on **previously unseen records**
- Need **new ways** for estimating errors.

---

## Estimating generalization errors

### Occam's Razor

- Given two models of similar generalization errors, one should **prefer the simpler model** over the more complex model
- For complex models, there is a **greater chance that it was fitted accidently by errors** in data
- Should include **model complexity** when evaluating a model
- When we evaluate generalization error, it is very good idea to include model complexity in the estimation of generalization error.

**Re-substitution errors**

- Error on training

**Generalization errors**

- Error on testing
  - Optimistic approach
  - Pessimistic approach

### Pessimistic approach

**Incorporates model complexity in error computation**

- For each leaf node, add penalty term (say, 0.5),
- Total errors: e'(T) = e(T) + N \* 0.5(N: number of leaf nodes)
- For a tree with 30 leaf nodes and 10 errors on training 9OUT OF 1000 instances):
  - Training error = 10/1000 = 1%
- Generalization error = (10 + 30 \* 0.5) / 1000 = 2.5%

### Estimating generalization errors: Validation set

- Divide the original training data into two smaller subsets
- Train the model on one subset
- Use other subset to estimate generalization errors
- The model attaining lowest error on validation set is used as final model.

### How to address overfitting

#### Pre-pruning:

- Stop the algorithm before it becomes a fully-grown tree
  - Stop if all instances belong to the same class
  - Stop if all the attributes values are the same

#### More restrictive conditions:

- Stop if number of instances is less than some user specified threshold
- Stop if expading the current node does not improve impurity measures over a certain threshold
- Difficult to choose the right threshold

Very difficult problem to choose what is the right threshold, and that is where comes the dilemma between overfitting and underfitting. Because if you choose a very high threshold, then you might be underfitting. YOu have improved impurity but you still don't consider it because it didn't cross the threshold and your threshold is too high.
Means that you might fit into underfitting domain.

#### Post-pruning:

- Grow decision tree to its **entirety**
- **Trim the nodes** of the decision tree in a bottom-up fashion
- If generalization error improves after trimming, **replaces sub-tree** by a leaf node.
- Class label of leaf node is determined from majority class of instances in the sub-tree.

**Q) In the context of decision boundaries, what is the function of a decision tree?**

- A) The decision tree divides the attribute space into boxes
  - Each node on a decision tree can be represented by a straight line on the attribute space, and these lines can create boxes.

---
