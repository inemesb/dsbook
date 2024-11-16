---
kernelspec:
  display_name: Python 3
  language: python
  name: python3
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
---
# Autoencoders

## Introduction

Autoencoders are a general framework used to learn efficient representations of data, often for dimensionality reduction or feature extraction. They operate by training a model to compress input data into a lower-dimensional representation and then reconstruct the original data from that compressed form. The primary goal of an autoencoder is not merely to copy the input, but rather to discover meaningful patterns and structures that capture the underlying features in a more compact representation.

An autoencoder consists of two main components: the encoder and the decoder. The encoder is responsible for compressing the input into a latent space representation, often called the bottleneck, which is typically of lower dimension than the input. The decoder, in turn, reconstructs the original data from this latent representation. Mathematically, let $x$ be the input data, the encoder function $f_{\theta}$ maps $x$ to a latent vector $z$, while the decoder function $g_{\phi}$ reconstructs $x$ from $z$, such that:

$$\hat{x} = g_{\phi}(f_{\theta}(x))$$

The model is trained to minimize the reconstruction loss, typically using a loss function like the mean squared error (MSE) between the original input $x$ and the reconstructed output $\hat{x}$:

$$L(x, \hat{x}) = \lVert x - \hat{x} \rVert^2$$

This objective ensures that the latent representation retains as much relevant information about the original data as possible while being compressed. The encoder-decoder architecture can introduce non-linearity through the use of activation functions such as ReLU or sigmoid, making autoencoders capable of capturing more complex relationships than purely linear methods.

```{mermaid}
flowchart LR
    A["Input Data, $$x$$"] --> |Encoder| C["Latent Representation, $$z$$"]
    C --> |"Decoder"|E["Reconstructed Data, $$\hat{x}$$"]
    A --> L["Loss, $$L(x, \hat{x})$$"]
    E --> L
```

Autoencoders have several variations, such as denoising autoencoders, which add noise to the input data during training to make the representation more robust, and variational autoencoders (VAEs), which impose a probabilistic structure on the latent space for generative purposes.

In the next section, we will see how Principal Component Analysis (PCA) can be understood as a simple form of autoencoder, where both the encoder and decoder are linear functions and the latent representation is defined by the principal components. This perspective helps bridge the gap between classical statistical methods and modern approaches to dimensionality reduction.

## PCA as an Autoencoder

Principal Component Analysis (PCA) can be interpreted as a specific type of autoencoder where the encoder and decoder functions are linear. In PCA, the encoder projects the input data onto a lower-dimensional subspace defined by the principal components, effectively compressing the data while retaining the directions of maximum variance. The decoder then reconstructs the data by projecting back from this subspace to the original space.

To understand why the maximization of the variance in the components is equivalent to minimizing the variance in the residuals, consider the nature of PCA. PCA seeks to find a set of orthogonal directions (principal components) along which the variance of the data is maximized. By capturing the maximum variance in the first few components, the reconstruction error (defined as the difference between the original data and its projection onto these components) is minimized. This is equivalent to saying that PCA minimizes the variance of the residuals, which is the part of the data that cannot be explained by the selected components.

Mathematically, PCA can be expressed using Singular Value Decomposition (SVD), which decomposes the data matrix $X$ into three matrices: $U$, $\Sigma$, and $V^T$, such that:

Here, $U$ and $V$ contain the left and right singular vectors, and $\Sigma$ is a diagonal matrix of singular values. The first $k$ columns of $V$ define the principal components, and by projecting $X$ onto these components, we obtain the low-dimensional representation. The reconstruction of $X$ from these $k$ components can be seen as minimizing the reconstruction error in terms of mean squared error (MSE), making SVD and PCA equivalent to minimizing the MSE in an autoencoder framework.

This perspective provides insight into how PCA is fundamentally related to linear autoencoders: both aim to represent data in a compressed form while preserving as much information as possible, with PCA focusing explicitly on maximizing variance and minimizing reconstruction error.

Autoencoders are a general framework used to learn efficient representations of data, often for dimensionality reduction or feature extraction. They operate by training a model to compress input data into a lower-dimensional representation and then reconstruct the original data from that compressed form. The primary goal of an autoencoder is not merely to copy the input, but rather to discover meaningful patterns and structures that capture the underlying features in a more compact representation.

An autoencoder consists of two main components: the encoder and the decoder. The encoder is responsible for compressing the input into a latent space representation, often called the bottleneck, which is typically of lower dimension than the input. The decoder, in turn, reconstructs the original data from this latent representation. Mathematically, let $x$ be the input data, the encoder function $f_{\theta}$ maps $x$ to a latent vector $z$, while the decoder function $g_{\phi}$ reconstructs $x$ from $z$, such that:

