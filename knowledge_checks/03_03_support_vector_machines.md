# Knowledge Check - Support Vector Machines

1. True or False? Support Vector Machines (SVM) perform badly on high dimension data.
   - False
     - The dimensionality of data does not affect the performance of SVMs.
2. What are the advantages of having decision boundaries with a large margin in Support Vector Machines? (select all that apply)
   - A large margin implies there is a high confidence in classification.
     - Large margins generalize well.
   - If the margin is small, then any slight perturbation to the decision boundary can have quite a significant impact on its classification.
     - Large margins generalize well.
   - Decision boundaries with large margin tend to have better generalization errors.
     - Large margins will lead to maximally separate classes which would generalize well.
3. What are the different ways of multi-class SVM solution? (select all that apply)
   - For each pair of classes, build a One vs. One SVM.
     - One vs. One \ One vs. rest
   - For each class, build a One vs. Rest SVM
     - One vs. One \ One vs. rest
4. Suppose we are given the following positively labeled data points in:

```
(3,1),(3,−1),(6,1),(6,−1)
```

and the following negatively labeled data points in:

```
(1,0),(0,1),(0,−1),(−1,0).
```

What is the equation of the decision boundary? - X−2=0 5. In the above example, which ones are the support vectors?

- (3,1),(3,−1),(1,0)
  - The training points that are closest to the decision boundary.

6. Figure 5: Support VectorMachine (SVM) Dataset

| X      | Y      | Class |
| ------ | ------ | ----- |
| 0.5    | 0.866  | +     |
| 0.866  | 0.5    | +     |
| 0.7071 | 0.5    | +     |
| 0      | 1      | +     |
| 1.732  | 1      | -     |
| 1.4142 | 1.4142 | -     |
| 2      | 0      | -     |
| 1      | 1.732  | -     |

Review the table labeled Figure 5: Support Vector Machine (SVM) Dataset.
Your friend has asked you to train a Support Vector Machine (SVM) on the provided dataset. You check the dataset, which is two dimensional, and understand that there is no hyperplane that can completely separate the two classes. Therefore, linear SVM is not the best option.
If you transform the data into three dimensions , and you decide to use non-linear SVM, which hyperplane will the SVM provide for separating the two classes?

- $\x^2 + y^2 = 2.5
