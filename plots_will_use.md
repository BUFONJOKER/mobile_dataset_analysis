# 📊 Seaborn Plot Guide for Your Mobile Dataset

## 🧩 Data overview
- Categorical:
    - `Company Name`, `Model Name`, `Processor`
- Numerical:
    - `Front Camera`, `Back Camera`, `Mobile Weight in grams`, `RAM in GB`, `Battery Capacity in mAh`, `Screen Size in inches`
    - Launched prices: `Launched Price (Pakistan USD)`, `Launched Price (India USD)`, `Launched Price (China USD)`, `Launched Price (USA USD)`, `Launched Price (Dubai USD)`

---

## 🟦 Categorical ↔ Categorical
## 🟦 Categorical ↔ Categorical

### 🧪 Common goals & code examples
- Compare counts and overlap between two categorical columns.
- Examples:
    - Count plot (counts by category, with hue)
    ```python
    sns.countplot(x='Company Name', hue='Processor', data=df)
    ```
    - Crosstab heatmap (intensity of overlap)
    ```python
    ct = pd.crosstab(df['Company Name'], df['Processor'])
    sns.heatmap(ct, cmap='Blues', annot=True, fmt='d')
    ```
    - Normalized proportions (row-wise or column-wise)
    ```python
    ct_norm = pd.crosstab(df['Company Name'], df['Processor'], normalize='index')
    sns.heatmap(ct_norm, cmap='YlGnBu', annot=True, fmt='.2f')
    ```
    - Faceted counts
    ```python
    sns.catplot(kind='count', x='Company Name', hue='Processor', col='SomeOtherCategory', data=df)
    ```
    - Clustermap for grouping patterns
    ```python
    sns.clustermap(ct, cmap='viridis', standard_scale=1)
    ```

### 🛠️ Data prep & tips
- Aggregate rare levels (group as "Other") to avoid clutter.
- Order categories explicitly (pd.Categorical) to control axis order.
- Use normalize in crosstab to view proportions instead of raw counts.
- Rotate or wrap x-axis labels when many categories (plt.xticks(rotation=45)).
- Filter low-count combinations or annotate only significant cells.

### ⚙️ Variations & styling
- Add palettes & colorbars: palette='Set2' or cmap='coolwarm'.
- Annotate percentages: fmt='.1%' when using normalized data.
- Use linewidths and linecolor for clearer cell separation.
- Swap rows/cols or sort by total counts to emphasize important categories.

### 🎯 When to use
- Use countplot / catplot for quick frequency comparisons.
- Use heatmap / crosstab when you want intensity or co-occurrence patterns.
- Use clustermap to discover groupings across categorical combinations.

### ✨ Quick patterns
- Quick check: sns.countplot for one-vs-hue.
- Relationship intensity: pd.crosstab -> sns.heatmap.
- Patterns/clusters: sns.clustermap on crosstab.
- Proportions: crosstab(normalize=...) + annotated heatmap.

