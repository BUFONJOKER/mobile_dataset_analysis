Here’s a **clear, structured summary** of what your notebook does step-by-step 👇

---

## 🧾 **Project Overview**

The notebook performs **Exploratory Data Cleaning and Preparation (EDA)** on a *mobile phones dataset (2025)* containing details like company, model, specifications, and launch prices in various countries.
The main focus is on **data cleaning, transformation, and standardization** to make the dataset ready for analysis or visualization.

---

## ⚙️ **1. Initial Setup**

* Imports libraries: `pandas`, `numpy`, `matplotlib.pyplot`, and `seaborn`.
* Loads the dataset:

  ```python
  df = pd.read_csv("dataset/Mobiles Dataset (2025).csv", encoding='ISO-8859-1')
  ```
* Makes a working copy of the dataframe.

---

## 🧩 **2. Data Inspection**

* Displays:

  * First few rows with `df.head()`
  * Column names with `df.columns`
  * Data types using `df.dtypes`

---

## 🏷️ **3. Column Renaming**

Columns are renamed for clarity and consistency:

| Original                    | New Name                               |
| --------------------------- | -------------------------------------- |
| `Mobile Weight`             | `Mobile Weight (gram)`                 |
| `RAM`                       | `RAM (GB)`                             |
| `Front Camera`              | `Front Camera (MP)`                    |
| `Back Camera`               | `Back Camera (MP)`                     |
| `Battery Capacity`          | `Battery Capacity (mAh)`               |
| `Screen Size`               | `Screen Size (inch)`                   |
| `Launched Price (Pakistan)` | `Launched Price (Pakistan USD)`        |
| ...                         | (similar for India, China, USA, Dubai) |

---

## 🧹 **4. Handling Missing and Duplicate Data**

* Checks for missing values → `df.isnull().sum()`
* Finds duplicate rows → `df[df.duplicated()]`
* Removes all duplicates → `df.drop_duplicates(keep=False, inplace=True)`
* Confirms duplicates are gone.

---

## 🔢 **5. Cleaning Numerical Columns**

### 🧮 Weight, RAM, Battery, Screen Size

* Removes text like `'g'`, `'GB'`, `'mAh'`, `'inches'` using `.str.replace()`.
* Converts cleaned strings to numeric using `pd.to_numeric()`.
* Handles commas and stray spaces in battery and size columns.

### 💲 Launch Prices

Cleans and standardizes prices from multiple countries:

* Removes units: `'PKR'`, `'INR'`, `'CNY'`, `'USD'`, `'AED'`.
* Removes commas and spaces.
* Converts to numeric with error coercion.
* Drops rows with missing Pakistan price (`dropna(subset=['Launched Price (Pakistan USD)'])`).

---

## 💱 **6. Currency Normalization**

To convert all prices to USD equivalents, applies scaling factors:

```python
columns = {
    'Launched Price (Pakistan USD)': 281,
    'Launched Price (India USD)': 87.82,
    'Launched Price (China USD)': 7.12,
    'Launched Price (Dubai USD)': 3.67
}
```

Then divides each column’s value by the corresponding rate.

---

## 🧽 **7. Final Cleaning**

* Drops remaining missing values: `df.dropna(inplace=True)`
* Standardizes company names: `df['Company Name'] = df['Company Name'].apply(lambda x: x.title())`

---

## 🧠 **8. Processor Classification**

Creates a new **processor brand** category using a custom function:

```python
def processor_brand(processor):
    # Identifies the chipset family based on keywords
```

Possible outputs:

* Apple
* Exynos
* Snapdragon
* MediaTek
* Unisoc
* Spreadtrum
* Kirin
* Google Tensor
* Qualcomm Snapdragon
* Other

---

## 📸 **9. Camera Columns Cleanup**

* Renames:

  * `Back Camera (MP)` → `Back Camera Main (MP)`
  * `Front Camera (MP)` → `Front Camera Main (MP)`
* Removes extra text like `'MP'`, `'megapixel'`, etc.
* Keeps only numeric camera megapixels.
* Converts to numeric values for analysis.

---

## 📊 **10. Final Dataset**

After all transformations:

* Dataset is fully numeric and standardized.
* Categorical columns: `Company Name`, `Model Name`, `Processor`.
* Numerical columns: Weight, RAM, Camera, Battery, Screen Size, Launch Prices (all in USD).

---

## ✅ **Summary of Data Preparation**

| Step        | Task                | Result                           |
| ----------- | ------------------- | -------------------------------- |
| Load        | Read CSV            | Dataset imported successfully    |
| Clean       | Remove text/symbols | Numeric columns standardized     |
| Convert     | Currency → USD      | Global price comparison possible |
| Drop        | Duplicates & NaN    | Clean and consistent data        |
| Engineer    | Processor brands    | Categorized chipset information  |
| Standardize | Naming conventions  | Uniform column structure         |

---

## 🧾 **Ready For**

* Descriptive statistics (mean, median, distribution)
* Visualizations (e.g., Seaborn plots)
* Correlation and feature analysis
* Price vs. specs modeling or prediction

---

Would you like me to create a **visual summary (flowchart)** or **short markdown version (for README)** of this analysis?
