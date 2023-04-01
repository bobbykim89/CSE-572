# Alternative data mining techniques

## Instance-based classifiers

### Instance based classifiers: examples

- **Rote-learner:**
  - Memorizes entire training data and performs classification only if attributes of record match one of the training examples exactly
- **Nearest neighbor:**
  - Uses k "closest" points (nearest neighbors) for performing classifcation

### Nearest neightbor classifiers

- **Requires these things:**
  - The set of stored records
  - Distance metric to compute distance between records
  - The value of k, the number of nearest neighbors to retrieve
- **To classify an unknown record:**
  - Compute distance to other training records
  - Identify _k_ nearest neighbors
  - Use class labels of nearest neighbors to determine the class label of unknown record

#### Nearest-neighbor: Voronoi diagram

- A way of partitioning the space so you can use later for segmentation

### Nearest neighbor classification

- **Compute distance between two points:**
  - Euclidean distance
    - ```
        d(p,q) = SQRT(SUM((p - q)^2))
      ```
- **Determine the class from nearest neighbor list:**
  - Take the majority vote of class laels among the k-nearest neighbors
  - Weigh the vote according to distance
    - weight factor, w = 1 / d^2
- **Choosing the value of k:**
  - If k is too small, sensative to noise points
  - If k is too large, neighborhood may include points from other classes
- **Scaling issues:**
  - Attributes may have to be scaled to prevent distance measures from being dominated by one of the attributes
- **Issues with data dimensionality**
  - Curse of dimensionality
- **k-NN classifiers are lazy learners**
  - It does not build models explicitly
  - Unlike eager learners such as decision tree induction
  - Classifying unknown records are relatively expensive

#### PEBLS (Parallel examplar-based learning system)

- Works with both continuous and nominal features
  - For nominal features, distance between two nomina values is computed using modified value difference metric (MVDM)
- Each record is assigned a weight factor
- Number of nearest neighbor, k = 1

```
d(V_1, V_2) = SUM(|(n_1i/n_1) - (n_2i/n_2)|)
*V_1, V_2 are attribute values

delta(X,Y) = w_x*w_y * SUM(d(X_i,Y_i)^2)
w_x = number of times X is used for prediction / number of times X predicts correctly
```

**PEBLS example:**

- Distance between nominal attribute values:

```
d(single, married) = |2/4 - 0/4| + |2/4 - 4/4| = 1
d(single, divorced) = |2/4 - 1/2| + |2/4 1/2| = 0
d(married, divorced) = |0/4 - 1/2| + |4/4 - 1/2| = 1
d(refund=Yes, refund=No) = |0/3 - 3/7| - |3/3 - 4/7| = 6/7
```

## Bayes classifier

- A probabilistic framework for solving classification problems
  - An `experiment` produces exactly one out of several possible outsomes
  - The set of all possible outcomes is called the `sample space` of the experiment
  - A subset of the sample space (a collection of possible outcomes) is called an `event`

### Bayes classifier: continuous random variables

- If we consider a random variable X and we have a sample space Omega. So random variable X is just a sampling from the sample space, and we do different types of sampling from the sample space, we'll get outcomes for the particular random variable, and if we have a sufficient number of outcomes and plot it along a real scale then that becomes a random variable. So random variable evolves over time. That means if you do more and more sampling, the random variable will have more and more different values.
- Random variables can be continuous as well as discrete.
  - If we have a random variable X that expresses the outcome of heads and tails or that expresses the outcome of a coin toss, then X can only take the value heads and tails. So then that case it is a discrete random variable.
  - If we are looking at temperature, if we're modeling temperature of a particular place over time, then that temperature can take any real value between zero degrees or maybe minus 20 degrees to 40 degrees. So in that case X is a continuous random variable.
- **Probability Mass Function (PMF):**
  - A discrete random variable X has an associated probability mass function (PMF) P_x(x), which denotes the probability that the random variable X can assume a value x.
  - The PMF of a discrete random variable X satisfies the following properties
    ```
    P(X = x) = f(x) >= 0
    SUM(f(x) = 1)
    P(X subgroup of A) = SUM(f(x))
    ```
- **Probability density function (PDF)**
  - A continuous random variable X has an associated probability density function (PDF) p_x(x), which denotes the probabiloity that the random variable X can assume a value within a given interval
  - The PDF of a continuous random variable X is an integrable function f(x) that satisfies the following properties:
  ```
  P(X = x) = f(x) >= 0
  ** Gaussian curve
  ```
- **The normal distribution:**
  - A very commonly used continuous probability distribution
  - The probability density function of a normal distribution is:
- **Prior probability / Marginal Probability:**
  - Prior knowledge about an event occurring
  - It is not conditioned on another event
  - Examples:
    - The probability that a card drawn at random from a fair deck of ards is red = p(red) = 0.5
    - The probability that a card drawn at random from a fair deck is a 4 = p(4) = 4/52 = 1/13
- **Joint probability**
  - The probability that two (or more) events occur simultaneously
  - It is the probability of the intersection of two or more events
  - For two random variables A and B, the joint probability is denoted by p(A,B)
  - Example:
    - The Probability that a card drawn at random from a fair deck is a 4 and red = p(4 and red) = 2/52 = 1/26
