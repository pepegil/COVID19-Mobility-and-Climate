<h1> Extraction, Transformation and Load:   </h1>
<p>Data come from the period March 2020 to January 2021 </p>

  <li> Climate data : Ministerio de Transición Ecológica. (2021). AEMET OpenData. http://www.aemet.es/es/datos_abiertos/AEMET_OpenData </li>
  <li> Relative humidity data : MeteoBlue. (2021). meteoblue weather close to you. https://www.meteoblue.com/es/tiempo/historyclimate/weatherarchive/ </li>
  <li>Mobility data :Ministerio de Transportes Movilidad y Agenda. (2021). Plan de medidas para responder al impacto del COVID 19 en el sector transporte y movilidad. https://www.mitma.es/ministerio/covid-19/evolucion-movilidad-big-data/opendata-movilidad </li>
  <li> Covid-19 data :   Montera34. (2021). escovid19data. https://github.com/montera34/escovid19data/blob/master/data/output/</li>

<p>
</p>
<p>
  <h1> Source code for extraction is here:   </h1>
  <li> Climate : https://github.com/pepegil/Master-Final-project/blob/main/0-ETL-climate.ipynb</li>
  <li> Mobility : https://github.com/pepegil/Master-Final-project/blob/main/0-ETL-mobility-0.ipynb  </li>
  <li> covid19 : https://github.com/pepegil/Master-Final-project/blob/main/0-ETL-covid19.ipynb</li>
</p>

<p> Data are transformed into pandas dataframe. </p>
<p> Then they are saved with names : </p>
<ul> clima.csv </ul>
<ul>clima_ext.csv * This is create with new features derived from the originals</ul>
<ul>movility.csv </ul>
<ul>movility_ext.csv * this is when the field destino is used to separate exterior and interior journeys of municipalities  </ul>
<ul>covid_preprocesado.csv </ul>


Go back https://github.com/pepegil/Master-Final-project/blob/main/README.md
Here's a clear explanation of this code snippet that you can use on your WordPress page:

## Code Explanation: Mobility Data Analysis

This Python script analyzes municipal mobility data from Spain, processing daily travel patterns to understand how people move within and between municipalities.

### What the Code Does:

**1. Initial Setup**
```python
distancias = []
distancias_ext = []
cols_eliminar = ["origen", 'destino']
```
- Creates empty lists to store results
- Defines columns to be removed later in processing

**2. Main Processing Loop**
The code loops through multiple dates, processing mobility data for each day:

```python
for fecha in fechas:
```

**3. Data Loading**
For each date, it:
- Loads a CSV file containing mobility data between Spanish municipalities
- The data includes: origin, destination, time period, distance range, number of trips, and kilometers traveled

**4. Trip Classification**
```python
viajes_int = dia[dia.origen == dia.destino]  # Internal trips (within same municipality)
viajes_ext = dia[dia.origen != dia.destino]  # External trips (between different municipalities)
```

**5. Provincial Analysis**
For each province, the code:
- Merges municipal data with trip information
- Calculates trip totals by:
  - **Distance ranges**: 0.5-2km, 2-5km, 5-10km, 10-50km, 50-100km, 100+km
  - **Time periods**: Groups hours into 4-hour blocks (0-3, 4-7, 8-11, 12-15, 16-19, 20-23)

**6. Data Aggregation**
The script creates a comprehensive summary including:
- Total trips and kilometers for internal movements (within municipalities)
- Total trips and kilometers for external movements (between municipalities)
- All data broken down by distance ranges and time periods

### Key Insights This Analysis Provides:
- **Travel Patterns**: Understanding when people travel most (rush hours, midday, evening)
- **Distance Analysis**: How far people typically travel for different purposes
- **Internal vs External Mobility**: Comparing trips within a municipality versus trips to other areas
- **Provincial Summaries**: Aggregated mobility data for each Spanish province

This type of analysis is valuable for urban planning, transportation infrastructure decisions, and understanding population movement patterns.
