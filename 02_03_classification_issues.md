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

## Generalization: Bias variance tradeoff

Trying to generalize based on past experience

### Generalization:

- Components of generalization error
  - **Note:** All models have error, there is no such thing as true model, but we assume the class attibutes for training set is true model.
  - **Bias:** how much the average model over all training sets differ from the true model?
    - Error due to inaccurate assumptions/simplifications made by the model.
  - **Variance:** How much models estimated from different training sets differ from each other.
    - When model is too complex, that means it learns nitty-gritty details of training sets that are not important for classification.
  - **Underfitting:** Model is too `simple` to represent all the relevant class characteristics
    - High bias and low variance
    - Hogh training error and high test error
  - **Overfitting:** model is too `complex` and fits irrelevant characteristics (noise) in the data
    - Low bias and high variance
    - Low training error and high test error.

**Q) Generalization error has different components, one of which is known as Bias. What is Bias?**

- A) A measure of how much the average model over all training sets differ from the true model
  - Bias is basically a measure of how far a preconceived notion is from the truth. Soon, you will hear about how bias is an error due to inaccurate assumptions or simplications made by a model.

**Q) In the context of Bias, why will a particular model differ from the training set?**

- A) Because the model might be too simplistic
  - Bias is the error due to inaccurate assumptions or simplifications made by the model.

**Q) Generalization error has different components, one of which is known as Variance. What is Variance?**

- A) A measure of how much models estimated from different training sets differ from each other
  - Variance can be an indication of a model that is too complex. A model that is too complex is learning the nitty-gritty details of the training set that are not important for classification.

---

## The bias tradeoff

```
Err(z) = Bias^2 + Variance + Irreducible Error
```

- Prediction errors models can be decomposed into two main components
  - error due to bias
  - error due to variance
- Tradeoff between a model's ability to minimize bias and variance
- You want moderate bias and moderate variance (You can't get low bias/low variance, high bias/high variance models means that machine learned nothing)

**Q) There is a tradeoff between the bias and variance of a model, and it is commonly called the No Free Lunch Theorem. Which limitation best describes this tradeoff?**

- A) A model cannot have both low bias and low variance.
  - The No Free Lunch Theorem describes the tradeoff between a model’s ability to minimize bias and variance. There is no “best of both worlds” because decreasing bias will increase variance (and vice versa).

**Q) In the context of the bias-variance tradeoff, which model most preferable?**

- A) A model with moderate variance and moderate bias

  - Although we would really prefer to have low bias and low variance, this is not possible because of the bias-variance tradeoff. Thus, our preference is to have moderate bias and variance. The bottom line is that we do not want either bias or variance to be high.

- As complexity increases training error decreases, test error decreases but after after saddle point, test error increases again.
- If you have many training examples then the saddle point is at a higher complexity machine? If you have a few training example, then the saddle point is a lower complexity machine. So this says they're what complexity of machine you should use depends on how many training data samples you have. That is a very important assumption, especially when we have this present day phenomenon of deep learning.
- Deep learning is only applicable if you have large number of training examples.

**Q) Suppose that you want to use a machine to solve a problem, for which you have a low number of training examples. Should you use deep learning?**

- A) No, because deep learning is a complex machine, and a low number of training examples requires a simpler machine
  - The complexity of the machine you use depends on how many training examples you have. In a situation where you have a low number of training examples, you should use simpler machines (e.g., a support vector machine (SVM)). Only use a system like deep learning if you have a large number of training examples.

---

## Evaluation

### Model evaluation

- **Metrics for performance evaluation**
  - How to evaluate performance of a model?
  - Focus on the predictive capacity of model
  - Confusion metrix

| Predicted class |
| --------------- | --------- | --------- | -------- |
|                 |           | class=yes | class=no |
|                 |           | --------- | -------- |
| actual class    | class=yes | a         | b        |
|                 | class=no  | c         | d        |

