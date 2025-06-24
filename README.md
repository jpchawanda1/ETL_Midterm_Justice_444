# ETL Midterm Justice 444

This project demonstrates a simple ETL (Extract, Transform, Load) pipeline using Python and pandas. The pipeline consists of three main steps:

- Adds a 'total_price' column as quantity × unit_price
- **Ensures that `quantity`, `unit_price`, and `total_price` columns are stored as whole numbers (integers) in the transformed CSVs and loaded database tables.**
- Removes duplicate rows

- The SQLite database is created in the `loaded/` directory.
- The transformed CSVs are saved in the `transformed/` directory.
- The preview in the load step shows the first 5 rows of the loaded data.
- All price and quantity figures are stored as integers (no decimals) for consistency.

# 6. Summary of All Data Updates by Notebook

### etl_extract.ipynb
- Loads `raw_data.csv` and `incremental_data.csv`.
- Previews the data using `.head()` and `.info()`.
- Records and displays missing values, duplicate rows, and column names as tables.
- Saves backup copies as `data/raw_data_copy.csv` and `data/incremental_data_copy.csv`.

### etl_transform.ipynb
- Removes duplicate rows from both datasets.
- Handles missing values:
  - Fills missing string/object values with `'Unknown'`.
  - Fills missing numeric values with the column mean (rounded to 1 significant figure).
  - Fills missing datetime values with `1970-01-01`.
- Converts all date columns to datetime and strips time (keeps only the date).
- Categorizes the `product` column into broader groups using a new `product_category` column (e.g., Apparel, Electronics, Books, Food & Beverage, Other).
- Adds a new column `total_price` as `quantity * unit_price`.
- Standardizes column order so that `product_category` comes after `product` and `total_price` comes after `unit_price`.
- Saves the transformed data as `transformed/transformed_full.csv` and `transformed/transformed_incremental.csv`.

### etl_load.ipynb
- Loads the transformed CSVs into a SQLite database (`loaded/etl_results.db`).
- Writes two tables: `full_data` and `incremental_data`.
- Previews the first 5 rows of the `full_data` table using a SQL query, displaying the data in a formatted table with the correct column order.
# ETL Lab Project

## 1. Project Overview
This ETL (Extract, Transform, Load) lab demonstrates a complete data pipeline using Python. The project extracts raw and incremental data, applies multiple transformations (including cleaning, categorization, and formatting), and loads the results into a SQLite database for further analysis. The workflow is organized into modular Jupyter notebooks for each ETL phase.


## 2. ETL Phases
- **etl_extract.ipynb**: Extracts raw and incremental datasets from CSV files and prepares them for transformation.
- **etl_transform.ipynb**: Applies at least four meaningful transformations to both datasets, such as removing duplicates, handling missing values, converting date columns, and categorizing the `product` column. Outputs are saved as transformed CSV files.
    - **Transformations Applied (with Before/After Examples):**
        1. **Remove Duplicate Rows**
           - *What/Why:* Ensures each record is unique, preventing double-counting and data skew.
           - *Before:* Two identical rows for the same order.
           - *After:* Only one row remains.

        2. **Handle Missing Values**
           - *What/Why:* Prevents errors in analysis and ensures data completeness.
           - *String/Object columns:* Fill with `'Unknown'`.
             - *Before:* `customer_name: NaN`
             - *After:* `customer_name: Unknown`
           - *Datetime columns:* Fill with `1970-01-01`.
             - *Before:* `order_date: NaN`
             - *After:* `order_date: 1970-01-01`
           - *Numeric columns:* Fill with the column mean (rounded to 1 significant figure).
             - *Before:* `quantity: NaN` (mean=2.3)
             - *After:* `quantity: 2.0`

        3. **Convert Date Columns to Datetime**
           - *What/Why:* Ensures date columns are in a consistent, analyzable format and strips time for clarity.
           - *Before:* `order_date: 2024-01-01 12:34:56`
           - *After:* `order_date: 2024-01-01`

        4. **Categorize 'product' Column**
           - *What/Why:* Groups similar products for easier analysis and reporting.
           - *Before:* `product: iPhone, T-shirt, Coke, Book`
           - *After:* `product_category: Electronics, Apparel, Food & Beverage, Books, Other`

        5. **Enrichment: Add 'total_price' Column**
           - *What/Why:* Provides a calculated field for total transaction value, useful for financial analysis.
           - *Before:* No `total_price` column.
           - *After:* `total_price = quantity * unit_price`

        6. **Column Order Standardization**
           - *What/Why:* Ensures consistent column order for easier reading and downstream processing.
           - *Before:* Columns in arbitrary order.
           - *After:* `product_category` comes after `product`, `total_price` comes after `unit_price`.
- **etl_load.ipynb**: Loads the transformed CSV files into a SQLite database (`loaded/etl_results.db`). Previews the stored results using SQL queries and displays the data in a formatted table.

## 3. Tools Used
- Python 3.x
- Pandas
- NumPy
- SQLite (via sqlite3)
- Jupyter Notebook
- Tabulate (for pretty table output)
- OS (for file and directory management)

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


## 5. Screenshot of Data Preview
Below is a sample preview of the `full_data` table after loading into SQLite:


## 6. Visualizations

This project provides visualizations to analyze the transformed sales data, using data loaded directly from the SQLite database (`loaded/etl_results.db`).

### Included Visualizations

- **Product Comparison**
  - Grouped bar chart and dual-axis plot showing the number of items sold and total revenue per product in 2024.

- **Calendar Heatmap**
  - Displays daily transaction counts for each month in 2024, with integer annotations, up to the latest available date in the data.

All transaction counts in the visualizations are shown as integers. The visualizations are implemented in the `etl_visualization.ipynb` notebook and are designed to be robust and up-to-date.

# ETL_Midterm_Justice_444
This project demonstrates Full Extraction and Incremental Extraction concepts in ETL (Extract, Transform, Load) processes using Python and pandas. Implemented as a Jupyter Notebook.