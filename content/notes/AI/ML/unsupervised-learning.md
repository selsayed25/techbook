---
title: "Unsupervised Learning"
---

# Unsupervised Learning

Unsupervised learning is a fascinating area of machine learning focused on uncovering hidden patterns or structures in data that hasn't been labeled or categorized. Unlike supervised learning, where you train a model with known input-output pairs, unsupervised learning dives into the data to find out what’s underneath without any predefined labels. This technique is crucial for exploring data, reducing its complexity, and clustering similar items together.

## A Brief History

Unsupervised learning has its roots in the early days of statistics and pattern recognition. Back in the 1960s and 70s, key methods like principal component analysis (PCA) and cluster analysis were developed to simplify data and find groups of similar items.

A major breakthrough came with clustering algorithms like k-means and hierarchical clustering. These methods helped in grouping data points based on their similarities, giving us valuable insights into the data's structure.

In the 1990s and 2000s, the field advanced with more sophisticated techniques such as Gaussian mixture models (GMMs) and t-Distributed Stochastic Neighbor Embedding (t-SNE). The explosion of big data and advancements in computational power accelerated these methods, making them widely used in various fields.

## The Math Behind It

Unsupervised learning covers a range of techniques, each with its own set of mathematical principles. The key areas include clustering, dimensionality reduction, and density estimation.

### Clustering

Clustering is all about grouping similar data points together. The goal is to divide the data into clusters where items in the same cluster are more alike than those in different clusters.

**K-Means Clustering**

K-means is a popular clustering algorithm that divides data into {{< katex >}}k{{< /katex >}} clusters by minimizing the variance within each cluster. Here's a quick rundown of how it works:

1. Start with {{< katex >}}k{{< /katex >}} randomly chosen cluster centroids.
2. Assign each data point to the nearest centroid.
3. Update the centroids by computing the average of the points assigned to each cluster.
4. Repeat the assignment and update steps until the centroids no longer change.

Here's a simple Python example:

```python
import numpy as np

# K-means clustering algorithm
def k_means(X, k, num_iterations=100):
    centroids = X[np.random.choice(X.shape[0], k, replace=False)]
    
    for _ in range(num_iterations):
        distances = np.linalg.norm(X[:, np.newaxis] - centroids, axis=2)
        clusters = np.argmin(distances, axis=1)
        
        new_centroids = np.array([X[clusters == i].mean(axis=0) for i in range(k)])
        
        if np.all(centroids == new_centroids):
            break
        
        centroids = new_centroids
    
    return centroids, clusters

# Example data
X = np.array([[1, 2], [1, 4], [1, 0], [4, 2], [4, 4], [4, 0]])

# Run k-means
centroids, clusters = k_means(X, k=2)
print(f"Centroids:\n{centroids}")
print(f"Clusters:\n{clusters}")
```

**Hierarchical Clustering**

Hierarchical clustering builds a tree-like structure of clusters. There are two main types:

1. **Agglomerative Clustering:** Starts with individual points and merges them iteratively.
2. **Divisive Clustering:** Begins with all data as one cluster and splits it iteratively.

Here’s how you can perform hierarchical clustering:

```python
from scipy.spatial.distance import pdist, squareform
from scipy.cluster.hierarchy import linkage, fcluster

def hierarchical_clustering(X, t):
    distances = pdist(X, metric='euclidean')
    linkage_matrix = linkage(distances, method='ward')
    clusters = fcluster(linkage_matrix, t=t, criterion='maxclust')
    
    return linkage_matrix, clusters

# Example data
X = np.array([[1, 2], [1, 4], [1, 0], [4, 2], [4, 4], [4, 0]])

# Run hierarchical clustering
linkage_matrix, clusters = hierarchical_clustering(X, t=2)
print(f"Linkage Matrix:\n{linkage_matrix}")
print(f"Clusters:\n{clusters}")
```

### Dimensionality Reduction

Dimensionality reduction is about simplifying data by reducing its features while keeping the core structure intact. This is useful for visualizing high-dimensional data and speeding up computations.

**Principal Component Analysis (PCA)**

PCA is a common technique for dimensionality reduction. It transforms data into a new coordinate system where the largest variance is captured on the first axis (principal component), the second largest on the next axis, and so on.

Here’s a basic example of PCA in Python:

```python
import numpy as np

def pca(X, num_components):
    X_centered = X - np.mean(X, axis=0)
    covariance_matrix = np.cov(X_centered, rowvar=False)
    eigenvalues, eigenvectors = np.linalg.eigh(covariance_matrix)
    
    sorted_indices = np.argsort(eigenvalues)[::-1]
    eigenvectors = eigenvectors[:, sorted_indices]
    eigenvalues = eigenvalues[sorted_indices]
    
    principal_components = eigenvectors[:, :num_components]
    X_reduced = X_centered.dot(principal_components)
    
    return X_reduced

# Example data
X = np.array([[1, 2], [1, 4], [1, 0], [4, 2], [4, 4], [4, 0]])

# Run PCA
X_reduced = pca(X, num_components=1)
print(f"Reduced Data:\n{X_reduced}")
```

**t-Distributed Stochastic Neighbor Embedding (t-SNE)**

t-SNE is a technique for visualizing high-dimensional data in a lower-dimensional space. It minimizes the divergence between the probability distributions of pairwise similarities in high-dimensional and low-dimensional spaces.

Here’s a simple version of t-SNE:

```python
import numpy as np
from scipy.spatial.distance import pdist, squareform

def tsne(X, num_components, perplexity=30.0, num_iterations=1000):
    distances = pdist(X, metric='euclidean')
    distances = squareform(distances)
    
    P = np.exp(-distances ** 2 / (2 * perplexity**2))
    P = P / np.sum(P, axis=1, keepdims=True)
    
    Y = np.random.randn(X.shape[0], num_components)
    
    for _ in range(num_iterations):
        distances_Y = pdist(Y, metric='euclidean')
        distances_Y = squareform(distances_Y)
        
        Q = np.exp(-distances_Y**2)
        Q = Q / np.sum(Q, axis=1, keepdims=True)
        
        gradient = (P - Q) @ Y
        Y += gradient * 0.1
    
    return Y

# Example data
X = np.array([[1, 2], [1, 4], [1, 0], [4, 2], [4, 4], [4, 0]])

# Run t-SNE
X_reduced = tsne(X, num_components=2)
print(f"Reduced Data:\n{X_reduced}")
```

## Visual Aids

To help visualize these concepts, here are some diagrams:

**K-Means Clustering**

![K-Means Clustering](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/K-means_convergence.gif/617px-K-means_convergence.gif?20170530143526)
*Figure 1: How k-means clustering refines clusters.*

**Principal Component Analysis (PCA)**

![Principal Component Analysis](https://upload.wikimedia.org/wikipedia/commons/thumb/d/db/3D_PCA_of_Kuwaiti.png/800px-3D_PCA_of_Kuwaiti.png?20210111115832)
*Figure 2: PCA projecting data into a lower-dimensional space.*

**t-Distributed Stochastic Neighbor Embedding (t-SNE)**

![t-SNE](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/T-SNE_Embedding_of_MNIST.png/621px-T-SNE_Embedding_of_MNIST.png?20220303091655)
*Figure 3: t-SNE visualizing high-dimensional data in two dimensions.*