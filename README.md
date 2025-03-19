# Product Dataset Analysis

Transforming raw product data into actionable insights through cleaning, analysis, and visualization.

## 📋 Project Overview
This project focuses on analyzing a product dataset containing 4,350 entries, with the goal of cleaning, exploring, and visualizing the data to uncover meaningful insights. The dataset includes details about products such as their names, IDs, categories, prices, publication types (professional or private), and geographical locations. Through systematic data preprocessing, exploratory data analysis (EDA), and visualization, this project demonstrates core data science skills, including data cleaning, handling missing values, and generating actionable insights using Python.

The final cleaned dataset, reduced to 2,970 entries, is prepared for advanced analyses such as price trend analysis or regional market studies. This project serves as a portfolio piece showcasing my expertise in data preprocessing, EDA, and visualization, making it a valuable resource for data science enthusiasts and professionals.

## 🎯 Objectives
- **Clean the Dataset**: Address inconsistencies such as quotation marks, whitespace, and erroneous values (e.g., question marks in product names).
- **Handle Missing Values**: Identify and manage missing data in critical columns (price and Product_name) to ensure data integrity.
- **Explore the Data**: Perform EDA to understand the dataset’s structure, unique values, and distributions.
- **Visualize Insights**: Create visualizations to highlight key trends, such as the distribution of professional vs. private listings.
- **Prepare for Further Analysis**: Deliver a clean dataset ready for advanced analyses like price trends or regional comparisons.

## 🛠️ Methodology
### 1. Data Loading and Initial Inspection
- The dataset (ProductsData.csv) is loaded using pandas with latin-1 encoding to handle special characters.
- Initial inspection reveals 4,350 entries with columns: `Product_name`, `Product_id`, `Product_Category`, `price`, `Professional_Publication`, `Region_address`, and `Local_address`.
- Issues identified: quotation marks around values, extra spaces in price, and missing values in price (770 initially).

### 2. Data Preprocessing
The preprocessing steps ensure the dataset is clean and usable for analysis:

#### Remove Quotation Marks
```python
for col in data.columns:
    data[col] = data[col].str.replace('"', '')
```

#### Clean the `price` Column
```python
data['price'] = data['price'].str.replace(' ', '')
```

#### Standardize Missing Values
```python
import numpy as np
data = data.replace(r'^\s*$', np.nan, regex=True)
```

#### Handle Errors in `Product_name`
```python
data['Product_name'] = data['Product_name'].apply(lambda x: np.nan if str(x).find('?') > -1 else x)
```

#### Identify Unique and Missing Values
```python
# Unique values
categorical = data.select_dtypes(['category', 'object']).columns
for col in categorical:
    print(f"{col}: {data[col].nunique()} unique value(s)")

# Missing values
missing_values = data.isnull().sum()
print("\nMissing values:")
print(missing_values)
```

#### Drop Rows with Missing Values
```python
data.dropna(subset=['price', 'Product_name'], inplace=True)
data['price'] = pd.to_numeric(data['price'], errors='coerce')
```

### 3. Exploratory Data Analysis (EDA)
- **Dataset Overview**: The original dataset had 4,350 entries, 45 unique product categories, and 16 regions, with "Voitures" (654 entries) and "Grand Casablanca" (1,355 entries) being the most frequent.
- **Data Types**: Post-cleaning, `price` is converted to `float64`, while other columns remain as `object`.

### 4. Visualization
#### Publication Type Distribution
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(8, 6))
sns.countplot(data=data, x='Professional_Publication')
plt.title('Distribution of Professional vs. Private Publications', fontsize=14)
plt.xlabel('Publication Type', fontsize=12)
plt.ylabel('Count', fontsize=12)
plt.show()
```

## 📊 Key Findings
- **Data Reduction**: The dataset was reduced from 4,350 to 2,970 entries after removing rows with missing price (1,221) and `Product_name` (380) values.
- **Category Diversity**: 45 unique product categories, with "Voitures" (cars) being the most common (originally 654 entries).
- **Regional Focus**: Grand Casablanca dominates with 1,355 entries in the original dataset.
- **Publication Type**: Private listings significantly outnumber professional ones, as shown in the visualization (originally 2,688 private listings).
- **Data Quality**: The cleaned dataset is free of missing values in critical columns and has a numeric `price` column, making it ready for further analysis.

## 🖼️ Visualizations
### Professional vs. Private Listings
**Insight**: Private sellers dominate the dataset, reflecting a marketplace driven by individual listings.

## 🚀 Getting Started
### Prerequisites
Python 3.7+
Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`
```bash
pip install pandas numpy matplotlib seaborn
```

### Installation
Clone the repository:
```bash
git clone https://github.com/yourusername/product-analysis.git
cd product-analysis
```
Ensure the dataset (`ProductsData.csv`) is in the project directory.
Run the Jupyter Notebook:
```bash
jupyter notebook Product_Analysis.ipynb
```

## Dataset
The dataset (`ProductsData.csv`) is not included in the repository due to size or privacy constraints. It contains 4,350 entries with the following columns:
- `Product_name`
- `Product_id`
- `Product_Category`
- `price`
- `Professional_Publication`
- `Region_address`
- `Local_address`

If you have a similar dataset, you can adapt the code by updating the file path in the notebook.

## 📈 Future Work
- **Price Analysis**: Analyze price trends across categories or regions.
- **Additional Visualizations**: Create plots for top product categories, price distributions, or regional breakdowns.
- **Statistical Analysis**: Perform statistical tests to identify significant differences (e.g., price differences between professional and private listings).
- **Machine Learning**: Use the cleaned dataset for predictive modeling, such as price prediction based on category and region.
