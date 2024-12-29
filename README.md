# **Google Stock Prediction Report**

---

## **1. Introduction**

### **Objective:**
The aim of this project is to build a **binary classification model** to predict whether the **next day’s closing price** for Google stock will be **higher or lower** compared to the **current day’s closing price**. This approach simulates predicting price direction based on historical patterns.

### **Key Questions:**
1. How accurately can we predict the direction of Google stock prices?  
2. Which features (e.g., rolling averages, volume) are the most important for the prediction?  
3. Which machine learning model—**Logistic Regression**, **Random Forest**, or **XGBoost**—provides the most reliable results?  

---

## **2. Dataset Overview**

### **Data Source:**
The dataset contains daily stock data for **Google (Alphabet Inc.)** from **2004 to 2020**. It includes key financial metrics like opening, closing, high, and low prices, as well as trading volume.

### **Columns:**
- **Date**: Trading date.  
- **Open**: Opening price of the stock.  
- **High**: Maximum price of the stock during the day.  
- **Low**: Minimum price of the stock during the day.  
- **Close**: Closing price of the stock.  
- **Adj Close**: Adjusted closing price considering splits/dividends.  
- **Volume**: Number of shares traded.

### **Preprocessing Steps:**
- Converted `Date` to a datetime format and sorted chronologically.  
- Created a binary target variable:  
  - `Target = 1` if the next day's closing price is higher.  
  - `Target = 0` otherwise.  
- Engineered rolling averages for closing prices and volume as features.  

---

## **3. Exploratory Data Analysis (EDA)**

### **Key Insights:**
1. **Target Distribution**:  
   - About **53% of days** showed an **increase** in closing price, while **47% decreased or remained the same**.  

2. **Correlation Analysis**:  
   - High correlations were observed among **Open**, **Close**, **High**, and **Low** prices.  
   - **Volume** had weaker correlations, suggesting it might capture independent patterns.  

3. **Rolling Features**:  
   - Short-term trends like **5-day rolling averages** showed smoother patterns, helping to filter noise.  

4. **Outlier Detection**:  
   - Volume displayed noticeable spikes around specific dates, possibly related to **earnings announcements** or **market events**.  

---

### **EDA Visualizations:**
1. **Target Distribution** - Pie chart showing 53% uptrend vs. 47% downtrend.  
2. **Correlation Heatmap** - Highlighted relationships among numerical features.  
3. **Feature Distributions Before and After Scaling** - Demonstrated normalization impact on features like **Close** and **Volume**.  
4. **Time-Series Plots** - Trends of **Open**, **Close**, and **Volume** over time.  
5. **Boxplots** - Detected outliers in **Volume** and **Price**.  
6. **Rolling Averages** - Smoother trends captured short-term fluctuations.  

---

## **4. Modeling Approach**

### **Feature Engineering:**
- Used existing features (**Open**, **Close**, **High**, **Low**, **Volume**).  
- Created additional rolling averages (**5-day closing price** and **5-day volume**).  
- Standardized features using **StandardScaler**.  

### **Models Trained:**
1. **Logistic Regression**:  
   - Linear classifier optimized for binary classification.  
2. **Random Forest Classifier**:  
   - Ensemble method capturing non-linear relationships.  
3. **XGBoost Classifier**:  
   - Gradient-boosted trees for enhanced performance.  

### **Training and Testing Split:**
- **80%** training set (chronological split).  
- **20%** test set to prevent data leakage from future values.  

---

## **5. Model Evaluation**

### **Logistic Regression Results:**
- **Accuracy:** **54.14%**  
- **Precision, Recall, and F1-scores:**
  - Class 0 (Price Down): **F1 = 35%**  
  - Class 1 (Price Up): **F1 = 64%**  

**Observations:**
- Better at identifying **price increases (class 1)** than **price decreases (class 0)**.  
- High false-positive rate for **class 0** indicates model bias toward predicting price increases.  

---

### **Random Forest Results:**
- **Accuracy:** **47.84%**  
- **Precision, Recall, and F1-scores:**
  - Class 0 (Price Down): **F1 = 42%**  
  - Class 1 (Price Up): **F1 = 52%**  

**Observations:**
- Random Forest struggled to generalize patterns effectively.  
- Lower performance suggests the need for **hyperparameter tuning** or feature engineering.  

---

### **XGBoost Results:**
- **Accuracy:** **52.53%**  
- **Precision, Recall, and F1-scores:**
  - Class 0 (Price Down): **F1 = 50%**  
  - Class 1 (Price Up): **F1 = 55%**  

**Observations:**
- XGBoost performed **better than Random Forest** but still lacked strong predictive power.  
- Feature importance plots showed **rolling averages** as more influential than raw prices.  

---

### **Model Comparison:**

| Metric                  | Logistic Regression | Random Forest | XGBoost   |
|-------------------------|---------------------|---------------|-----------|
| **Accuracy**            | **54.14%**          | 47.84%        | 52.53%    |
| **F1-Score (Class 1)**  | **64%**             | 52%           | 55%       |
| **ROC-AUC (Avg)**       | 0.58                | 0.51          | **0.60**  |
| **Feature Importance**  | Limited Weighting   | Rolling Features | Rolling Features |

**Key Finding:**  
- **Logistic Regression** performed slightly better than other models, especially for identifying **upward trends**.  
- **XGBoost** showed potential for improvement with **hyperparameter tuning** and **more features**.  
- **Random Forest** performed the weakest, indicating challenges in capturing time-series dependencies.  

---

## **6. Observations**

1. **Performance Limitations**:  
   - Models struggled to predict price movements with high accuracy, likely due to **market noise** and **randomness** in stock data.  
2. **Feature Importance**:  
   - Rolling averages of **close prices** and **volume** showed stronger signals than raw prices.  
3. **Model Limitations**:  
   - Logistic Regression and XGBoost performed moderately well but failed to exceed **60% accuracy**.  
4. **Market Complexity**:  
   - Stock prices are influenced by **external factors** like news, earnings, and economic trends, which were not included in this dataset.
