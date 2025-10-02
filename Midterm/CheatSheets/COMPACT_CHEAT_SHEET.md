# 📝 COMPACT 3x5 CHEAT SHEET

## **SIDE 1: FORMULAS & MATH**

### **LINEAR REGRESSION**
y = β₀ + β₁x + ε  |  y = Xβ + ε  |  β̂ = (X^T X)^(-1) X^T y
R² = 1 - SS_res/SS_tot  (higher = better, 0-1)

### **kNN CLASSIFICATION** 
Find k neighbors → majority vote  |  Acc = Correct/Total
Confusion Matrix: Rows=True, Cols=Predicted, Diag=Correct

### **CROSS-VALIDATION**
k-fold: split→train→test→repeat  |  Better than single split

### **PYTHON FUNDAMENTALS (Lecture 1)**
**Variable Types**: int, float, str  |  type(x) to check
**String Ops**: 3*"abc"="abcabcabc"  |  "a"+"b"="ab"  |  'McDonald\'s'
**Lists**: [1,2,3] mutable  |  .append() .insert() .remove() .pop()
**Slicing**: s[0] s[-1] s[1:3] s[:3] s[3:]  |  s[start:end] excludes end
**Identity vs Equality**: == (values) vs is (objects)  |  x=[1,2]; y=[1,2]; x==y✓ x is y✗

---

## **SIDE 2: CODE PATTERNS**

### **UNIVERSAL ML PATTERN**
```python
import pandas as pd, numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, confusion_matrix

# Load & Split
df = pd.read_csv('file.csv')
X, y = df[['feat']].values, df['target'].values
X_tr, X_te, y_tr, y_te = train_test_split(X,y,test_size=0.3)

# Fit & Predict
model = LinearRegression()  # or KNeighborsClassifier(k)
model.fit(X_tr, y_tr)
y_pred = model.predict(X_te)

# Evaluate
r2 = model.score(X_te, y_te)  # regression
acc = accuracy_score(y_te, y_pred)  # classification
cm = confusion_matrix(y_te, y_pred)
```

### **MANUAL OLS**
```python
X_int = np.column_stack([np.ones(len(X)), X])
β = np.linalg.inv(X_int.T @ X_int) @ X_int.T @ y
```

### **CROSS-VALIDATION**
```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(model, X, y, cv=5)
```

### **PLOTTING**
```python
plt.scatter(x,y); plt.plot(x,pred,'r-')
plt.xlabel('X'); plt.ylabel('Y'); plt.show()
```

### **LASSO**
```python
from sklearn.linear_model import Lasso
lasso = Lasso(alpha=0.01); lasso.fit(X,y)
```

**EXAM TIPS**: Check shapes | Never test on train | Use CV for k | Odd k values
