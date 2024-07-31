---
title: "Basic Neural Networks (Perceptrons)"
---

# Neural Network Basics: Perceptrons

Neural networks are at the core of today's AI and machine learning breakthroughs, and the perceptron is one of the simplest yet fundamental components of these networks. Understanding perceptrons is key to grasping more complex neural network architectures. Let’s explore what perceptrons are all about, including their history, how they work, and a practical code example.

## Historical Context

The perceptron concept was introduced by Frank Rosenblatt in 1958. Rosenblatt was inspired by how the human brain processes information, aiming to mimic its functionality. His perceptron was one of the earliest algorithms that could "learn," marking a significant advancement in AI. Despite its promise, the perceptron had limitations, like struggling with problems that aren’t linearly separable (e.g., the XOR problem). This critique, detailed in Minsky and Papert’s 1969 book "Perceptrons," led to a dip in neural network research. However, the field revived in the 1980s with the development of multi-layer perceptrons and backpropagation.

## The Perceptron Model

At its core, a perceptron is a basic type of neural network used for binary classification tasks. It consists of an input layer, weights, a bias term, and an activation function. The perceptron model can be expressed with this equation:

<center>
{{< katex >}}y = \phi(\mathbf{w} \cdot \mathbf{x} + b){{< /katex >}}
</center>

where:
- {{< katex >}}\mathbf{x}{{< /katex >}} is the input vector.
- {{< katex >}}\mathbf{w}{{< /katex >}} is the weight vector.
- {{< katex >}}b{{< /katex >}} is the bias term.
- {{< katex >}}\phi{{< /katex >}} is the activation function.
- {{< katex >}}y{{< /katex >}} is the output.

The activation function {{< katex >}}\phi{{< /katex >}} is usually a step function, outputting 1 if the input exceeds a certain threshold and -1 otherwise.

### Mathematical Formulation

Given an input vector {{< katex >}}\mathbf{x} = [x_1, x_2, ..., x_n]{{< /katex >}} and a weight vector {{< katex >}}\mathbf{w} = [w_1, w_2, ..., w_n]{{< /katex >}}, the perceptron calculates the weighted sum as follows:

<center>
{{< katex >}}z = \mathbf{w} \cdot \mathbf{x} + b = \sum_{i=1}^{n} w_i x_i + b{{< /katex >}}
</center>

The activation function then determines the output {{< katex >}}y{{< /katex >}}:

<center>
{{< katex >}}y = \phi(z) = \begin{cases} 
      1 & \text{if } z \geq 0 \\
      -1 & \text{if } z < 0 
   \end{cases}
{{< /katex >}}
</center>

### Training the Perceptron

Training a perceptron involves adjusting the weights and bias based on prediction errors. The perceptron learning algorithm updates the weights and bias using the following rules:

<center>
{{< katex >}}w_i \leftarrow w_i + \Delta w_i{{< /katex >}}
{{< katex >}}b \leftarrow b + \Delta b{{< /katex >}}
</center>

where:
- {{< katex >}}\Delta w_i = \eta (y - \hat{y}) x_i{{< /katex >}}
- {{< katex >}}\Delta b = \eta (y - \hat{y}){{< /katex >}}

Here, {{< katex >}}\eta{{< /katex >}} is the learning rate, {{< katex >}}y{{< /katex >}} is the true label, and {{< katex >}}\hat{y}{{< /katex >}} is the predicted label.

## Code Example

Here’s how you can implement a perceptron in Python from scratch, using NumPy for numerical operations. This example shows how the perceptron learning algorithm works with a simple dataset.

```python
import numpy as np

# Step function as the activation function
def step_function(x):
    return np.where(x >= 0, 1, -1)

# Perceptron class
class Perceptron:
    def __init__(self, input_size, learning_rate=0.01):
        self.weights = np.zeros(input_size)
        self.bias = 0
        self.learning_rate = learning_rate

    def predict(self, x):
        z = np.dot(self.weights, x) + self.bias
        return step_function(z)

    def train(self, X, y, epochs=100):
        for _ in range(epochs):
            for xi, target in zip(X, y):
                prediction = self.predict(xi)
                update = self.learning_rate * (target - prediction)
                self.weights += update * xi
                self.bias += update

# Sample dataset: AND logic gate
X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])
y = np.array([-1, -1, -1, 1])

# Create and train the perceptron
perceptron = Perceptron(input_size=2)
perceptron.train(X, y)

# Test the perceptron
for xi in X:
    print(f"Input: {xi}, Prediction: {perceptron.predict(xi)}")
```

In this code, we define a simple `Perceptron` class with methods for predicting and training. We train the perceptron on the AND logic gate dataset, where the output is 1 only if both inputs are 1, and -1 otherwise. The training process involves updating the weights and bias based on the difference between predicted and actual values.