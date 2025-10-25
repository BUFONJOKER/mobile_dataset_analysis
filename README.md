
---

# 📱 Mobile Dataset Analysis and Visualization

## 🧭 Project Overview
The **Mobile Dataset Analysis and Visualization** project focuses on exploring and modeling smartphone data to extract insights about mobile specifications, performance, and pricing.  
It follows a complete **Data Science Lifecycle**, including:

- Data preprocessing and feature engineering  
- Exploratory data analysis (EDA) and visualization  
- Model training, tuning, and evaluation  
- Deployment via an interactive web app  

The primary goal is to build predictive models (e.g., price prediction or classification of mobile categories) and present insights through visualizations and dashboards.

---

## ⚙️ Workflow

### 1. 🧹 Data Preprocessing
Data preprocessing ensures that the dataset is clean, consistent, and analysis-ready.

**Key steps:**
- **Handling Missing Values:**  
  Missing or null data is treated via imputation (mean, median, or mode) or dropped if irrelevant.  
  ```python
  df['Launched Price (Pakistan USD)'].fillna(df['Launched Price (Pakistan USD)'].median(), inplace=True)
````

* **Removing Duplicates:**

  ```python
  df.drop_duplicates(inplace=True)
  ```

* **Data Type Conversion:**

  ```python
  df[col] = df[col].astype(str).str.replace(r'\D', '', regex=True).astype('int64')
  ```

* **Feature Engineering:**

  * Create new features like `Price_to_Performance_Ratio`, `Pixel_Density`, etc.
  * Encode categorical variables (e.g., *Company Name*, *Processor*).

* **Normalization and Scaling:**
  Scale numerical data to ensure uniform contribution of all features.

---

### 2. 🔍 Exploratory Data Analysis (EDA)

EDA helps discover trends, correlations, and feature relationships.

**Common visualizations:**

* **Univariate:** Histograms, boxplots, KDE plots
* **Bivariate:** Scatterplots, barplots
* **Multivariate:** Heatmaps, pairplots

**Examples:**

```python
sns.barplot(x='Company Name', y='Launched Price (Pakistan USD)', data=df)
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
```

EDA identifies key factors influencing mobile prices — such as **RAM**, **Processor**, and **Battery Capacity**.

---

### 3. 🤖 Model Building

Models are built using **Scikit-learn** for regression or classification tasks.

**Steps:**

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

**Example (Random Forest Regressor):**

```python
from sklearn.ensemble import RandomForestRegressor
model = RandomForestRegressor()
model.fit(X_train, y_train)
```

**Hyperparameter Tuning:**

```python
from sklearn.model_selection import GridSearchCV
grid = GridSearchCV(model, param_grid={'n_estimators':[100,200]}, cv=5)
grid.fit(X_train, y_train)
```

---

### 4. 📊 Model Evaluation

Evaluate model accuracy and generalization using appropriate metrics.

**Regression Metrics:**

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* R² Score

**Classification Metrics:**

* Accuracy
* Precision, Recall, F1-score
* Confusion Matrix / ROC-AUC

**Example:**

```python
from sklearn.metrics import mean_absolute_error, r2_score
print("MAE:", mean_absolute_error(y_test, y_pred))
print("R²:", r2_score(y_test, y_pred))
```

---

### 5. 🚀 Model Deployment

Deployment uses **Streamlit**, allowing users to interact with the model via a simple web UI.

**Steps:**

1. **Save model:**

   ```python
   import joblib
   joblib.dump(model, 'final_model.pkl')
   ```
2. **Build Streamlit App:**

   ```python
   import streamlit as st
   import joblib

   model = joblib.load('final_model.pkl')
   st.title("📱 Mobile Price Predictor")

   ram = st.number_input("Enter RAM (GB):")
   battery = st.number_input("Enter Battery Capacity (mAh):")

   if st.button("Predict Price"):
       prediction = model.predict([[ram, battery]])
       st.success(f"Predicted Price: ${prediction[0]:.2f}")
   ```
3. **Run App:**

   ```bash
   streamlit run app.py
   ```

---

## ⚡ How to Run the Project

### 🧰 1. Install `uv` (Python package manager)

[`uv`](https://github.com/astral-sh/uv) is a fast package and environment manager for Python.

Install it with:

```bash
pip install uv
```

or

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

### 💾 2. Clone the Repository

```bash
git clone https://github.com/<your-username>/mobile-dataset-analysis.git
cd mobile-dataset-analysis
```

---

### 🔄 3. Sync and Install Dependencies

Automatically create a virtual environment and install all required packages:

```bash
uv sync
```

This installs dependencies defined in `pyproject.toml` such as:

* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn
* streamlit

---

### ▶️ 4. Run the Project

Launch the Streamlit app:

```bash
streamlit run app.py
```

The app will open in your browser at:

```
http://localhost:8501
```

---

## 🛠️ Technologies Used

| Category             | Tools / Libraries               |
| -------------------- | ------------------------------- |
| **Language**         | Python                          |
| **Data Handling**    | Pandas, NumPy                   |
| **Visualization**    | Matplotlib, Seaborn             |
| **Machine Learning** | Scikit-learn                    |
| **Deployment**       | Streamlit                       |
| **Package Manager**  | uv                              |
| **Environment**      | Jupyter Notebook / Google Colab |

---

## ✅ Conclusion

This project demonstrates an **end-to-end data science workflow**, from raw data to deployment.

**Key Takeaways:**

* Data cleaning and feature engineering are critical for model performance.
* EDA helps interpret and visualize data effectively.
* Model tuning ensures high accuracy and generalization.
* Streamlit + uv simplify deployment and dependency management.

By integrating data processing, modeling, and interactive deployment, this project provides actionable insights into smartphone market trends and price prediction.

---

```

---