```
Accuracy = (a + d)/(a + b + c + d) = (TP + TN) / (TP + TN + FP + FN)

* TP = TRUE positive
* FN = FALSE negative
* FP = FALSE positive
* TN = TRUE negative
* Falses are errors.
```

- If an application has a balance between the classes yes adn no, so the entire set is pretty balanced, that means that there is nearly equal number of yes classes, and equalnumber of no classes. In that case accuracy is a good measure.
- If there are cases where the distribution of class equals yes, and class equals no, then the distribution is heavily skewed. For example, let's say there are lot of yes classes and very few no classes, then accuracy is not a good metric, is not a reliable metric to evaluate the performance of model.

**Example) Limitation of accuracy: Class imbalance**

- Consider a 2-class problem
  - Number of class 0 examples = 9990
  - Number of class 1 examples = 10
- If model predicts everything to be class 0, accuracy is 9999/10000 = 99.9%.
  - Accuracy is misleading because model does not detect any class 1 example

### Strategy 1: Aletenative metrics

- True Positive rate
  - TPR = TP / (TP + FN)
- Tue negative rate
  - TNR = TN / (TN + FP)
- False positive rate
  - FPR = FP / (FP + TN)
- False negative rate

  - FNR = FN / (FN + TP)

- **Precision:**

  - Computes the fraction of records that actually turn out to be positive in the group the classifier has declared as positive class
  - Higher Precision implies a low number of false positive rrors committed by the classifier
  - ```
    p = TP / (TP + FP)
    ```

- **Recall:**

  - Recall computes the fraction of positive examples correctly predicted by the classifier
  - Higher recall implies very few positive examples are misclassified as the negative class
  - Recall is equivalent to the true positive rate (TPR)
  - ```
    r = TP / (TP + FN)
    ```

#### F_1 measure

```
p = TP / (TP + FP)
r = TP / (TP + FN)

F_1 = 2 / ((1 / r) + (1 / p)) = 2rp / (r + p)
```

- **Methods for performance evaluation**
  - How to obtain reliable estimates?
- **Methods for model comparison**
  - How to compare the relative performance among competing models?

**Q) In the confusion matrix, what do “a” and “d” represent?**

- A) "a” and “d” both represent the accuracy of the model.
  - According to the matrix, these values represent when the predicted class is the same as the actual class. For example, if the data point belongs in Class = Yes, the model predicts that the data point belongs in Class = Yes.

**Q) What is the definition of a False Negative (FN)?**

- A) The Actual Class=Yes, and the Predicted Class=No
  - A False Negative is when a datapoint that should belong to Class = Yes is incorrectly put in Class = No. Be sure to familiarize yourself with the definitions of the other ways we evaluate the performance of a model: False Positive (FP), True Positive (TP), and True Negative (TN).

**Q) One of the alternative metrics involves finding the sum of a and b from the confusion matrix. Which description is most accurate about a+b?**

- A) a+b = total number of instances that are positive
  - The sum TP+FN (or a+b in the confusion matrix) is the total number of instances that are Class=Yes. If you look at the entire training set, the total number of instances such that Class=Yes is fixed if you do not change the training dataset. This summation is used to calculate the True Positive Rate, which is an alternative metric to the measure of Accuracy calculated using the confusion matrix.

**Q) How do we calculate False Negative Rate?**

- FN / (FN + TP)
  - We calculate False Negative Rate by FNR = FN / (FN + TP). FNR is the complement of True Positive Rate (TPR).

**Q) How do we calculate precision?**

- TP / (TP + FP)
  - Precision is an alternative way of evaluating the performance of a machine. It computes the fraction of records that actually turn out to be positive in the group the classifier has declared as the positive class. A higher precision implies a lower number of False Positive errors committed by the classifier.

**Q) What does a high value of F_1 indicate?**

- It indicates that both precision and recall are high
  - F_1 is the combination of the precision and recall metrics. A good model will have high precision and high recall, which will result in a high F_1 value. It can be difficult to develop a model that maximizes both metrics, however.
