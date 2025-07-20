The process in **0-ETL-mobility-1.ipynb** is focused on extracting, organizing, and aggregating Spanish human mobility data at the province and municipality level, using both tabular and GIS (geographic) information. Below is a structured summary of the key steps:

---

### 1. **Data Preparation**

- **Download and Extraction:**  
  - Mobility data is downloaded from the Spanish Ministry of Transport’s COVID-19 mobility portal.
  - Data comes in monthly tar files (`yyyymm_maestra1_mitma_municipio.tar`), which are untarred to daily gzipped files and then decompressed to daily txt files.

### 2. **Import Libraries**

- Python libraries such as pandas, numpy, matplotlib, geopandas, zipfile, and requests are imported for data handling, visualization, and geospatial processing.

### 3. **Load GIS Data**

- **Shapefiles** for Spanish municipalities and districts are loaded from compressed zip files using geopandas.
- The relevant shapefile components (`.shp`, `.dbf`, `.prj`, `.shx`) are identified and extracted for both municipalities and districts.
- The shapes are checked for dimensions and projections.

### 4. **Mapping Relationships**

- **District-Municipality Mapping:**  
  - A CSV file mapping districts to municipalities is loaded.
- **Municipality Code Mapping:**  
  - Another CSV maps municipality codes to MITMA codes.
- These are merged to create a comprehensive mapping structure.

### 5. **Province Identification**

- **Function Definition:**  
  - A function is defined to select all municipalities within a given province based on their code ranges and merge them with GIS data.
- **Province Selection:**  
  - The function is applied to define the municipalities and GIS data for each province under study.

### 6. **Regional Grouping and Visualization**

- Provinces are grouped into larger regions (e.g., Galicia, Andalucía) by combining their GIS geometries.
- Plots are generated to visually confirm boundaries and coverage.

### 7. **Prepare Province Data Structures**

- All provinces of interest are organized into a list with their respective data for later aggregation.

### 8. **Date Handling**

- A CSV with available dates is loaded and processed using custom date-formatting functions.

### 9. **Extraction of Mobility Data**

- **Iterative Aggregation:**  
  - For each date and each province:
    - The daily mobility file is loaded.
    - Data is merged with province municipalities.
    - Trip Classification. Aggregations are made for:
      - **Distance:** Number of trips by distance range: 0.5-2km, 2-5km, 5-10km, 10-50km, 50-100km, 100+km
      - **Period:** Number of trips by time period: Groups hours into 4-hour blocks (0-3, 4-7, 8-11, 12-15, 16-19, 20-23)
      - **External vs Internal:** The `destino` field is used to separate internal (within-province) from external (between-province) trips:
         viajes_int = dia[dia.origen == dia.destino]  # Internal trips (within same municipality)
         viajes_ext = dia[dia.origen != dia.destino]  # External trips (between different municipalities)

### 10. **(Not Fully Visible) Data Output**

- - Aggregated results are appended for each day and province.
- While the notebook’s output section is not fully shown, the common next step is to save the aggregated mobility data for later analysis.

---

## **Summary Table**

| Step | Description |
|------|-------------|
| 1    | Download and decompress MITMA mobility data files by day |
| 2    | Import libraries for data analysis and GIS |
| 3    | Load and process Spanish district and municipality GIS shapefiles |
| 4    | Merge and map municipality and district codes for alignment |
| 5    | Identify and extract municipalities for each province using code ranges |
| 6    | Aggregate provinces into regions and visualize maps |
| 7    | Organize province-wise data for aggregation |
| 8    | Process available analysis dates |
| 9    | For each date and province, aggregate mobility data by distance, period, and external/internal flows |
| 10   | (Implied) Save the aggregated results for downstream analysis |

---

### **Key Points**

- The process is highly modular, with clear separation between data download/preparation, GIS processing, mapping/merging, aggregation, and output.
- The notebook leverages both tabular and geospatial sources for high-resolution spatial analysis of human mobility.
- The “destino” (destination) field is uniquely used in this version to distinguish between internal and external province flows, adding an extra analytical dimension compared to the previous notebook.
