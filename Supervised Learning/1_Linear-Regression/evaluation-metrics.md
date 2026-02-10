
---

# 0. Evaluation Metrics — How Good Is the Model?

After training a regression model, we ask one simple question:

> **How close are my predictions to the actual values?**

Let’s use a **single concrete example** for *all* metrics.

---

## Example Dataset (Very Important)

Assume we have 5 data points:

| x | Actual y | Predicted ŷ |
| - | -------- | ----------- |
| 1 | 2        | 2.5         |
| 2 | 4        | 3.5         |
| 3 | 5        | 4.8         |
| 4 | 4        | 4.2         |
| 5 | 5        | 5.1         |

---

## Step 1: Compute Errors (Residuals)

Residual = Actual − Predicted

| y | ŷ   | Error (y − ŷ) |
| - | --- | ------------- |
| 2 | 2.5 | −0.5          |
| 4 | 3.5 | 0.5           |
| 5 | 4.8 | 0.2           |
| 4 | 4.2 | −0.2          |
| 5 | 5.1 | −0.1          |

Residuals show **how far off** the model is for each point.

---

# 1. Mean Absolute Error (MAE)

### Formula

[
\text{MAE} = \frac{1}{n}\sum |y - \hat{y}|
]

### Step-by-Step Calculation

Take **absolute values** of errors:

| Error | Absolute Error |
| ----- | -------------- |
| −0.5  | 0.5            |
| 0.5   | 0.5            |
| 0.2   | 0.2            |
| −0.2  | 0.2            |
| −0.1  | 0.1            |

Sum:

[
0.5 + 0.5 + 0.2 + 0.2 + 0.1 = 1.5
]

Divide by n = 5:

[
\text{MAE} = \frac{1.5}{5} = \boxed{0.3}
]

### Interpretation

👉 **On average, predictions are off by 0.3 units**

### Why MAE Is Easy to Understand

* Same unit as y
* Direct meaning
* No squaring → no exaggeration

### Limitation

❌ Treats small and large errors almost equally

```
Error 10 vs Error 1
MAE impact: 10x vs 1x
```

---

# 2. Mean Squared Error (MSE)

### Formula

[
\text{MSE} = \frac{1}{n}\sum (y - \hat{y})^2
]

### Step-by-Step Calculation

Square each error:

| Error | Squared Error |
| ----- | ------------- |
| −0.5  | 0.25          |
| 0.5   | 0.25          |
| 0.2   | 0.04          |
| −0.2  | 0.04          |
| −0.1  | 0.01          |

Sum:

[
0.25 + 0.25 + 0.04 + 0.04 + 0.01 = 0.59
]

Divide by n = 5:

[
\text{MSE} = \frac{0.59}{5} = \boxed{0.118}
]

### Why Squaring Matters

```
Error = 5 → squared = 25
Error = 1 → squared = 1
```

Large mistakes hurt **much more**.

### Pros & Cons

✔ Penalizes large errors
❌ Unit becomes y² (hard to interpret)

---

# 3. Root Mean Squared Error (RMSE)

### Formula

[
\text{RMSE} = \sqrt{\text{MSE}}
]

### Calculation

[
\text{RMSE} = \sqrt{0.118} ≈ \boxed{0.34}
]

### Why RMSE Is Popular

* Same unit as y
* Penalizes large errors
* Smooth optimization behavior

### Interpretation

👉 **Typical prediction error ≈ 0.34 units**

---

# Comparison Summary (MAE vs MSE vs RMSE)

| Metric | Penalizes big errors? | Easy to interpret? |
| ------ | --------------------- | ------------------ |
| MAE    | ❌ No                  | ✔ Yes              |
| MSE    | ✔ Yes                 | ❌ No               |
| RMSE   | ✔ Yes                 | ✔ Yes              |

---

# 11. R-Squared (Coefficient of Determination)

R² answers a **different question**:

> **How much of the variation in y is explained by the model?**

---

## Step 1: Compute Mean of y

Actual y values:

[
y = [2, 4, 5, 4, 5]
]

Mean:

[
\bar{y} = \frac{2+4+5+4+5}{5} = 4
]

---

## Step 2: Compute SST (Total Variance)

[
\text{SST} = \sum (y - \bar{y})^2
]

| y | y − mean | Square |
| - | -------- | ------ |
| 2 | −2       | 4      |
| 4 | 0        | 0      |
| 5 | 1        | 1      |
| 4 | 0        | 0      |
| 5 | 1        | 1      |

[
\text{SST} = 6
]

---

## Step 3: Compute SSR (Residual Variance)

[
\text{SSR} = \sum (y - \hat{y})^2
]

We already computed this:

[
\text{SSR} = 0.59
]

---

## Step 4: Compute R²

[
R^2 = 1 - \frac{SSR}{SST}
]

[
R^2 = 1 - \frac{0.59}{6} = 1 - 0.098 ≈ \boxed{0.90}
]

---

## Interpretation of R² = 0.90

👉 **90% of the variance in y is explained by the model**

---

## Visual Meaning

```
Total spread (SST)
|--------------------------|

Unexplained error (SSR)
|----|

Explained by model
|------------------|
```

---

## R² Value Meaning

| R²  | Meaning             |
| --- | ------------------- |
| 1.0 | Perfect fit         |
| 0.9 | Excellent           |
| 0.5 | Moderate            |
| 0.0 | Same as mean        |
| < 0 | Worse than guessing |

---

# 12. Adjusted R-Squared

### Why It Exists

Adding more features **always increases R²**, even useless ones.

Adjusted R² fixes this.

---

### Formula

[
\text{Adjusted } R^2 = 1 - \frac{(1 - R^2)(n - 1)}{n - p - 1}
]

Where:

* n = number of samples
* p = number of predictors

---

### Example

Assume:

* R² = 0.90
* n = 5
* p = 2

[
\text{Adjusted } R^2 =
1 - \frac{(1 - 0.9)(5 - 1)}{5 - 2 - 1}
]

[
= 1 - \frac{0.1 × 4}{2}
= 1 - 0.2
= \boxed{0.80}
]

---

## Key Insight

* If new feature **helps** → Adjusted R² ↑
* If useless → Adjusted R² ↓

---

# Final Mental Model

| Metric      | Answers                           |
| ----------- | --------------------------------- |
| MAE         | “Average error magnitude?”        |
| RMSE        | “How bad are typical mistakes?”   |
| R²          | “How much variance do I explain?” |
| Adjusted R² | “Did extra features really help?” |

---


