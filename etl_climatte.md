# Climate Data Extraction and Transformation Process

This notebook describes the step-by-step process used to extract, clean, and prepare a comprehensive climate dataset for analysis, combining meteorological and humidity data for several Spanish provinces.

---

## 1. **Importing Libraries**
The script starts by importing key Python libraries:
- **NumPy** and **Pandas** for data manipulation.
- **Matplotlib** for plotting (though not used in the main ETL process).

---

## 2. **Reading Dates**
A CSV file containing relevant dates is loaded as a DataFrame, setting up the temporal dimension for the analysis.

---

## 3. **Loading Meteorological Data**
For each province, meteorological data is:
- Downloaded from [AEMET](https://www.aemet.es) in JSON format.
- Converted from JSON to CSV.
- Loaded back into a DataFrame for further processing.
- Cleaned by dropping unnecessary columns (like unnamed index columns).

This process is repeated for every province included in the study.

---

## 4. **Cleaning Columns**
A list of non-useful columns (e.g., names, time of minimum/maximums, wind direction) is defined and removed from all DataFrames, retaining only relevant meteorological variables.

---

## 5. **Adding Humidity Data**
Humidity data for each province (from Meteoblue graphics) is stored in an Excel file. For each province, the meteorological DataFrame is concatenated with the corresponding humidity data, resulting in a combined DataFrame per province.

---

## 6. **Combining All Provinces**
All provincial climate DataFrames are concatenated into a single DataFrame, creating a unified dataset with all the provinces’ data stacked vertically.

---

## 7. **Unifying Province Names**
Province names are standardized (e.g., "CIUDAD REAL" becomes "CIUDAD_REAL", "A CORUÑA" becomes "LA_CORUÑA", "OURENSE" becomes "ORENSE") to ensure consistency for merging and analysis.

---

## 8. **Sorting and Indexing**
The unified DataFrame is sorted alphabetically by province and by date, then the index is reset and cleaned for a tidy structure.

---

## 9. **Transforming Precipitation Data**
Precipitation data comes in mixed formats (strings with commas, decimals, special flags like "Ip" or "nan"). All precipitation values are:
- Converted to strings.
- Transformed into numeric floats, with special values ("Ip", "nan") set to 0.0.
- Cleaned and replaced in the main DataFrame.

---

## 10. **Final Dataset**
The result is a clean, analysis-ready DataFrame (`datos_clima`) with the following columns:
- **fecha**: Date of observation
- **provincia**: Province name (standardized)
- **altitud**: Altitude
- **tmed**: Mean temperature
- **prec**: Precipitation (in liters)
- **tmin**: Minimum temperature
- **tmax**: Maximum temperature
- **velmedia**: Mean wind speed
- **sol**: Sunlight hours
- **presMax**: Maximum pressure
- **presMin**: Minimum pressure
- **hr**: Relative humidity

The DataFrame is sorted by date and province, ready for further analysis or visualization.

---

### **Summary Table Example**

| fecha       | provincia   | altitud | tmed | prec | tmin | tmax | velmedia | sol  | presMax | presMin | hr  |
|-------------|-------------|---------|------|------|------|------|----------|------|---------|---------|-----|
| 2020-03-01  | ALICANTE    | 43      | 17.6 | 0.0  | 12.6 | 22.6 | 3.1      | 7.0  | 1012.5  | 1007.2  | 64  |
| ...         | ...         | ...     | ...  | ...  | ...  | ...  | ...      | ...  | ...     | ...     | ... |

---

This process ensures a reliable, harmonized dataset for climate analysis across multiple Spanish provinces and time periods.