- **Conditional probability**
  - Probability that event occurs given that event B has already occurred
    ```
    P(A|B) = P(A, B) / P(B)
    ```
  - Out of the samples where B has occurred how many instances are there for A
- ```
  P(X, Y) = P(Y|X).P(X) = P(X|Y).P(Y)
  Bayes theorem:
  P(Y|X) = (P(X|Y).P(Y)) / P(X)
  ```
- Law of total probability
  - It is a fundamenta lrule relating marginal probabilities to conditional probabilities
  - ```
    P(A) = SUM(A|B_n).P(B_n)
         = P(A|B_1).P(B_1) + P(A|B_2).P(B_2) + ...
         = P(A, B_1) + P(A, B_2) + ...
    ```

## Bayes classifier example

### Law of total probability example

- Suppose that two factories supply light bulbs to the market
  - Factory X's bulbs work for over 5000 hours in 99% of cases
  - Factory Y's bulbs work for over 5000 hours in 95% of cases
  - It's known that factory X SUPPLIES 60% of total bulbs available. What is the probability that a purchased bulb will work for longer than 5000 hours?
  ```
  P(B = x) = 6 / 10, P(B = y) = 4 / 10
  P(A|B = x) = 0.99, P(A|B = y) = 0.95
  P(A) = P(A|B = x).P(B = x) + P(A|B = y).P(B = y)
       = 0.99 * 0.6 + 0.95 * 0.4
       = 0.974
  ```

### Bayes theorem example

- Given:
  - A doctor knows that meningitis causes stiff neck for 50% of time
  - Prior probability of any patient having meningitis 1/50000
  - Prior probability of any patient having stiff nexk is 1/20
  - If a patient has a stiff neck, what is the probability that he/she ha meningitis
  ```
  Prior probability of S, P(S) = 1 / 20
  Prior probability of M, P(M) = 1 / 50000
  Conditional probability of having stiff neck given the patient has meningitis, P(S|M) = 1/2
  There fore, conditional probability that the patient has meningitis, given he/she has stiff neck is
  P(M|S) = (P(S|M)P(M)) / P(S) = (0.5 * (1 / 50000)) / (1 / 20) = 0.0002
  ```

### Batesian classifiers

- **Conditional independencs:**
  - Let X, Y, and Z denote three random variables. X is said to be conditionally independent of Y given Z, if following condition holds:
    - ```
      P(X|Y,Z) = P(X|Z)
      ```
    - Example:
      - Relationship between a person's arm length and reading skills
      - One might observe that people with longer arms tend to have higher level of reading skills
      - Can be explained by the prescence of confounding factor, age.
      - A young child tends to have shorter arm and lacks the reading skills of an adult
      - If age of a person is fixed, then the observed relationship between arm length and reading skills disappears
      - Thus, the arm length and reading skills are conditionally independent, when age is fixed.
  - Consider three random variables X, Y and Z such that X is conditionally independent of Y given Z. We then have the following:
    - ```
      P(X,Y|Z) = P(X,Y,Z) / P(Z) *Bayes theorem
               = (P(X,Y,Z)/P(Y,Z)).(P(Y,Z) / P(Z))
               = P(X|Y,Z).P(Y|Z)
               = P(X|Z).P(Y|Z) *Conditional independence
      ```
    - Thus, the conditional independence X and Y given Z implies the following,
      - ```
        P(X,Y|Z) = P(X|Z).P(Y|Z)
        ```

**Naive bayes classifiers simplifies it with one assumption**

## Naive Bayes classifier

### How to estimate probability from data

- **Class:** P(C) = N_c / N
- For discrete attributes: P(A_i | C_k) = |A_ik| / N_c
- For continuous attributes:
  - Discretize each continuous attribute
  - Replace with its corresponding discrete interval
  - Compute conditional probability
    - P(X_i | Y = y)
  - Watch for estimation errors
- Gaussian distribution

### Example of Naive Bayes classifier

X = (refund = no, married, income = 120k)

```
P(X|class = no) = P(refund = no|class = no)
* P(married | class = no)
* P(income = 120k | class = no)
= 4 / 7 * 4 / 7 * 0.0072 = 0.0024

P(X | class = yes) = P(Refund = no | class = yes)
                     * P(married | class = yes)
                     * P(income = 120k | class = yes)
                     = 1 * 0 = 1.2 * 12^-9

P(no | X) > P(yes | X)
=> No else yes
P (N_o | X) = [P(N_o)P(X|N_o)] / P(x)
```

### Naive Bayes classifier: probability estimation

- **Original:** P(A_i|C) = N_ic / N_c
- **Laplace::** P(A_i|C) = (N_ic + 1) / (N_c + c)
- **m-estimate:** P(A_i|C) = (N_ic + mp) / (N_c + m) where m, p is some random number

### Naive bayes (Summary)

- Robust to isolated noise points are averaged out when estimating conditional probability
- Handle missing values by ignoring the instance during probability estimate calculations
- Robust to irrevalent attributes
- Correlated attributes can degrade the performance of classifiers as the conditional independence assumption no longer holds
