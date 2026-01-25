# Mathematical Foundations for Machine Learning (ML)

These notes rewrite and expand the lecture content with **clear explanations, physical intuition, and worked examples**. We begin from **fundamental physics concepts (scalars and vectors)** and smoothly transition into **machine learning mathematics**.

---

## 0. SCALARS, VECTORS, AND TENSORS (PHYSICAL & MATHEMATICAL FOUNDATION)

Before studying vectors in Machine Learning, it is important to understand how **physical quantities are classified**. This classification builds the intuition for later mathematical abstractions.

Physical quantities are broadly classified into:

* **Scalar quantities**
* **Vector quantities**
* **Tensor quantities**

This distinction is fundamental for describing motion, forces, and real-world systems — and later for understanding ML data representations.

---

### 0.1 Scalar Quantities

A **scalar quantity** is a physical quantity that has **only magnitude and no direction**.

#### Key Characteristics

* Represented by a **single numerical value** with units
* Direction is **not relevant**
* Follow **ordinary arithmetic rules** (addition, subtraction, multiplication, division)
* Easier to handle compared to vectors

#### Examples of Scalar Quantities

* Temperature
* Mass
* Time
* Distance
* Speed
* Energy
* Area
* Volume
* Density
* Electric charge

#### Measuring Instruments

* Thermometer → Temperature
* Balance / Scale → Mass
* Stopwatch → Time
* Ruler → Distance
* Speedometer → Speed
* Wattmeter → Power / Energy

#### Worked Example

If a car travels **100 km in 2 hours**, its **average speed** is:

```
Speed = Distance / Time = 100 / 2 = 50 km/h
```

Speed here is a **scalar** because direction is ignored.

---

### 0.2 Vector Quantities

A **vector quantity** is a physical quantity that has **both magnitude and direction**.

#### Key Characteristics

* Represented by a **numerical value + direction**
* Often drawn as an **arrow**
* Direction plays a crucial role
* Require special mathematical rules for operations

#### Examples of Vector Quantities

* Displacement
* Velocity
* Acceleration
* Force
* Momentum
* Weight
* Electric field
* Magnetic field
* Thrust
* Drag force
* Lift force
* Angular velocity
* Linear momentum

#### Worked Example

If a car is moving at **50 km/h towards the east**, its velocity is represented as:

* Magnitude → 50 km/h
* Direction → East

This cannot be represented by a single number alone.

---

### 0.3 Vector Notation

Vectors are commonly represented using:

* An **arrow above the symbol**:
  ( ec{v} )

* Bold letters (in textbooks):
  **v**

* Component form:

```
ec{v} = (vx, vy)
```

---

### 0.4 Equality of Vectors

Two vectors are **equal** if:

* Their **magnitudes are equal**
* Their **directions are the same**

Position does **not** matter.

📌 Vectors with the same length but different directions are **not equal**.

---

### 0.5 Multiplication of a Vector by a Scalar

When a vector ( ec{v} ) is multiplied by a scalar **k**:

* Direction remains the same (or reverses if k < 0)
* Magnitude changes

Mathematically:

```
|kec{v}| = k|ec{v}|
```

* If k > 1 → magnitude increases
* If 0 < k < 1 → magnitude decreases
* If k < 0 → direction reverses

---

### 0.6 Addition of Vectors

Vectors **cannot** be added like scalars.

Direction **must** be considered.

#### Triangle Law of Vector Addition

If two vectors ( ec{p} ) and ( ec{q} ) are placed head-to-tail, the **resultant vector** is:

```
ec{R} = ec{p} + ec{q}
```

Magnitude of resultant:

```
|R| = √(p² + q² + 2pq cosθ)
```

Where θ is the angle between vectors.

Direction of resultant:

```
tan(φ) = (q sinθ) / (p + q cosθ)
```

---

### 0.7 Parallelogram Law of Vector Addition

If two vectors acting at a point are represented by the **adjacent sides of a parallelogram**, the **diagonal** represents the resultant vector.

This law is equivalent to the triangle law.

---

### 0.8 Tensor Quantities

A **tensor quantity** requires:

* Magnitude
* Direction
* **More than one independent direction** for complete description

Tensors obey **specific transformation rules** under coordinate changes.

---

### 0.9 Momentum Flux (Tensor Example)

**Momentum flux** describes the **rate at which momentum crosses a surface**.

To fully specify momentum flux, we need:

1. Direction of momentum being transported
2. Direction of the surface normal

Because of this dual directional dependence:

* Momentum flux is **not a scalar**
* Not a vector
* It is a **tensor quantity**

#### Physical Interpretation

Imagine water particles flowing through a surface:

* Each particle carries momentum
* Momentum flux measures **how much momentum crosses the surface per second**

📌 This idea is fundamental in:

* Fluid dynamics
* Stress tensors
* Continuum mechanics

---

## 1. VECTORS

### 1.1 What is a Vector?

A **vector** is one of the most fundamental objects in Machine Learning.

There are three common perspectives:

* **Physics**: A quantity with *magnitude and direction* (e.g., velocity)
* **Mathematics**: An *ordered list of numbers*
* **Machine Learning / Data Science**: A *representation of features* of a data point

In ML, **every data point is represented as a vector**.

---

### 1.2 Vector Representation

A vector with two features:

