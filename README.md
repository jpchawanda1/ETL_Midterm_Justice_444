# ETL Midterm Justice 444

---

## 1. Project Overview

This ETL (Extract, Transform, Load) lab demonstrates a complete data pipeline using Python. The project extracts raw and incremental data, applies multiple transformations (including cleaning, categorization, and enrichment), and loads the processed data into a database, ready for analysis and visualization.

### Project Structure

```
ETL_Midterm_<FirstName>_<IDLast3Digits>/
│
├── data/
│   ├── raw_data.csv
│   └── incremental_data.csv
│
├── transformed/
│   ├── transformed_full.csv
│   └── transformed_incremental.csv
│
├── loaded/
│   ├── full_data.db or full_data.parquet
│   └── incremental_data.db or incremental_data.parquet
│
├── etl_extract.ipynb
├── etl_transform.ipynb
├── etl_load.ipynb
├── etl_visualization.ipynb
├── README.md
└── .gitignore
```

---

## 2. ETL Phases

- **`etl_extract.ipynb`**:  
  Extracts raw and incremental datasets from CSV files and prepares them for transformation.

- **`etl_transform.ipynb`**:  
  Applies at least four meaningful transformations to both datasets, such as:
    1. **Remove Duplicate Rows**  
       - *Why:* Ensures each record is unique, preventing double-counting and data skew.  
       - *Example:*  
         - Before: Two identical rows for the same order  
         - After: Only one row remains
    2. **Handle Missing Values**  
       - *Why:* Prevents errors in analysis and ensures data completeness.  
         - *String/Object columns:* Fill with `'Unknown'`  
         - *Datetime columns:* Fill with `1970-01-01`  
         - *Numeric columns:* Fill with the column mean (rounded to 1 significant figure)
    3. **Convert Date Columns to Datetime**  
       - *Why:* Ensures date columns are in a consistent, analyzable format (stripping time for clarity)
    4. **Categorize 'product' Column**  
       - *Why:* Groups similar products for easier analysis and reporting  
       - *Example:*  
         - Before: `product: iPhone, T-shirt, Coke, Book`  
         - After: `product_category: Electronics, Apparel, Food & Beverage, Books, Other`
    5. **Enrichment: Add 'total_price' Column**  
       - *Why:* Provides a calculated field for total transaction value (`total_price = quantity * unit_price`)
    6. **Column Order Standardization**  
       - *Why:* Ensures consistent column order for easier reading and downstream processing.

- **`etl_load.ipynb`**:  
  Loads the transformed CSV files into a SQLite database (`loaded/etl_results.db`). Previews the stored results using SQL queries and displays the data in a formatted table.

---

## 3. Tools Used

- Python 3.x
- Pandas
- NumPy
- SQLite (via `sqlite3`)
- Jupyter Notebook
- Tabulate (for pretty table output)
- OS (for file and directory management)

---

## 4. How to Run the Project

1. **Clone or download the repository.**
2. **Install required packages:**
   ```bash
   pip install pandas numpy tabulate jupyter
   ```
3. **Run each notebook in order:**
    - `etl_extract.ipynb` to extract data
    - `etl_transform.ipynb` to transform data
    - `etl_load.ipynb` to load data and preview results
4. **Check the `transformed/` folder** for output CSVs and the `loaded/` folder for the SQLite database.
5. **Preview results** in the notebook output or by querying the SQLite database directly.

---

## 5. Screenshot of Data Preview

Below is a sample preview of the `full_data` table after loading into SQLite:

*Add your screenshot or example table here.*

---

## 6. Visualizations

The project provides visualizations to analyze the transformed sales data, using data loaded directly from the SQLite database (`loaded/etl_results.db`).

### Included Visualizations

- **Product Comparison**
  - Grouped bar chart and dual-axis plot showing the number of items sold and total revenue per product in 2024.

- **Calendar Heatmap**
  - Displays daily transaction counts for each month in 2024, with integer annotations, up to the latest available date in the data.

All transaction counts in the visualizations are shown as integers. The visualizations are implemented in the `etl_visualization.ipynb` notebook and are designed to be robust and up-to-date.

---
