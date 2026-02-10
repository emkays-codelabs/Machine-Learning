
---

# 📈 Linear Regression From Scratch (Pure Python, Fully Explained)

This project explains **Simple Linear Regression** from absolute basics and implements it **from scratch using pure Python** (no NumPy, no ML libraries).

The purpose is **learning, not shortcuts**:

* What Linear Regression really is
* Why the formulas exist
* How numbers change during training
* What the graphs actually mean
* Why the final equation looks the way it does

---

## 1️⃣ What Is Linear Regression?

Linear Regression tries to **fit a straight line** through data so that the line represents the **best possible relationship** between input and output.

We assume this form:

```
y_hat = m * x + c
```

Where:

* `x` → input value
* `y` → actual output
* `y_hat` → predicted output
* `m` → slope (how steep the line is)
* `c` → intercept (where the line crosses y-axis)

---

## 2️⃣ Intuition Behind `m` and `c`

### Slope (`m`)

* Controls **tilt of the line**
* Higher `m` → steeper line
* Lower `m` → flatter line

### Intercept (`c`)

* Shifts the line **up or down**
* Represents predicted value when `x = 0`

Together, `m` and `c` fully define the line.

---

## 3️⃣ Dataset Used

We intentionally use **small data** so behavior is visible:

```
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 5]
```

This roughly follows an upward trend but includes noise.

---

## 4️⃣ How Do We Measure Error?

We need a way to measure **how wrong the line is**.

### Mean Squared Error (MSE)

```
MSE = (1 / n) * Σ (y - y_hat)^2
```

Explanation:

* For each point, subtract prediction from actual value
* Square it (no negative values, larger errors punished more)
* Average across all points

Lower MSE = better line.

---

## 5️⃣ Why Gradient Descent?

We do **not know** the best `m` and `c` beforehand.

So we:

1. Start with `m = 0`, `c = 0`
2. Measure error
3. Adjust `m` and `c` slightly
4. Repeat until error reduces

This process is **Gradient Descent**.

---

## 6️⃣ How Do We Update `m` and `c`?

We calculate how much `m` and `c` contribute to error.

### Gradient for `m`

```
dm = (-2 / n) * Σ x * (y - y_hat)
```

### Gradient for `c`

```
dc = (-2 / n) * Σ (y - y_hat)
```

### Update Rule

```
m = m - learning_rate * dm
c = c - learning_rate * dc
```

`learning_rate` controls **how fast we learn**.

---

## 7️⃣ Complete Pure Python Implementation

Save as **`linear_regression_demo.py`**

```python
import matplotlib.pyplot as plt

# -----------------------------
# Dataset
# -----------------------------
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 5]
n = len(x)

# -----------------------------
# Parameters
# -----------------------------
m = 0.0
c = 0.0
learning_rate = 0.01
epochs = 50

loss_history = []

# -----------------------------
# Training
# -----------------------------
for epoch in range(epochs):

    # Predictions
    y_hat = [m * x[i] + c for i in range(n)]

    # Mean Squared Error
    mse = sum((y[i] - y_hat[i]) ** 2 for i in range(n)) / n
    loss_history.append(mse)

    # Gradients
    dm = (-2 / n) * sum(x[i] * (y[i] - y_hat[i]) for i in range(n))
    dc = (-2 / n) * sum((y[i] - y_hat[i]) for i in range(n))

    # Update parameters
    m -= learning_rate * dm
    c -= learning_rate * dc

    # -----------------------------
    # Visualization per epoch
    # -----------------------------
    plt.clf()
    plt.scatter(x, y, color="blue", label="Actual Data")
    plt.plot(x, y_hat, color="red", label="Regression Line")

    equation = f"y = {m:.2f}x + {c:.2f}"
    plt.text(1, max(y) - 0.5, equation)

    plt.title(f"Epoch {epoch+1} | MSE = {mse:.4f}")
    plt.xlabel("x")
    plt.ylabel("y")
    plt.legend()
    plt.pause(0.1)

plt.show()

# -----------------------------
# Loss Curve
# -----------------------------
plt.figure()
plt.plot(range(1, epochs + 1), loss_history)
plt.xlabel("Epoch")
plt.ylabel("MSE")
plt.title("Loss Curve (Error vs Epoch)")
plt.show()
```

---

## 8️⃣ What Do the Graphs Mean?

### 📊 Graph 1: Line Fitting Over Epochs

* **Blue dots** → actual data
* **Red line** → current learned model
* Early epochs: line is wrong
* Later epochs: line aligns better with data

### ✍ Equation on Graph

```
y = m x + c
```

Updates every epoch to show learning progress.

---

### 📉 Graph 2: Loss Curve

X-axis:

```
Epoch number
```

Y-axis:

```
Mean Squared Error
```

What we expect:

* Error starts high
* Error decreases gradually
* Curve slopes downward

This confirms **learning is successful**.

---

## 9️⃣ Why Do These Final Values Appear?

Example final result:

```
m ≈ 0.60
c ≈ 2.20
```

Meaning:

* Each unit increase in `x` increases `y` by ~0.6
* Base value starts around 2.2

These values best minimize overall squared error for the dataset.

---

## 🔍 Why Not Perfect?

Because:

* Data is noisy
* Linear model cannot fit all points exactly
* Regression finds **best compromise line**

---
