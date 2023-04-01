# Artificial neural networks basics

## Perceptron

- Mathematical function
  - inputs i (with weights w)
  - bias b
- Lets say there is a mathematical function
  ```
  SIGMA(w_1 * i_1 + w_2 * i_2 + b) = output
  * where SIGMA is Activation function (acts as an on/off switch)
  ```
  - Basic perceptrion
    - n - inputs
    - 1st stage, SUM(w_k \* i_k) + b, linear
    - 2nd stage, o = SIGMA(SUM(w_k \* i_k) + b), can be non linear
    - What perceptron allows you to do is it allows you to encode nonlinear functions of the input. So it allows you to encode output as a nonlinear function of the input
  - Benefit of neuron
    - You can change the weights such that for training dataset you can have output for a class you want.

### Multilayer perceptron

- input i, perceptron k, another perceptron p
- How can it be used for classification?
  ```
  c = f(i_1, ... , i_n) an expected output of MLP
  ```

### Decision boundary

### Multilayer artificial newral network

- Input layer
- Output layer
- Any layers that are not input/output is hidden layer

### Feed-forward neural network

- Arrows are all directed from input layer to hidden layer to output layer
- Can't be reversed

### Recurrent neural network

- Recurrent neural network is for your unfold (for loop), then it gives an infinite number of layers.

### Common types of activation functions

- Linear function
- Signmoid function
- Tanh function
- Sign function
- Artificial neural networks has the property that can encode nonlinearities

## Perceptron learning algorithm

### Artificial neural networks

- Perceptron is a **supervised learning algorithm** of binary classifiers
- It is a linear classifier
  - A classification algorithm that makes its predictions based on a linear predictor function combining a set of weights with the feature vector
- The algorithm allows for online learning
  - It processes elements in the training set one at a time
- Perceptron have n inputs i with corresponding weight w,
- Perceptron algorithm, we try to figure out what are weights

### Learning perception model

- The key computation for this algorithm is the weight update formula in step 7 of the algorithm (k denotes the current iteration and k + 1 denotes the next iteration)

```
w_j^(k+1) = w_j^k + LAMBDA(y_i - y(hat)_i^(k)) * x_ij
* where,
w_j^(k+1) is weight of the jth attribugte in the next iteration
w_j^k is weight of the jth attribute in the current iteration
LAMBDA is learning rate
y_i - y(hat)_i^(k) is prediction error
x_ij is value of jth attribute of training example x_i
```

- in the weight update formula, the weights should not be changed too drastically between one iteration and the next
- The learning rate (lambda) has a value between - and 1 and is used to control the amount of adjustment made in each iteration
- In some cases, an adaptive value ob lambda can be used

### Perceptron

- Guaranteed to converge to an optimal solution (as long as the learning rate is sufficiently small) for linearly separable classification problems
- If the problem is not linearly separable, the algorithm fails to converge

## Artificial Neural Networks Learning with Backpropogation

### Learning the ANN model

- Algorithm:
  - Need an efficient algorithm that converges to the right solutions when sufficient training data is provided
- Approach:
  - Treat each hidden node or output node in the network as an independent perception and apply the same weight update formula
- Disadvantage:
  - Have no knowledge about the true outputs of hidden nodes
  - Difficult to determine the error term associated with each hidden node

We need to find global minima
Newton Rhapson equation
Initial guess is very important

- The goal of the ANN learning algorithm is to determine a set of weights w that minimize the total sum of squared errors

```
E(w) = (1 / 2) * SUM((y_i - Y(hat))^2)
```

### Gradient descent model

- Algorithms based on gradient descent method have been developed to efficiently solve the optimization problem
- The weight update formula used by gradient descent is:

```
w_j = w_j - LAMBDA * (LearningRate * E(w)) / (LearningRate * W_j)
```

### Backpropagation

- init -> random
- You know the right answer (training data), you throw random weight, generate random output, and compare it with real answer from training data.

### Design issues in ANN learning

- Input layer:
  - Determine number of nodes
  - Assign an input node to each of the input features
- Output Node:
  - Determine number of nodes
- Select network topology:
  - Weights and biases need to be initialized
  - Perform random initialization
  - Training examples with missing values should be removed or replaced

### Characteristics of ANN

- Multilayer neural networks
  - Important to select the appropriate network topology
- Redundant features
  - Can be used as weights
- Training data
  - Neural networks are sensitive to the presence of noise
  - Gradient descent method used for learning the weights of ANN converges to some local optimum
  - Time consuming process
