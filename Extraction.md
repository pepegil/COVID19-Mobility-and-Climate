<h2>All data is extracted from the www.</h2>

<p>Data come from the period March 2020 to January 2021 and can be downloaded here:</p>

  <li> Climate data : Ministerio de Transición Ecológica. (2021). AEMET OpenData. http://www.aemet.es/es/datos_abiertos/AEMET_OpenData </li>
      0-ETL-climate.ipynb
  <li> Relative humidity data : MeteoBlue. (2021). meteoblue weather close to you. https://www.meteoblue.com/es/tiempo/historyclimate/weatherarchive/ </li>
  <li>Mobility data :Ministerio de Transportes Movilidad y Agenda. (2021). Plan de medidas para responder al impacto del COVID 19 en el sector transporte y movilidad. https://www.mitma.es/ministerio/covid-19/evolucion-movilidad-big-data/opendata-movilidad </li>
  mobility-0.ipynb
  <li> Covid-19 data :   Montera34. (2021). escovid19data. https://github.com/montera34/escovid19data/blob/master/data/output/</li>
0-ETL-covid19.ipynb
<p>
  
</p>

<p> Data are transformed into pandas dataframe. </p>
<p> Then they are saved with names : </p>
<ul> clima.csv </ul>
<ul>clima_ext.csv * This is create with new features derived from the originals</ul>
<ul>movility.csv </ul>
<ul>movility_ext.csv * this is when the field destino is used to separate exterior and interior journeys   </ul>

Go back https://github.com/pepegil/prueba-0/blob/main/README.md