$$\hat{x} = g_{\phi}(f_{\theta}(x))$$

The model is trained to minimize the reconstruction loss, typically using a loss function like the mean squared error (MSE) between the original input $x$ and the reconstructed output $\hat{x}$:

$$L(x, \hat{x}) = \lVert x - \hat{x} \rVert^2$$

This objective ensures that the latent representation retains as much relevant information about the original data as possible while being compressed. The encoder-decoder architecture can introduce non-linearity through the use of activation functions such as ReLU or sigmoid, making autoencoders capable of capturing more complex relationships than purely linear methods.

```{mermaid}
graph TD
    A[Input Data (x)] --> B[Encoder]
    B --> C[Latent Representation (z)]
    C --> D[Decoder]
    D --> E[Reconstructed Data (\hat{x})]
```

Autoencoders have several variations, such as denoising autoencoders, which add noise to the input data during training to make the representation more robust, and variational autoencoders (VAEs), which impose a probabilistic structure on the latent space for generative purposes.

In the next section, we will see how Principal Component Analysis (PCA) can be understood as a simple form of autoencoder, where both the encoder and decoder are linear functions and the latent representation is defined by the principal components. This perspective helps bridge the gap between classical statistical methods and modern approaches to dimensionality reduction.

### PCA as an Autoencoder
Principal Component Analysis (PCA) can be interpreted as a specific type of autoencoder where the encoder and decoder functions are linear. In PCA, the encoder projects the input data onto a lower-dimensional subspace defined by the principal components, effectively compressing the data while retaining the directions of maximum variance. The decoder then reconstructs the data by projecting back from this subspace to the original space.

To understand why the maximization of the variance in the components is equivalent to minimizing the variance in the residuals, consider the nature of PCA. PCA seeks to find a set of orthogonal directions (principal components) along which the variance of the data is maximized. By capturing the maximum variance in the first few components, the reconstruction error (defined as the difference between the original data and its projection onto these components) is minimized. This is equivalent to saying that PCA minimizes the variance of the residuals, which is the part of the data that cannot be explained by the selected components.

Mathematically, PCA can be expressed using Singular Value Decomposition (SVD), which decomposes the data matrix $X$ into three matrices: $U$, $\Sigma$, and $V^T$, such that:

$$X = U \Sigma V^T$$

Here, $U$ and $V$ contain the left and right singular vectors, and $\Sigma$ is a diagonal matrix of singular values. The first $k$ columns of $V$ define the principal components, and by projecting $X$ onto these components, we obtain the low-dimensional representation. The reconstruction of $X$ from these $k$ components can be seen as minimizing the reconstruction error in terms of mean squared error (MSE), making SVD and PCA equivalent to minimizing the MSE in an autoencoder framework.

This perspective provides insight into how PCA is fundamentally related to linear autoencoders: both aim to represent data in a compressed form while preserving as much information as possible, with PCA focusing explicitly on maximizing variance and minimizing reconstruction error.

### Implementing Autoencoders with Multilayer Perceptrons (MLPs)

#### The PyTorch Package

PyTorch is a popular open-source deep learning framework developed by Facebook's AI Research lab. It provides a flexible and efficient platform for building and training neural networks, including autoencoders. PyTorch uses a dynamic computation graph, which makes it particularly user-friendly for experimenting with different model architectures, as changes can be made on-the-fly without needing to recompile the entire graph.

PyTorch's core components include `torch.Tensor` for handling multi-dimensional data, `nn.Module` for defining neural network layers and models, and the `torch.optim` package for optimizing models. These features make it straightforward to implement and train complex architectures, such as autoencoders, with relatively few lines of code.
Autoencoders can be implemented using Multilayer Perceptrons (MLPs), which are neural networks composed of multiple layers of interconnected nodes. In an MLP-based autoencoder, both the encoder and decoder are typically represented as feedforward neural networks with one or more hidden layers.

#### Implementation 

To implement an autoencoder with an MLP, we start by defining the architecture. The encoder consists of a series of fully connected layers that reduce the dimensionality of the input data until reaching the bottleneck layer, which represents the latent space. The decoder then consists of a series of layers that expand the latent representation back to the original input dimension.

A simple MLP-based autoencoder can be implemented in Python using popular deep learning libraries like TensorFlow or PyTorch. Below is an example implementation using PyTorch. As a test case, lets ćonsider synthetic data with a certain structure, 2D data from a "noisy" circle, that we scamble by projecting it into a 10 dimensional space. Could we train an encoder that in its latent representation capture the original structure of the data?

Steps Summary of the code:

