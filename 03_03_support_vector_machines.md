# Support vector machines

## Linear SVM Problem Formulation

- Has core assumption that any training with two classes can be separated by a line if it is in two-dimension, a plane if it is three-dimension, a hyperplane if it n-dimension
- Linear classifier
- How many such lines are possible?

```
SUM(w_i * x_i) + b
```

- The line maximally separates two classes (assumption)
- Definition of maximal separation?
  - Maximize distances between closest points to the line for different training sets (maximize d_1 + d_2)

### Linear SVM: separable case

- w is called support vectors

```
w.x_s + b = k, k > 0
w.x_c + b = k`, k` < 0
y = 1, if w.z + b > 0
y = -1, if w.z + b < 0

w.(x_1 - x_2) = 2
=> ||w||.d = 2, (taking magnitude on both sides of the equation)
=> d = 2 / ||w||
```

- **Training:**
  - An SVM involves estimating the parameters w and b from the training data
  - The parameters must be chosen in such way that the following two conditions are met:
  ```
  w.x_i + b >= 1, if y_i = 1
  w.x_i + b >= 1, if y_i = -1
  ```
  - Can combine both inequalities in a single inequality as follows:
  ```
  y_i.(w.x_i + b) >= 1, i = 1, 2, ..., N
  ```
  - Minimize (1/2).||w||^2, maximize d
- The learning task in an SVM can be formalized as the following optimization problem

```
L_p = (1/2).||w||^2- SUM(LAMBDA_i{y_i.(w.x_i + b) - 1}),
LAMBDA_i >= 0, i = 1, 2, ..., N
Where LAMBDA_i is Lagrangian multipliers

Primal problem:
w = SUM(LAMBDA_i.y_i.x_i), SUM(LAMBDA_i.y_i) = 0

Dual problem:
L_D = SUM(LAMBDA_i - (1/2).SUM(LAMBDA_i.LAMBDA_j.y_i.y_j.x_i.x_j)), Rewriting w in terms of LAMBDA_i
such that: LAMBDA_i >= 0, SUM(LAMBDA_i.y_i) = 0 => QP problem
```

- Once we solve the Lagrangian multipliers, we have:

```
w = SUM(LAMBDA_i.y_i.x_i)
Obtaining b,
LAMBDA_i.[_i.(w.x_i + b) - 1] = 0, i = 0, 1, ...,N

Substituting w:
y = 1, if SUM(LAMBDA_i.y_i.x_i.z) + b > 0
y = -1, if SUM(LAMBDA_i.y_i.x_i.z) + b < 0
```

- Consider the solution to the varibale w obtained before:
  ```
  w = SUM(LAMBDA_i.y_i.x_i)
  ```
- Support vectors:
  - Training samples with non-zero Lagrangian multipliers
- Support vector machine:
  - The decision boundary depends only on the support vectors (these training vectors support the decision boundary)
- w's are not the support vectors. The support vectors are the training data points that have non-zero Lagrangian multipliers.
- The non-zero lagrangian multipliers are the training data points that lie on the lines that are parallel to the solid lines.

## Example of Linear Separable SVM

## Non-separable SVM

- In the cases it is not separable
  ```
  [y_i(w.x_i + b) -1] = 0, cannot be hard constraint
  ```
- For non separable case:
  - w.x_i + b >= 1 - E, if y_i = 1, where E is Slack value
  - If you have more slack there is more penalty from slack

## Nonlinear SVM

- When you can't separate by a line, you can increase dimension
- Problem of dimensionality, is that you increase dimension the problem gets really complicated, so you don't want to increase dimension. You want to have few dimension as possible.
  - i.e. instead of plotting x_1 and x_2, transform variables to x_1 square and x_2 square
  - Kernel transformation when you use function to transform original value to something more manageable.
- Lower dimension space:
  - Input space
  - Original attribute space
- Higher dimensional space
  - Feature space
  - Kernal space: does not increase dimension, transforms variables.
  - Hilbert space
- Formulation stays the same for equations, but transform dimensions (apply a function)
- You need a transformation function phi, to convert your dimensions into something linear, you don't need to calculate phi, you just need to calculate some function f that is equivalent to to dot product of phi(x_i).phi(x_j). f is called kernal function.
- The dot product in the feature space can be expressed in terms of a similarity function in the original space.

```
K(x_i, x_j) = phi(x_i).phi(x_j)
```

- Similarity function
  - Function K is called **kernel function**
  - Cannot be used as kernel function
  - Kernel function computed for a pair of vectors should be equivalent to the dot product between the vectors in the feature space
  - ENsured by **Mercer's theorem**
- Kernel matrix (or gram matrix): Matrix of kernel functions

### Mercer's theorem

- **Theorem:**
  - The function K(:,:) is a valid kernel if and only if the corresponding gram matrix is symmetric and positive semi-definite (PSD)
- **Components:**
  - Mercer kernels
  - Kernel trick (you don't have to know transformation function phi)
- **Steps:**
  - Valid kernel
  - Entire computation is done in the lower dimensional input space
  - Curse of dimensionality can be avoided
  - Computing similarity using kernel functions much cheaper

**Commonly used kernels**

- Linear kernel
- Polynomial kernel of degree d
- Gaussian or radial basis function (RBF) kernel

### Multiclass SVM

- **One-against-rest (1-r) approach:**
  - Decomposes the multi-class problem into K binary problems
  - For each class y_i, a binary problem is created where all instances that belong to y_i are considered positive examples/remaining negative
  - Binary SVM is then trained to separate the positive and the negative examples
- **One-against-one (1-1) approach:**
  - Constructs K(K-1)/2 binary classifiers
  - Each classifier is used to distinguish between a pair of classes (y_i, y_j)
  - Instances that do not belong to either y_i or y_j are ignored while constructing the binary classifiers for (y_i, y_j)

### SVM Characteristics

- SVM learning problem can be formulated as a convex optimization problem, efficient algorithms can be used to find the global minimum of the objective function
- SVM's maximize the margin of the decision boundary; they are also called maximum margin models
- The user needs to provide parameters like the type of the kernel function and the kernel parameters and the value of the constant C to introduce the slack variables
- SVM's can be applied to categorical data vy indroducing dummy variables for each categorical attribute valie present in the data
- SVM's can be used for multiclass classification using the one-against-rest or the one-against-one approaches.
