---
title: "Supervised Learning"
---

# Supervised Learning

Supervised learning is one of the core methods in machine learning, where a model learns from labeled examples to make predictions or decisions. Essentially, it’s like teaching a model by example: you give it a bunch of input-output pairs, and it tries to learn the relationship between them. The ultimate goal is to train the model so it can predict the correct output for new, unseen data. In this guide, we'll explore the history of supervised learning, its mathematical underpinnings, and practical implementations. Plus, we'll dive into some Python code examples to bring these concepts to life.

## Historical Context

The roots of supervised learning stretch back to the early days of statistical analysis and pattern recognition. In the mid-20th century, techniques like linear regression emerged, aimed at understanding relationships between variables. These early methods laid the foundation for what we now call supervised learning.

The term "supervised learning" gained traction in the 1980s and 1990s as machine learning research picked up steam. During this time, new algorithms such as decision trees, support vector machines, and neural networks began to take shape. This progress was fueled by advances in computing power and the rise of large datasets.

A major milestone in the history of supervised learning was the development of the backpropagation algorithm in the 1980s. This breakthrough enabled effective training of deep neural networks, sparking significant advancements in AI and machine learning. Today, supervised learning is a cornerstone of many applications, from image and speech recognition to natural language processing.

## Mathematical Foundations

At the heart of supervised learning is the concept of mapping functions and optimization. The idea is to learn a function {{< katex >}} f{{< /katex >}} that maps inputs {{< katex >}} \mathbf{x}{{< /katex >}} to outputs {{< katex >}} \mathbf{y}{{< /katex >}} based on a set of training examples. Mathematically, this is expressed as:

{{< katex >}} \mathbf{y} = f(\mathbf{x}){{< /katex >}}

where {{< katex >}} \mathbf{x}{{< /katex >}} represents the input features, and {{< katex >}} \mathbf{y}{{< /katex >}} represents the output labels. The goal is to find a function {{< katex >}} f{{< /katex >}} that minimizes the difference between the predicted outputs and the actual labels.

### Loss Functions

A key component of supervised learning is the loss function, which measures how well the model's predictions match the true outputs. Two common loss functions are mean squared error (MSE) for regression tasks and cross-entropy loss for classification tasks.

#### Mean Squared Error (MSE)

For regression tasks, MSE calculates the average squared difference between predicted values and actual values. The MSE loss function is given by:

{{< katex >}} \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2{{< /katex >}}

where {{< katex >}} n{{< /katex >}} is the number of samples, {{< katex >}} y_i{{< /katex >}} is the true value, and {{< katex >}} \hat{y}_i{{< /katex >}} is the predicted value.

##### Example

Here’s a Python implementation of MSE:

```python
import numpy as np

# Define the mean squared error function
def mean_squared_error(y_true, y_pred):
    return np.mean((y_true - y_pred) ** 2)

# Sample data
y_true = np.array([3.0, -0.5, 2.0, 7.0])
y_pred = np.array([2.5, 0.0, 2.1, 7.8])

# Calculate MSE
mse = mean_squared_error(y_true, y_pred)
print(f"Mean Squared Error: {mse}")
```

In this example, we define a function to compute the mean squared error between true and predicted values and then calculate it for a sample dataset.

#### Cross-Entropy Loss

For classification tasks, cross-entropy loss evaluates the performance of a classification model by comparing the predicted probability distribution with the true distribution. The cross-entropy loss function is:

{{< katex >}} \text{Cross-Entropy} = -\frac{1}{n} \sum_{i=1}^{n} \sum_{k=1}^{K} y_{ik} \log(\hat{y}_{ik}){{< /katex >}}

where {{< katex >}} n{{< /katex >}} is the number of samples, {{< katex >}} K{{< /katex >}} is the number of classes, {{< katex >}} y_{ik}{{< /katex >}} is a binary indicator (0 or 1) if class label {{< katex >}} k{{< /katex >}} is the correct classification for sample {{< katex >}} i{{< /katex >}}, and {{< katex >}} \hat{y}_{ik}{{< /katex >}} is the predicted probability of class {{< katex >}} k{{< /katex >}} for sample {{< katex >}} i{{< /katex >}}.

##### Example

Here’s a Python implementation of cross-entropy loss:

```python
import numpy as np

# Define the cross-entropy loss function
def cross_entropy_loss(y_true, y_pred):
    epsilon = 1e-15  # Small value to avoid log(0)
    y_pred = np.clip(y_pred, epsilon, 1. - epsilon)
    return -np.mean(y_true * np.log(y_pred))

# Sample data
y_true = np.array([1, 0, 0, 1])
y_pred = np.array([0.9, 0.1, 0.2, 0.8])

# Calculate cross-entropy loss
cross_entropy = cross_entropy_loss(y_true, y_pred)
print(f"Cross-Entropy Loss: {cross_entropy}")
```

In this example, we calculate the cross-entropy loss between true labels and predicted probabilities, ensuring numerical stability with `np.clip`.

### Gradient Descent

Gradient descent is an optimization technique used to minimize the loss function by iteratively adjusting model parameters. The idea is to compute the gradient of the loss function with respect to the parameters and move in the direction that reduces the loss.

The gradient descent update rule for a parameter {{< katex >}} \theta{{< /katex >}} is:

{{< katex >}} \theta = \theta - \eta \frac{\partial L}{\partial \theta}{{< /katex >}}

