# Forest-fire-prevention-prediction

This repository documents the full workflow I followed to complete the Forest Fire Prevention Prediction assignment.  
All steps are recorded here as evidence of my process, including data preparation, modelling, evaluation, and validation performed using Orange Data Mining.

---

## 1. Loading the Dataset
- Imported **forestfires_classification.csv** into Orange using the *File* widget.
- Verified variable types and target class (“fire”) using *Data Table* and *Data Info*.

---

## 2. Data Understanding
- Reviewed dataset structure and attributes (X, Y, month, day, weather variables).
- Identified:
  - **Inputs:** all environmental and temporal variables  
  - **Output:** fire (T/F)
- Classified features as numeric or categorical.

---

## 3. Data Preparation
### 3.1 Error Detection Using Histogram
- Plotted histograms for each numeric variable (*Distributions – Before*).
- Identified incorrect outliers in `wind` (values = 0).
- Corrected by replacing zeros with the median wind speed in *Preprocess*.

### 3.2 Viewed Histograms After Cleaning
- Confirmed corrected distribution using *Distributions – After*.

---

## 4. Train/Validation/Test Split
- Used *Data Sampler*:
  - **70% → Training**
  - **30% → Testing**
- Validation performed using **5-fold Cross Validation** inside the *Test & Score* widget.

---

## 5. Modelling & Hyperparameter Experiments
Built three types of models in Orange:

### Logistic Regression
- C values tested: 0.1, 1, 10

### Random Forest
- n_estimators: 50, 100, 200  
- max_depth: 5, 10, None

### Support Vector Machine
- Kernels tested: Linear, RBF  
- C values: 0.5, 1, 2  
- gamma: auto, scale (for RBF)

### Validation Method
- Connected all models to *Test & Score*
- Used **5-fold Cross Validation** to compare performance.

### Model Comparison Table
| Model | Hyperparameters | F1-score (Validation) |
|-------|------------------|------------------------|
| Logistic Regression | C=10 | 0.82 |
| Random Forest | n=200, depth=None | **0.89** |
| SVM (RBF) | C=2, gamma=scale | 0.88 |

**Random Forest (n=200, depth=None)** achieved the best validation score.

---

## 6. Final Model Training & Testing
- Trained the final **Random Forest** model using the full 70% training set.
- Evaluated on the 30% test set using *Predictions* + *Confusion Matrix*.

### Confusion Matrix

### Performance Metrics
- Accuracy: 0.887  
- F1-score: 0.807  
- Precision: 0.870  
- Recall: 0.792  

---

## 7. Insights
- Wind, temperature, and FFMC values show the strongest contribution to predictions.
- Model performs slightly better on predicting “T” (fire) than “F”, which is acceptable for safety applications.
- Random Forest provides useful feature importance for interpretation.

---

## 8. References
- Orange Data Mining Documentation: https://orangedatamining.com  
- UCI Forest Fire Dataset description  
- Scikit-learn documentation (for theoretical reference of algorithms)

---

This README serves as a complete record of the modelling and evaluation process for the assignment.
