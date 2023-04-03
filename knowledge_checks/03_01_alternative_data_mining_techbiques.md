# Knowledge Check - Alternative Data Mining Techniques

1. True or False? Naïve Bayes Classifier assumes that the attributes are conditionally independent given the class.
   - True
     - Naïve Bayes Classifier assumes sample attributes are conditionally independent given the class labels. Dependence among attribute will lead to more computationally expensive models which would require its own set of simplifying assumptions.
2. To describe K-Nearest Neighbors (K-NN) classifiers as being “lazy learners” means. (select all that apply)
   - They do not build models explicitly
     - K-NN in training phase only decides on the exact distance metric measure and number of neighbors to be used in decision making for prediction. No model is learnt during training phase and at test phase a sample needs to be compared with all sample instances in training set.
   - Classifying unknown records is relatively expensive.
     - K-NN spends more computation time in the testing phase than in training phase, as it needs to calculate distance between test samples with all sample instances in training set, find the nearest ones and and make decision.
3. What are some challenges of K-Nearest Neighbors (K-NN) classifiers? (select all that apply)
   - Attribute Scaling
     - To prevent distance measures being dominated by one or few of the attributes.
   - Choosing number of neighbors.
     - Performance directly depend on the exact number of neighbors that are checked.
   - Data Dimensionality
     - high dimension data would have on average less distance between data samples and lead to curse of dimensionality.
4. Question 4
   Consider that Y = wealth, and X1 = Gender, X2 = Hours worked.
   Let us consider the following data:

```
P(Y = rich, X1 = Female, X2 < 40.5) = 0.0245895
P(Y = poor, X1 = Female, X2 < 40.5) = 0.253122
P(Y = rich, X1 = Female, X2 >= 40.5) = 0.0116293
P(Y = poor, X1 = Female, X2 >= 40.5) = 0.0421768
P(Y = rich, X1 = male, X2 < 40.5) = 0.0971295
P(Y = poor, X1 = male, X2 < 40.5) = 0.331313
P(Y = rich, X1 = male, X2 >= 40.5) = 0.105933
P(Y = poor, X1 = male, X2 >= 40.5) = 0.134106
```

Based on these information, compute P(Y = rich | X1 = Female, X2 < 40.5).

- 0.09
  - The answer is found using Bayes Theorem: P(Y|X) = P(X,Y) \* P(X) and then applying law of total probability: P(A) = P(A|B_1)P(B_1) + … + P(A|B_n)P(B1_n).

5. Based on these information, compute P(Y = rich | X1 = Female, X2 < 40.5) using Naive Bayes assumption of conditional independence.
   - 0.067
     - The answer is found using Bayes Theorem and conditional independence calculations.
6. What is the advantage of using Laplace probability estimation in Naïve Bayes Classifier? (select all that apply)
   - Probability does not get to infinity if there are no samples from specific class.
     - In Laplace estimation, we add a constant value to the denominator.
   - Probability does not get to zero if a certain attribute value never occurs in a specific class.
     - In Laplace estimation, we add one to the numerator
7. What are the advantaged of Naïve Bayes Classifier? (select all that apply)
   - Robust to irrelevant attributes
     - Such attributes do not skew the probability estimation.
   - Robust to isolated noise points
     - Averaging happens during probability estimation.
   - Handles missing attribute values.
     - It will be ignored during probability estimation.