where {{< katex >}} \eta{{< /katex >}} is the learning rate, and {{< katex >}} \frac{\partial L}{\partial \theta}{{< /katex >}} is the gradient of the loss function with respect to {{< katex >}} \theta{{< /katex >}}.

#### Example

Here’s a Python implementation of gradient descent for a simple linear regression model:

```python
import numpy as np

# Define the linear regression model
def linear_regression(X, y, learning_rate, num_iterations):
    m, n = X.shape
    theta = np.zeros(n)
    
    for _ in range(num_iterations):
        predictions = X.dot(theta)
        errors = predictions - y
        gradient = (1 / m) * X.T.dot(errors)
        theta -= learning_rate * gradient
    
    return theta

# Sample data
X = np.array([[1, 1], [1, 2], [1, 3]])
y = np.array([1, 2, 3])

# Parameters
learning_rate = 0.01
num_iterations = 1000

# Run gradient descent
theta = linear_regression(X, y, learning_rate, num_iterations)
print(f"Optimal parameters: {theta}")
```

In this example, we use gradient descent to fit a linear regression model. We initialize parameters, compute predictions, and iteratively update the parameters to minimize the error.

## Types of Supervised Learning

Supervised learning can be broadly categorized based on the nature of the output variable:

### Classification

Classification involves predicting a categorical label for each input sample. Examples include recognizing objects in images or classifying emails as spam or not spam.

#### Example

Let’s implement a simple classification algorithm using logistic regression:

```python
import numpy as np
from scipy.special import expit  # Sigmoid function

# Define the logistic regression model
def logistic_regression(X, y, learning_rate, num_iterations):
    m, n = X.shape
    theta = np.zeros(n)
    
    for _ in range(num_iterations):
        predictions = expit(X.dot(theta))
        errors = y - predictions
        gradient = (1 / m) * X.T.dot(errors)
        theta += learning_rate * gradient
    
    return theta

# Sample data
X = np.array([[1, 0], [1, 1], [1, 2], [1, 3]])
y = np.array([0, 0, 1, 1])

# Parameters
learning_rate = 0.1
num_iterations = 1000

# Run logistic regression
theta = logistic_regression(X, y, learning_rate, num_iterations)
print(f"Optimal parameters: {theta}")
```

In this code, we use logistic regression to classify input samples into two classes. The sigmoid function converts predictions into probabilities, and we update parameters using gradient ascent.

### Regression

Regression involves predicting a continuous value for each input sample. Examples include predicting house prices based on features or forecasting stock prices.

#### Example

Here’s a Python implementation of polynomial regression:

```python
import numpy as np

# Define the polynomial regression model
def polynomial_regression(X, y, degree, learning_rate, num_iterations):
    m = X.shape[0]
    X_poly = np.vstack([X**i for i in range(degree + 1)]).T
    theta = np.zeros(X_poly.shape[1])
    
    for _ in range(num_iterations):
        predictions = X_poly.dot(theta)
        errors = predictions - y
        gradient = (1 / m) * X_poly.T.dot(errors)
        theta -= learning_rate * gradient
    
    return theta

# Sample data
X = np.array([1, 2, 3, 4])
y = np.array([2, 8, 18, 32])

# Parameters
degree = 2
learning_rate = 0.01
num_iterations = 1000

# Run polynomial regression
theta = polynomial_regression(X, y, degree, learning_rate, num_iterations)
print(f"

Optimal parameters: {theta}")
```

In this example, we perform polynomial regression to fit a polynomial function to the data. Gradient descent helps us find the best-fitting polynomial coefficients.

### Evaluation Metrics

To evaluate the performance of supervised learning models, various metrics are used depending on the task. For classification, metrics like accuracy, precision, recall, and F1 score are commonly used. For regression, metrics such as mean squared error (MSE) and R-squared are often employed.

#### Example

Let’s compute accuracy for a classification task:

```python
import numpy as np

# Define the accuracy function
def accuracy(y_true, y_pred):
    return np.mean(y_true == y_pred)

# Sample data
y_true = np.array([1, 0, 1, 1])
y_pred = np.array([1, 0, 1, 0])

# Calculate accuracy
acc = accuracy(y_true, y_pred)
print(f"Accuracy: {acc}")
```

In this example, we calculate the accuracy of predicted labels by comparing them to the true labels.

## Image Illustrations

To make these concepts more concrete, here are some illustrative diagrams:

### Linear Regression

![Linear Regression](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Linear_regression.svg/438px-Linear_regression.svg.png?20160331104215)
*Figure 1: Illustration of linear regression.*

This image shows how linear regression fits a straight line to data points, aiming to minimize the mean squared error between predictions and actual values.

### Logistic Regression

![Logistic Regression](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cb/Exam_pass_logistic_curve.svg/609px-Exam_pass_logistic_curve.svg.png?20220327133556)
*Figure 2: Illustration of logistic regression.*

Here’s a diagram of the sigmoid function used in logistic regression to convert predictions into probabilities between 0 and 1.

### Decision Trees

![Decision Trees](https://upload.wikimedia.org/wikipedia/commons/f/ff/Decision_tree_model.png?20080123145148)
*Figure 3: Illustration of a decision tree.*

A decision tree splits data based on feature values to make predictions, useful for both classification and regression tasks.