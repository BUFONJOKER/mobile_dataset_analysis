
---

# 🎨 **📊 Seaborn Plot Cheat Sheet (for Your Dataset)**

---

## 🟦 **1️⃣ Categorical ↔ Categorical**

*(Compare category with another category)*

| Goal                                                     | Best sns Plot                  | Example                                                                                   |
| -------------------------------------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------- |
| Compare how many phones each company uses each processor | 🟢 `sns.countplot()`           | `sns.countplot(x='Company Name', hue='Processor', data=df)`                               |
| Visualize overlap between company & processor usage      | 🟣 `sns.heatmap()`             | `sns.heatmap(pd.crosstab(df['Company Name'], df['Processor']), annot=True, cmap='Blues')` |
| Multiple category comparison with facets                 | 🟢 `sns.catplot(kind='count')` | `sns.catplot(x='Processor', hue='Company Name', kind='count', data=df)`                   |
| Cluster companies by processor types                     | 🟣 `sns.clustermap()`          | `sns.clustermap(pd.crosstab(df['Company Name'], df['Processor']))`                        |

✅ **Use these to study company–processor combinations and market patterns.**

---

## 🟩 **2️⃣ Categorical ↔ Numerical**

*(Compare company, model, or processor with numeric specs or prices)*

| Goal                                         | Best sns Plot         | Example                                                                                |
| -------------------------------------------- | --------------------- | -------------------------------------------------------------------------------------- |
| Show distribution of prices per company      | 🟢 `sns.boxplot()`    | `sns.boxplot(x='Company Name', y='Launched Price (USA USD)', data=df)`                 |
| Compare average battery across companies     | 🟢 `sns.barplot()`    | `sns.barplot(x='Company Name', y='Battery Capacity in mAh', data=df)`                  |
| Show all individual phone RAMs per processor | 🟣 `sns.stripplot()`  | `sns.stripplot(x='Processor', y='RAM in GB', data=df)`                                 |
| Spread + density of RAM per processor        | 🟢 `sns.violinplot()` | `sns.violinplot(x='Processor', y='RAM in GB', data=df)`                                |
| For many data points (better than box)       | 🟢 `sns.boxenplot()`  | `sns.boxenplot(x='Company Name', y='Launched Price (Pakistan USD)', data=df)`          |
| Trend line between categories                | 🟣 `sns.pointplot()`  | `sns.pointplot(x='Processor', y='Screen Size in inches', hue='Company Name', data=df)` |

✅ **Best for showing how price, battery, RAM, or screen size differ across companies or processors.**

---

## 🟥 **3️⃣ Numerical ↔ Numerical**

*(Explore relationships, trends, or correlations between numeric specs and prices)*

| Goal                                   | Best sns Plot                  | Example                                                                                                           |
| -------------------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Check linear relationship (trend line) | 🟢 `sns.lmplot()`              | `sns.lmplot(x='RAM in GB', y='Launched Price (USA USD)', data=df)`                                                |
| Simple scatter relationship            | 🟣 `sns.scatterplot()`         | `sns.scatterplot(x='Battery Capacity in mAh', y='Screen Size in inches', data=df)`                                |
| Density of points                      | 🟢 `sns.kdeplot()`             | `sns.kdeplot(x='Front Camera', y='Back Camera', fill=True, data=df)`                                              |
| Many numeric pairs at once             | 🟣 `sns.pairplot()`            | `sns.pairplot(df[['RAM in GB', 'Battery Capacity in mAh', 'Launched Price (USA USD)', 'Screen Size in inches']])` |
| Correlation heatmap                    | 🟢 `sns.heatmap()`             | `sns.heatmap(df.corr(), annot=True, cmap='coolwarm')`                                                             |
| Density with hex bins                  | 🟣 `sns.jointplot(kind='hex')` | `sns.jointplot(x='RAM in GB', y='Launched Price (USA USD)', kind='hex', data=df)`                                 |

✅ **Use these for relationships like Price vs RAM, Price vs Battery, or Screen Size vs Weight.**

---

## 🟨 **4️⃣ Multi-variable (3+ Variables)**

*(Add hue, size, or facets to represent more dimensions)*

| Goal                                    | Best sns Plot          | Example                                                                                                                              |
| --------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Add company color to numeric relation   | 🟢 `sns.scatterplot()` | `sns.scatterplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', hue='Company Name', data=df)`                            |
| Add both color + size encoding          | 🟣 `sns.scatterplot()` | `sns.scatterplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', hue='Processor', size='Screen Size in inches', data=df)` |
| Separate subplots by processor          | 🟢 `sns.relplot()`     | `sns.relplot(x='RAM in GB', y='Launched Price (USA USD)', col='Processor', data=df)`                                                 |
| Compare trend per company per processor | 🟣 `sns.lmplot()`      | `sns.lmplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)', hue='Company Name', col='Processor', data=df)`                |
| Compare RAM across company & processor  | 🟢 `sns.boxplot()`     | `sns.boxplot(x='Company Name', y='RAM in GB', hue='Processor', data=df)`                                                             |

✅ **Use these when you want 3D-style or grouped analysis — e.g., how price changes with RAM for each company and processor.**

---

## 🧾 **Summary Table by Relationship Type**

| Relationship                  | Recommended sns Plots                                                                  |
| ----------------------------- | -------------------------------------------------------------------------------------- |
| **Categorical ↔ Categorical** | `countplot`, `catplot(kind='count')`, `heatmap`, `clustermap`                          |
| **Categorical ↔ Numerical**   | `barplot`, `boxplot`, `violinplot`, `stripplot`, `swarmplot`, `boxenplot`, `pointplot` |
| **Numerical ↔ Numerical**     | `lmplot`, `regplot`, `scatterplot`, `kdeplot`, `pairplot`, `heatmap`, `jointplot`      |
| **Multi-variable (3+)**       | `relplot`, `lmplot(hue=...)`, `pairplot`, `boxplot(hue=...)`, `facetgrid`              |

---
