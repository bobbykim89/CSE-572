# INTRO TO DEEP LEARNING
- The initial concept was in 1957 (perceptron).
- In this period, researchers were trying to come up with different structures (XOR, multilayer, SVM).
- Deep learning happened in 2006, it was not that popular.
- What changed was GPU and high computational capabilities. Then we can think of training a DNN since it is a very big computational problem.

## BIG DATA
- We have sensors at a very high frequency, giving a lot of data in a short period of time.
- We need to extract knowledge from this data, but the volume is high.
  - If you don't have a lot of data, then the complexity is low and you don't need DNN.
  - **If you have a LOT OF DATA, we need HIGH COMPLEXITY machines**. Hence DNN motivation.

## DEEP NEURAL NETWORK
1. ANN feed forward
2. Lots of hidden layers >10
   1. Each hidden layer has 50-100 nodes/neurons
   2. Complexity increases very fast because for each node you have 2 connections... you end up with a nx50x100 edges and so on for each layer.

## RECURRENT NEURAL NETWORK
- You have inputs, outputs, and a self loop that feeds the output back in.
- You can unroll the loop and plug in the output into a different hidden layer... and the output of that hidden layer goes into the next hidden layer... etc.
**You have infinite hidden layers.**
- Useful for solving SEQUENTIAL PROBLEMS (ex: extract time series data).

## RECURSIVE NEURAL NETWORK
- they are NOT recurrent NNs.
1. imagine **tree nets**... where you have a set of hidden nodes that act as a feed forward neural net.
2. The output of each node goes to another hidden layer and so on.
3. Useful for hierarchical data.

### Difference between recurrent and recursive
- Recurrent and recursive neural networks are closely related. Recurrent Neural Networks are used for processing sequential data. Recursive Neural Networks are better suited for hierarchical data due to their tree structure.
- both Recurrent Neural Networks and Recursive neural networks can be used for time series (sequential dadta). But Recursive neural networks have limited memory, are computationally expensive, and are difficult to handle variable-length sequences compared to Recurrent Neural Networks.

## CONVOLUTION NEURAL NETWORK
- Used to extract knowledge from images.
- 3D neural network
- Each node can perform a convolution operation.
1. you have an image and feed it to the CNN.
2. Each node on the CNN represents a small matrix of weights
3. You can do pixel-by-pixel convolution... you shift the box a little bit
- Any visual feature extraction is nothing but a **convolution with filters.**

Filter &rarr; a matrix of weights

## Popular tools 
- TensorFlow
- Keras
- Theano
- Caffe