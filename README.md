
---

# RandriaLogisticReg - Logistic Regression Implementation

This repository implements a basic Logistic Regression classifier from scratch using Python and Numpy. The logistic regression model is trained using the dataset generated by the `make_blobs` function, which is visualized using `matplotlib`.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
- [Contributing](#contributing)
- [License](#license)

## Installation

1. **Clone the repository:**
   ```
   git clone <repository-url>
   cd <repository-folder>
   ```

2. **Install the required dependencies:**
   ```bash
   pip install numpy matplotlib scikit-learn
   ```

## Usage

You can run the Logistic Regression model by executing the following script:

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs

# Generate synthetic data
X, y = make_blobs(n_samples=100, n_features=2, centers=2, random_state=0)
y = y.reshape((y.shape[0], 1))

# Plot the generated data
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='bwr')

# Logistic Regression Class
class RandriaLogisticReg:
    def initialisation(X):
        W = np.random.randn(X.shape[1], 1)
        b = np.random.randn(1)
        return (W, b)

    def sigmoid(Z):
        return 1 / (1 + np.exp(-Z))

    def forward_prop(X, W, b):
        Z = X.dot(W) + b
        return RandriaLogisticReg.sigmoid(Z)

    def log_loss(A, y):
        return 1 / len(y) * np.sum(-y * np.log(A) - (1 - y) * np.log(1 - A))

    def gradients(X, A, y):
        dW = 1 / len(y) * np.dot(X.T, A - y)
        db = 1 / len(y) * np.sum(A - y)
        return (dW, db)

    def optimisation(X, W, b, A, y, learning_rate):
        dW, db = RandriaLogisticReg.gradients(X, A, y)
        W = W - learning_rate * dW
        b = b - learning_rate * db
        return (W, b)

    def predict(X, W, b):
        A = RandriaLogisticReg.forward_prop(X, W, b)
        return A >= 0.5

    def regression_logistique(X, y, learning_rate=0.1, n_iter=100):
        # Initialisation
        W, b = RandriaLogisticReg.initialisation(X)

        # Training loop
        for i in range(n_iter):
            A = RandriaLogisticReg.forward_prop(X, W, b)
            W, b = RandriaLogisticReg.optimisation(X, W, b, A, y, learning_rate)

        return (W, b)

# Training the logistic regression model
RandriaLogisticReg.regression_logistique(X, y, learning_rate=0.1, n_iter=100)
```

### Visualizing the Data

After running the code, you should see a scatter plot of the synthetic dataset generated using `make_blobs`. The points will be colored according to their class (2 centers).

### Model Training

The `RandriaLogisticReg` class defines several methods to implement logistic regression:

1. **initialisation(X):** Initializes the weights (`W`) and bias (`b`) of the model.
2. **sigmoid(Z):** Applies the sigmoid activation function.
3. **forward_prop(X, W, b):** Performs the forward propagation step, calculating the predictions.
4. **log_loss(A, y):** Computes the logistic loss (cross-entropy loss).
5. **gradients(X, A, y):** Computes the gradients of the loss with respect to `W` and `b`.
6. **optimisation(X, W, b, A, y, learning_rate):** Updates the weights and bias using gradient descent.
7. **predict(X, W, b):** Predicts the class for each data point (0 or 1) based on the learned weights and bias.
8. **regression_logistique(X, y, learning_rate, n_iter):** The main method to train the logistic regression model. It calls the initialization, forward propagation, loss calculation, and gradient descent optimization steps for the specified number of iterations.

## Code Explanation

1. **Data Generation:**
   - The data is generated using the `make_blobs` function from `scikit-learn`. This creates 100 samples with 2 features (2D data) and 2 centers (binary classification problem).
   - The target labels `y` are reshaped to have a single column.

2. **Logistic Regression Model:**
   - The logistic regression model is implemented in the `RandriaLogisticReg` class. The model is trained using gradient descent to minimize the logistic loss function (`log_loss`).

3. **Training and Evaluation:**
   - The model is trained for 100 iterations (`n_iter=100`) using a learning rate of 0.1 (`learning_rate=0.1`).

4. **Prediction:**
   - After training, the `RandriaLogisticReg.predict()` method can be used to classify new data points based on the learned weights.

5. **Visualization:**
   - A scatter plot is created using `matplotlib` to visualize the dataset, with the points colored according to their class.

## Contributing

Feel free to fork this repository, make improvements, and create a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Notes on Issues:

- There is a typo in your code that causes an error in the method name. The `forward_prop` method is incorrectly referred to as `foward_prop` in the `regression_logistique` method.
  - **Fix:**
    ```python
    A = RandriaLogisticReg.forward_prop(X, W, b)
    ```

