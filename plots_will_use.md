# 📊 Seaborn Plot Guide for Your Mobile Dataset

## 🧩 Data overview
- Categorical:
    - `Company Name`, `Model Name`, `Processor`
- Numerical:
    - `Front Camera`, `Back Camera`, `Mobile Weight in grams`, `RAM in GB`, `Battery Capacity in mAh`, `Screen Size in inches`
    - Launched prices: `Launched Price (Pakistan USD)`, `Launched Price (India USD)`, `Launched Price (China USD)`, `Launched Price (USA USD)`, `Launched Price (Dubai USD)`

---

## 🟦 Categorical ↔ Categorical
- Use to compare frequency and overlap between categories.
- Common goals & code examples:
    - Compare counts
        ```python
        sns.countplot(x='Company Name', hue='Processor', data=df)
        ```
    - Crosstab / heatmap for overlap intensity
        ```python
        sns.heatmap(pd.crosstab(df['Company Name'], df['Processor']), cmap='Blues')
        ```
    - Multi-facet count
        ```python
        sns.catplot(kind='count', x='Company Name', hue='Processor', data=df)
        ```
    - Cluster relationships
        ```python
        sns.clustermap(pd.crosstab(df['Company Name'], df['Processor']))
        ```

---

## 🟩 Categorical ↔ Numerical
- Compare distributions, means, and show individual points per category.
- Examples:
    - Boxplot (distribution + outliers)
        ```python
        sns.boxplot(x='Company Name', y='Launched Price (USA USD)', data=df)
        ```
    - Barplot (means)
        ```python
        sns.barplot(x='Company Name', y='Battery Capacity in mAh', data=df)
        ```
    - Stripplot (all points)
        ```python
        sns.stripplot(x='Company Name', y='Front Camera', data=df)
        ```
    - Swarmplot (non-overlapping points)
        ```python
        sns.swarmplot(x='Company Name', y='Front Camera', data=df)
        ```
    - Violin / boxen / kde examples
        ```python
        sns.violinplot(x='Processor', y='RAM in GB', data=df)
        sns.boxenplot(x='Processor', y='RAM in GB', data=df)
        sns.kdeplot(y='Launched Price (USA USD)', hue='Processor', multiple='stack', data=df)
        ```
    - Pointplot for trends with hue
        ```python
        sns.pointplot(x='Company Name', y='Launched Price (USA USD)', hue='Processor', data=df)
        ```

---

## 🟥 Numerical ↔ Numerical
- Explore relationships, trends, density, and correlations.
- Examples:
    - Regression + trend
        ```python
        sns.lmplot(x='RAM in GB', y='Launched Price (USA USD)', data=df)
        ```
    - Scatter
        ```python
        sns.scatterplot(x='Battery Capacity in mAh', y='Screen Size in inches', data=df)
        ```
    - 2D KDE
        ```python
        sns.kdeplot(x='Front Camera', y='Back Camera', fill=True, data=df)
        ```
    - Pairplot / correlation heatmap / jointplot
        ```python
        sns.pairplot(df[numerical_columns])
        sns.heatmap(df[numerical_columns].corr(), annot=True, cmap='coolwarm')
        sns.jointplot(x='Screen Size in inches', y='Launched Price (USA USD)', kind='hex', data=df)
        ```

---

## 🟨 Multi-variable (3+ variables)
- Encode additional variables via hue, size, cols, or facets.
- Examples:
    - Color by category
        ```python
        sns.scatterplot(x='RAM in GB', y='Launched Price (USA USD)', hue='Company Name', data=df)
        ```
    - Size + hue
        ```python
        sns.scatterplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)',
                                        size='Screen Size in inches', hue='Processor', data=df)
        ```
    - Facets by category
        ```python
        sns.relplot(x='RAM in GB', y='Launched Price (USA USD)', col='Processor', data=df)
        ```
    - Combined lmplot with hue and col
        ```python
        sns.lmplot(x='Battery Capacity in mAh', y='Launched Price (USA USD)',
                             hue='Company Name', col='Processor', data=df)
        ```

---

## 🧾 Quick summary — pick by relationship
- Categorical → Categorical: countplot, heatmap, catplot(kind='count'), clustermap
- Categorical → Numerical: boxplot, violinplot, barplot, stripplot, swarmplot, boxenplot, pointplot, kdeplot
- Numerical → Numerical: lmplot, regplot, scatterplot, kdeplot, pairplot, heatmap, jointplot
- Multi-variable: relplot, lmplot(hue=...), pairplot, facetgrid, scatterplot(size=..., hue=...)

--- 

Tips:
- Start with countplot / boxplot / scatterplot to get a quick sense.
- Use faceting (col/row) and hue to compare groups without overlaying too much.
- Annotate and rotate x labels when categories are many (e.g., plt.xticks(rotation=45)).
- Consider subsampling or boxenplot/violin if the dataset is very large.
