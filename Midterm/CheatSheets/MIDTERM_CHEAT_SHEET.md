# 📝 STA4724 MIDTERM CHEAT SHEET (3x5 Double-Sided)

## 🎯 STRATEGIC LAYOUT FOR MAXIMUM IMPACT

### **SIDE 1: FORMULAS & CORE CONCEPTS**

---

## 📊 **LINEAR REGRESSION**
**Formula**: y = β₀ + β₁x + ε
**Matrix Form**: y = Xβ + ε
**OLS Solution**: β̂ = (X^T X)^(-1) X^T y

**R² Score**: R² = 1 - (SS_res/SS_tot)
- Higher R² = Better fit (0 to 1)
- R² = % variance explained

**Multivariate**: y = β₀ + β₁x₁ + β₂x₂ + ... + βₚxₚ + ε

---

## 🎯 **CLASSIFICATION (kNN)**
**Algorithm**: Find k nearest neighbors, majority vote
**Distance**: Usually Euclidean: d = √Σ(xᵢ-yᵢ)²
**Accuracy**: Correct Predictions / Total Predictions

**Confusion Matrix**:
```
        Predicted
        0    1
True 0 [TN] [FP]
     1 [FN] [TP]
```
Accuracy = (TP + TN) / (TP + TN + FP + FN)

---

## 🔄 **CROSS-VALIDATION**
**k-fold CV**: Split data into k parts, train on k-1, test on 1
**Leave-One-Out**: k = n (each sample is test set once)
**Purpose**: Better estimate of model performance

---

## 🎯 **REGULARIZATION**
**Lasso**: Adds L1 penalty (|β|), promotes sparsity
**Ridge**: Adds L2 penalty (β²), shrinks coefficients
**Parameter**: λ (lambda) or α (alpha) controls strength

---

### **SIDE 2: CODE PATTERNS & QUICK REFERENCE**

---

## 💻 **ESSENTIAL CODE PATTERNS**

### **Data Loading & Prep**
```python
import pandas as pd, numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, confusion_matrix

df = pd.read_csv('file.csv')
X = df[['feature1', 'feature2']].values
y = df['target'].values
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)
```

### **Linear Regression**
```python
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
r2 = model.score(X_test, y_test)
print(f"Intercept: {model.intercept_}")
print(f"Coefficients: {model.coef_}")
```

### **Manual OLS**
```python
X_with_intercept = np.column_stack([np.ones(len(X)), X])
beta = np.linalg.inv(X_with_intercept.T @ X_with_intercept) @ X_with_intercept.T @ y
```

### **kNN Classification**
```python
knn = KNeighborsClassifier(n_neighbors=k)
knn.fit(X_train, y_train)
y_pred = knn.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
cm = confusion_matrix(y_test, y_pred)
```

### **Cross-Validation**
```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(model, X, y, cv=5)
print(f"CV Score: {scores.mean():.3f} ± {scores.std():.3f}")
```

### **Lasso Regression**
```python
from sklearn.linear_model import Lasso
lasso = Lasso(alpha=0.01)
lasso.fit(X_train, y_train)
```

---

## 🧠 **PYTHON ESSENTIALS**

### **Identity vs Equality**
- `==` compares VALUES
- `is` compares OBJECTS (memory location)
- `x = [1,2]; y = [1,2]; z = x`
- `x == y` → True, `x is y` → False, `x is z` → True

### **List Operations**
```python
result = []
for i in range(len(data)):
    if data[i] > i:
        result.append(1)
    elif data[i] < i:
        result.append(-1)
    else:
        result.append(0)
```

---

## 📈 **PLOTTING ESSENTIALS**
```python
import matplotlib.pyplot as plt
plt.scatter(x, y, alpha=0.7)
plt.plot(x, y_pred, 'r-', linewidth=2)
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Title')
plt.legend()
plt.show()
```

---

## ⚠️ **EXAM TRAPS TO AVOID**

1. **Train/Test Split**: NEVER test on training data!
2. **Shape Issues**: Check X.shape, y.shape before fitting
3. **Scaling**: Some algorithms need feature scaling
4. **k in kNN**: Try odd numbers, use CV to select
5. **Overfitting**: High training accuracy, low test accuracy
6. **Underfitting**: Low accuracy on both train and test

---

## 🎯 **QUICK DECISION TREE**

**Continuous Target** → Linear Regression
**Categorical Target** → Classification (kNN)
**Many Features** → Consider Lasso/Ridge
**Small Dataset** → Use Cross-Validation
**Poor Performance** → Check for over/underfitting

---

## 📊 **COMMON TRANSFORMATIONS**
- **Log Transform**: `np.log(x)` for skewed data
- **Standardization**: `(x - mean) / std`
- **Min-Max Scaling**: `(x - min) / (max - min)`

---

## 🔢 **QUICK MATH REMINDERS**
- **Matrix Multiplication**: (m×n) @ (n×p) = (m×p)
- **Transpose**: X.T or X^T
- **Inverse**: np.linalg.inv(X)
- **Norm**: np.linalg.norm(x) = √(x₁² + x₂² + ...)

---

## 🎓 **FINAL TIPS**
- Read questions CAREFULLY
- Show your work for partial credit
- Check units and interpretations
- Verify shapes match before operations
- Use descriptive variable names
- Comment your code clearly

**YOU'VE GOT THIS!** 🚀
