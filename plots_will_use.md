---

# 🧩Data Overview

| Type            | Columns                                                                                                                                                                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Categorical** | `Company Name`, `Model Name`, `Processor`                                                                                                                                                                                                                                       |
| **Numerical**   | `Front Camera`, `Back Camera`, `Mobile Weight in grams`, `RAM in GB`, `Battery Capacity in mAh`, `Screen Size in inches`, `Launched Price (Pakistan USD)`, `Launched Price (India USD)`, `Launched Price (China USD)`, `Launched Price (USA USD)`, `Launched Price (Dubai USD)` |

---

# 🎨 ALL SEABORN PLOTS — With Examples for Columns

---

## 🟦 1️⃣ **Categorical ↔ Categorical**

| Goal                            | Example                       | Recommended sns Plots                                           | Purpose                                   |
| ------------------------------- | ----------------------------- | --------------------------------------------------------------- | ----------------------------------------- |
| Compare counts                  | `Company Name` vs `Processor` | `sns.countplot(x='Company Name', hue='Processor')`              | Frequency distribution                    |
| Relationship strength           | `Company Name` vs `Processor` | `sns.heatmap(pd.crosstab(df['Company Name'], df['Processor']))` | Show overlap intensity                    |
| Show multiple categorical views | `Company Name` vs `Processor` | `sns.catplot(kind='count', x='Company Name', hue='Processor')`  | Flexible multi-facet plot                 |
| Category grouping patterns      | `Company Name` vs `Processor` | `sns.clustermap()`                                              | Clustered relationship between categories |

✅ *Best for seeing which companies use which processors.*

---

## 🟩 2️⃣ **Categorical ↔ Numerical**

| Goal                                    | Example                                      | Recommended sns Plots                                                            | Purpose                    |
| --------------------------------------- | -------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------- |
| Compare distributions                   | `Company Name` vs `Launched Price (USA USD)` | `sns.boxplot(x='Company Name', y='Launched Price (USA USD)')`                    | Shows spread, outliers     |
| Compare means                           | `Company Name` vs `Battery Capacity in mAh`  | `sns.barplot(x='Company Name', y='Battery Capacity in mAh')`                     | Mean comparison            |
| Show all individual data points         | `Company Name` vs `Front Camera`             | `sns.stripplot(x='Company Name', y='Front Camera')`                              | Scatter of categories      |
| Avoid overlap in scatter                | `Company Name` vs `Front Camera`             | `sns.swarmplot(x='Company Name', y='Front Camera')`                              | Non-overlapping points     |
| Distribution per category               | `Processor` vs `RAM in GB`                   | `sns.violinplot(x='Processor', y='RAM in GB')`                                   | Density + spread           |
| Combine distributions                   | `Processor` vs `RAM in GB`                   | `sns.boxenplot(x='Processor', y='RAM in GB')`                                    | Better for large data      |
| Compare multiple numerical per category | `Company Name` vs multiple prices            | `sns.pointplot(x='Company Name', y='Launched Price (USA USD)', hue='Processor')` | Trends between categories  |
| Show KDE within categories              | `Processor` vs `Launched Price`              | `sns.kdeplot(y='Launched Price (USA USD)', hue='Processor', multiple='stack')`   | Smooth category comparison |

✅ *Best for comparing prices, specs, or capacities between companies or processors.*

---

## 🟥 3️⃣ **Numerical ↔ Numerical**

| Goal                         | Example                                         | Recommended sns Plots                                                                       | Purpose                             |
| ---------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------- |
| Relationship + trend line    | `RAM in GB` vs `Launched Price (USA USD)`       | `sns.lmplot(x='RAM in GB', y='Launched Price (USA USD)')`                                   | Linear trend fit                    |
| Simple scatter               | `Battery Capacity` vs `Screen Size`             | `sns.scatterplot(x='Battery Capacity in mAh', y='Screen Size in inches')`                   | Basic relationship                  |
| 2D density                   | `Front Camera` vs `Back Camera`                 | `sns.kdeplot(x='Front Camera', y='Back Camera', fill=True)`                                 | Density area                        |
| Show many numeric pairs      | All numeric columns                             | `sns.pairplot(df[numerical_columns])`                                                       | Multiple scatter plots + histograms |
| Correlation matrix           | All numeric columns                             | `sns.heatmap(df.corr(), annot=True, cmap='coolwarm')`                                       | Show correlation values             |
| Regression trend by category | `Battery Capacity` vs `Price`, hue by `Company` | `sns.lmplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', hue='Company Name')` | Trend per company                   |
| Hexbin alternative           | `Screen Size` vs `Price`                        | `sns.jointplot(x='Screen Size in inches', y='Launched Price (USA USD)', kind='hex')`        | Density in hex bins                 |

✅ *Best for analyzing how numerical features relate (e.g. RAM–Price, Battery–Weight).*

---

## 🟨 4️⃣ **Multi-variable (3+ variables)**

| Goal                                | Example                                           | Recommended sns Plots                                                                                                       | Purpose                   |
| ----------------------------------- | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| Add category color                  | `RAM` vs `Price` by `Company`                     | `sns.scatterplot(x='RAM in GB', y='Launched Price (USA USD)', hue='Company Name')`                                          | Third variable by color   |
| Add category size                   | `Battery Capacity` vs `Price`, size=`Screen Size` | `sns.scatterplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', size='Screen Size in inches', hue='Processor')` | Encode 4th dimension      |
| Multi-panel by category             | `RAM` vs `Price`, per `Processor`                 | `sns.relplot(x='RAM in GB', y='Launched Price (USA USD)', col='Processor')`                                                 | Faceted scatter plots     |
| Compare trends for groups           | `Battery Capacity` vs `Price`, by `Company`       | `sns.lmplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', hue='Company Name', col='Processor')`                | Multi-variable trend      |
| Distribution by multiple categories | `RAM in GB` by `Company` & `Processor`            | `sns.boxplot(x='Company Name', y='RAM in GB', hue='Processor')`                                                             | Multi-category comparison |

✅ *Use these when exploring 3D or layered relationships (company + specs + price).*

---

## 🧾 **Summary Table of Plot Types by Use Case**

| Relationship Type         | Plot Types                                                                             | Key sns Functions             |
| ------------------------- | -------------------------------------------------------------------------------------- | ----------------------------- |
| Categorical → Categorical | `countplot`, `heatmap`, `catplot(kind='count')`, `clustermap`                          | Frequency or co-occurrence    |
| Categorical → Numerical   | `barplot`, `boxplot`, `violinplot`, `stripplot`, `swarmplot`, `boxenplot`, `pointplot` | Compare numeric distributions |
| Numerical → Numerical     | `lmplot`, `regplot`, `scatterplot`, `kdeplot`, `pairplot`, `heatmap`, `jointplot`      | Trend, correlation, density   |
| Multi-variable            | `relplot`, `lmplot(hue=...)`, `pairplot`, `facetgrid`, `boxplot(hue=...)`              | Combine multiple dimensions   |

---
