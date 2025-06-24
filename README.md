# ETL Lab Project

## 1. Project Overview
This ETL (Extract, Transform, Load) lab demonstrates a complete data pipeline using Python. The project extracts raw and incremental data, applies multiple transformations (including cleaning, categorization, and formatting), and loads the results into a SQLite database for further analysis. The workflow is organized into modular Jupyter notebooks for each ETL phase.


## 2. ETL Phases
- **etl_extract.ipynb**: Extracts raw and incremental datasets from CSV files and prepares them for transformation.
- **etl_transform.ipynb**: Applies at least four meaningful transformations to both datasets, such as removing duplicates, handling missing values, converting date columns, and categorizing the 'Purpose' column. Outputs are saved as transformed CSV files.
    - **Handling Missing Values:**
        - For string/object columns: missing values are filled with `'Unknown'`.
        - For datetime columns: missing values are filled with a default date (`1970-01-01`).
        - **For numeric columns: missing values are filled with the column mean** (e.g., `df['col'] = df['col'].fillna(df['col'].mean())`). This ensures that missing numeric data does not bias the dataset with zeros or arbitrary values, and is a common data imputation technique.
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


# ETL_Midterm_Justice_444
This project demonstrates Full Extraction and Incremental Extraction concepts in ETL (Extract, Transform, Load) processes using Python and pandas. Implemented as a Jupyter Notebook.