```
(2, 3)
```

Example interpretation:

* Feature 1 → Study hours = 2
* Feature 2 → Sleep hours = 3

This single vector represents **one student**.

If we have 3 features:

```
(2, 3, 85)
```

* Study hours
* Sleep hours
* Exam score

📌 In ML, **number of features = dimension of the vector**.

---

### 1.3 Row and Column Vectors

* **Row vector**:

```
[ x1  x2  x3 ]
```

* **Column vector**:

```
| x1 |
| x2 |
| x3 |
```

In mathematics and ML theory, **column vectors are preferred**, especially in matrix multiplication.

---

### 1.4 Vector Operations

#### Vector Addition

Add corresponding elements:

```
(2, 3) + (1, 4) = (3, 7)
```

**Meaning**: Combining features or effects.

---

#### Scalar Multiplication

Multiply every element by a scalar:

```
2 × (2, 3) = (4, 6)
```

* Direction remains the same
* Magnitude changes

📌 In ML, scaling data = scalar multiplication.

---

### 1.5 Vector Magnitude (Length)

For vector:

```
A = (x, y)
```

Magnitude:

```
|A| = √(x² + y²)
```

Example:

```
A = (3, 4)
|A| = √(9 + 16) = 5
```

---

## 2. MATRICES

### 2.1 What is a Matrix?

A **matrix** is a collection of vectors arranged in **rows and columns**.

Example:

```
A = | 1  2 |
    | 3  4 |
```

This is a **2 × 2 matrix**.

---

### 2.2 Why Matrices Matter in ML

* Dataset = Matrix
* Neural network weights = Matrices
* Image = Matrix of pixels
* Word embeddings = Matrices

📌 ML is essentially **matrix computation at scale**.

---

### 2.3 Matrix Dimensions

Written as:

```
rows × columns
```

Example:

```
3 × 2 matrix → 3 rows, 2 columns
```

---

### 2.4 Matrix Multiplication

#### Rule

Matrix multiplication is possible **only if**:

```
(columns of A) = (rows of B)
```

#### Example

Matrix A (2 × 3):

```
| 1  2  3 |
| 4  5  6 |
```

Matrix B (3 × 2):

```
| 1  2 |
| 3  4 |
| 5  6 |
```

Result → (2 × 2):

```
| (1×1+2×3+3×5)   (1×2+2×4+3×6) |
| (4×1+5×3+6×5)   (4×2+5×4+6×6) |
```

---

📌 Neural networks perform **repeated matrix multiplications**.

---

## 3. DOT PRODUCT

### 3.1 Definition

The **dot product** of two vectors measures **how similar or aligned they are**.

Formula:

```
A · B = x1y1 + x2y2 + ... + xnyn
```

---

### 3.2 Worked Example

```
A = (1, 2)
B = (3, 4)

A · B = (1×3) + (2×4) = 11
```

---

### 3.3 Geometric Meaning

```
A · B = |A||B|cos(θ)
```

* Positive → similar direction
* Zero → orthogonal (90°)
* Negative → opposite direction

---

### 3.4 Cosine Similarity

```
cos(θ) = (A · B) / (|A||B|)
```

Range:

* +1 → identical
* 0 → unrelated
* -1 → opposite

📌 Used in:

* Recommendation systems
* Semantic search
* Vector databases

---

## 4. EIGENVALUES & EIGENVECTORS

### 4.1 Core Idea

For a matrix **A**:

```
A × v = λv
```

* v → Eigenvector (direction unchanged)
* λ → Eigenvalue (scaling factor)

---

### 4.2 Intuition

Think of stretching a spring:

* Length changes
* Direction remains the same

---

### 4.3 PCA (Principal Component Analysis)

PCA uses eigenvectors to:

* Find important directions
* Reduce dimensions
* Preserve maximum information

📌 PCA keeps **meaning**, not raw features.

---

## 5. DIFFERENTIAL CALCULUS

### 5.1 What is Differentiation?

Differentiation measures **how fast something changes**.

Example:

```
y = 2x

dy/dx = 2
```

Meaning:

* If x increases by 1 → y increases by 2

---

### 5.2 Slope Interpretation

* Derivative = slope of tangent
* Constant slope → straight line

📌 ML uses derivatives to minimize loss.

---

## 6. GRADIENT

### 6.1 Multivariable Functions

```
z = x² + y²
```

Partial derivatives:

```
∂z/∂x = 2x
∂z/∂y = 2y
```

Gradient:

```
∇z = (2x, 2y)
```

---

### 6.2 Gradient Descent

* Gradient points to **maximum increase**
* ML moves in **opposite direction**

📌 This is how models learn.

---

## 7. CHAIN RULE

### 7.1 Definition

If:

```
y = f(g(x))
```

Then:

```
dy/dx = (dy/dg) × (dg/dx)
```

---

### 7.2 ML Importance

* Backpropagation = chain rule applied repeatedly
* Enables deep neural networks

---

## 8. BIG PICTURE

Machine Learning =

* Vectors → Data
* Matrices → Transformations
* Dot Product → Similarity
* Eigenvectors → Meaningful directions
* Derivatives → Learning
* Chain Rule → Backpropagation

---

### ✅ You are now mathematically ready for:

* Linear Regression
* Loss Functions
* Optimization Algorithms
* Neural Networks
