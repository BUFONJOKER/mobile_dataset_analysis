
---

# 📱 **Mobile Dataset Analysis and Visualization**

## 🧭 **Project Overview**

The **Mobile Dataset Analysis and Visualization** project focuses on exploring and modeling smartphone data to extract insights about mobile specifications, performance, and pricing.
It follows a complete **Data Science Lifecycle**, including:

* Data preprocessing and feature engineering
* Exploratory data analysis (EDA) and visualization
* Model training, tuning, and evaluation
* Deployment via an interactive web app

The primary goal is to build predictive models (e.g., price prediction or classification of mobile categories) and present insights through visualizations and dashboards.

---

## ⚙️ **Workflow**

### 1. 🧹 **Data Preprocessing**

Data preprocessing ensures that the dataset is clean, consistent, and analysis-ready.

**Key steps:**

* **Handling Missing Values:**
  Missing or null data is treated via imputation (mean, median, or mode) or dropped if irrelevant.
  Example:

  ```python
  df['Launched Price (Pakistan USD)'].fillna(df['Launched Price (Pakistan USD)'].median(), inplace=True)
  ```

* **Removing Duplicates:**
  Duplicate rows are dropped to ensure unbiased results.

  ```python
  df.drop_duplicates(inplace=True)
  ```

* **Data Type Conversion:**
  Prices often contain currency symbols; they are cleaned using regex and converted to numeric types.

  ```python
  df[col] = df[col].astype(str).str.replace(r'\D', '', regex=True).astype('int64')
  ```

* **Feature Engineering:**

  * Creating new features like `Price_to_Performance_Ratio` or `Pixel_Density`.
  * Encoding categorical variables (e.g., *Company Name*, *Processor*) using one-hot or label encoding.

* **Normalization and Scaling:**
  Scaling ensures uniform feature contribution, especially for algorithms sensitive to magnitude differences.

---

### 2. 🔍 **Exploratory Data Analysis (EDA)**

EDA provides insights into patterns, trends, and correlations across features.

**Visual techniques include:**

* **Univariate Analysis:**

  * Histograms and KDE plots show distributions (e.g., *Battery Capacity*, *Price*).
  * Boxplots highlight outliers.

* **Bivariate Analysis:**

  * Scatter plots for numerical relationships (*Screen Size vs Price*).
  * Bar plots for categorical comparisons (*Company Name vs Average Price*).

* **Multivariate Analysis:**

  * Heatmaps for correlation analysis.
  * Pairplots for multidimensional relationships.

**Example plots using Seaborn:**

```python
sns.barplot(x='Company Name', y='Launched Price (Pakistan USD)', data=df)
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
```

EDA helps identify the key factors influencing mobile prices — such as **RAM**, **Processor**, and **Battery Capacity**.

---

### 3. 🤖 **Model Building**

Machine learning models are built using **Scikit-learn** to predict target variables such as *Launched Price* or *Mobile Category*.

**Steps:**

* **Feature Selection:**
  Important features are selected using correlation analysis and feature importance techniques.

* **Splitting the Dataset:**

  ```python
  from sklearn.model_selection import train_test_split
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
  ```

* **Model Training:**
  Models like **Linear Regression**, **Decision Tree**, or **Random Forest** are trained:

  ```python
  from sklearn.ensemble import RandomForestRegressor
  model = RandomForestRegressor()
  model.fit(X_train, y_train)
  ```

* **Hyperparameter Tuning:**
  Optimized using GridSearchCV for best performance.

  ```python
  from sklearn.model_selection import GridSearchCV
  grid = GridSearchCV(model, param_grid={'n_estimators':[100,200]}, cv=5)
  grid.fit(X_train, y_train)
  ```

---

### 4. 📊 **Model Evaluation**

Each model’s performance is evaluated to determine accuracy and reliability.

**Regression Metrics:**

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* R² Score

**Classification Metrics (if classification model):**

* Accuracy
* Precision, Recall, F1-score
* Confusion Matrix and ROC Curve

**Example:**

```python
from sklearn.metrics import mean_absolute_error, r2_score
print("MAE:", mean_absolute_error(y_test, y_pred))
print("R²:", r2_score(y_test, y_pred))
```

---

### 5. 🚀 **Model Deployment**

Deployment is done through **Streamlit**, enabling users to interact with the trained model through a web interface.

**Steps:**

1. **Model Serialization:**

   ```python
   import joblib
   joblib.dump(model, 'final_model.pkl')
   ```
2. **Building the Streamlit App:**
   Users can input phone specs and get predictions in real time.
3. **Deployment:**
   Hosted on Streamlit Cloud, Heroku, or Render for easy access.

Example Streamlit code:

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

---

## ⚡ **How to Run the Project**

### 🧰 **1. Install `uv` (Python package manager)**

[`uv`](https://github.com/astral-sh/uv) is a modern, fast package and environment manager for Python — much faster than pip or conda.

**Install it with:**

```bash
pip install uv
```

or

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

### 💾 **2. Clone the Repository**

```bash
git clone https://github.com/<your-username>/mobile-dataset-analysis.git
cd mobile-dataset-analysis
```

---

### 🔄 **3. Sync and Install All Dependencies Automatically**

Run the following command to automatically create a virtual environment and install all required libraries:

```bash
uv sync
```

This command uses the `uv.lock` or `pyproject.toml` file to install dependencies like **Pandas**, **NumPy**, **Matplotlib**, **Seaborn**, **Scikit-learn**, and **Streamlit**.

---

### ▶️ **4. Run the Project**

Once setup is complete, launch the Streamlit app:

```bash
streamlit run app.py
```

The app will open in your browser at:

```
http://localhost:8501
```

---

## 🛠️ **Technologies Used**

| Category                 | Tools / Libraries               |
| ------------------------ | ------------------------------- |
| **Programming Language** | Python                          |
| **Data Handling**        | Pandas, NumPy                   |
| **Visualization**        | Matplotlib, Seaborn             |
| **Machine Learning**     | Scikit-learn                    |
| **Deployment**           | Streamlit                       |
| **Package Management**   | uv                              |
| **Environment**          | Jupyter Notebook / Google Colab |

---

## ✅ **Conclusion**

This project demonstrates an **end-to-end data science workflow**, from cleaning raw mobile data to deploying an interactive web app.

Key learnings:

* Effective preprocessing and feature engineering improve model accuracy.
* EDA helps visualize and interpret data patterns meaningfully.
* Model tuning and evaluation ensure robustness.
* Streamlit and `uv` simplify deployment and environment management.

By combining analytical rigor and interactive visualization, this project provides valuable insights into the smartphone market — enabling better predictions and data-driven decisions.

---