1. **Generate 2D Circle Data with Noise**:
   - Use numpy to create 2D points on a noisy circle.
   - Visualize the generated data using matplotlib.

2. **Project Data into 10D Space**:
   - Apply a random linear transformation to the 2D data to create 10-dimensional representations.

3. **Define and Train the Autoencoder**:
   - The autoencoder consists of an encoder that compresses 10D data into a 2D latent space and a decoder that reconstructs it back to the original 10D.
   - Train the autoencoder using a Mean Squared Error loss to reconstruct the original high-dimensional data.

4. **Plot the Latent Space Embeddings**:
   - After training, visualize the latent representations to see how well the model compresses the data back into 2D.


```{code-cell}ipython3
import torch
import torch.nn as nn
import torch.optim as optim
import numpy as np
import matplotlib.pyplot as plt
from torch.utils.data import DataLoader, TensorDataset

# Step 1: Generate 2D points on a circle with noise
n_samples = 1000
noise_level = 0.1
np.random.seed(42)

theta = 2 * np.pi * np.random.rand(n_samples)
x = np.cos(theta) + noise_level * np.random.randn(n_samples)
y = np.sin(theta) + noise_level * np.random.randn(n_samples)

# Plot the original noisy circle data
plt.figure(figsize=(6, 6))
plt.scatter(x, y, alpha=0.5)
plt.title("Noisy 2D Circle Data")
plt.xlabel("x")
plt.ylabel("y")
plt.axis('equal')
plt.show()

# Step 2: Project the 2D data to a 10-dimensional space
points_2d = np.vstack((x, y)).T
projection_matrix = np.random.randn(2, 10)
high_dim_points = points_2d @ projection_matrix

# Convert to PyTorch tensors
high_dim_points = torch.tensor(high_dim_points, dtype=torch.float32)
dataset = TensorDataset(high_dim_points)
dataloader = DataLoader(dataset, batch_size=32, shuffle=True)

# Step 3: Define the Autoencoder with a 2D latent space
class Autoencoder(nn.Module):
    def __init__(self, input_dim, hidden_dim, latent_dim):
        super(Autoencoder, self).__init__()
        # Encoder network
        self.encoder = nn.Sequential(
            nn.Linear(input_dim, hidden_dim),
            nn.ReLU(),
            nn.Linear(hidden_dim, latent_dim)
        )
        # Decoder network
        self.decoder = nn.Sequential(
            nn.Linear(latent_dim, hidden_dim),
            nn.ReLU(),
            nn.Linear(hidden_dim, input_dim)
        )
    
    def forward(self, x):
        z = self.encoder(x)
        reconstructed = self.decoder(z)
        return z, reconstructed

# Set up model, loss function, and optimizer
input_dim = 10
hidden_dim = 6
latent_dim = 2
autoencoder = Autoencoder(input_dim, hidden_dim, latent_dim)

criterion = nn.MSELoss()
optimizer = optim.Adam(autoencoder.parameters(), lr=1e-3)

# Step 4: Train the autoencoder
num_epochs = 50
for epoch in range(num_epochs):
    for data in dataloader:
        inputs, = data
        
        # Forward pass
        latent, outputs = autoencoder(inputs)
        loss = criterion(outputs, inputs)
        
        # Backward pass
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
    
    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')

# Step 5: Plot the latent space embeddings
all_inputs = high_dim_points
with torch.no_grad():
    latent_embeddings, _ = autoencoder(all_inputs)

latent_embeddings = latent_embeddings.numpy()

plt.figure(figsize=(6, 6))
plt.scatter(latent_embeddings[:, 0], latent_embeddings[:, 1], alpha=0.5)
plt.title("Latent Space Embeddings")
plt.xlabel("Latent Dimension 1")
plt.ylabel("Latent Dimension 2")
plt.axis('equal')
plt.show()
```

In this implementation, the `Autoencoder` class defines both the encoder and decoder as sequential networks. The encoder compresses the input to a latent dimension, while the decoder reconstructs the input from the latent representation. The network is trained by minimizing the mean squared error (MSE) between the input and the reconstructed output.

The activation functions used in the encoder and decoder introduce non-linearity, enabling the autoencoder to learn more complex mappings than PCA. The `ReLU` activation is commonly used in the hidden layers, while the output layer uses a `Sigmoid` activation to ensure the reconstructed values are in a specific range (e.g., [0, 1] for normalized data).

MLP-based autoencoders are a powerful tool for learning non-linear representations of data, which makes them well-suited for tasks involving complex, high-dimensional datasets. By stacking multiple hidden layers, the autoencoder can capture increasingly abstract features, enabling effective dimensionality reduction and feature extraction.