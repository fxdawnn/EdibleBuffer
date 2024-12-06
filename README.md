# EdibleBuffer

# Overview
This repository captures the evaluation on [multifunctional landscape design with edible buffer](https://academic.oup.com/pnasnexus/article/2/10/pgad315/7325141). The post-analysis on fireline intensity, burn area, and f-value validation are carefully processed in the Jupyter Notebook. Evaluation was also done in the wildfire simulator FARSITE and suitability analysis MAXENT which would not be able to register into the github. However, the methods and data are carefully captured and stored and can be reproduced by putting the data in the same environment. A cleaner version of the evaluation can be found in [edible buffer repository](https://github.com/fxdawnn/EdibleBuffer) with the main fire intensity simulation.

# Environment
Geopandas
gdal
rasterio
import os
matplotlib
numpy
seaborn
# Wildfire modeling
We evaluated the result for wildfire simulation using the original landscape provided by **LANDFIRE** -- lcp data. We selected the sample file and showed how fuel was modified through Jupyter notebook. However, we captured the original standard fuel product and acquired weather information from **NOAA** for  the evaluation. The experiment is done in Google Cloud Engine where **FARSITE** can be run successfully. The environment image is captured and saved for future reproduction of the simulation. 

- Banana buffer and fuel modification
The landscape is adjusted according to the gdal and other tools. In gdal_lcp.ipynb, we presented a way to modify the landscape and analyze the fuel map. We sampled the Tubbs Fire area in Santa Rosa and presented it in the /landscape_lcp folder with the base fuel map. In the notebook, you can see we mass-produced the modified buffer with an extensive selection of fuel for follow-up evaluation.  The buffer shape file and the fuel map generation would be best accessed with the [old GitHub repo](https://github.com/fxdawnn/VeggieWildfire) with the /testing buffer folder ready. 

- wildfire modeling with modified fuel map
The processed fuel maps would be sent to **FARSITE** and generated post-processed results in fireline intensity and burn area analysis. As you can see from the result, to speed up the **FARSITE** evaluation, we clone the Windows GCE and run the experiment in parallel. Each fuel map would consume 30 ~ 300 mins depending on the burned area. There has been a friendly version **FARSITE** from GitHub but it wasn't able to produce the same fireline intensity outcome as the Windows version which we can monitor the process in GUI. However, a Ubuntu-friendly version would be more than helpful to speed up the process if the fire can be simulated parallelly in a single machine.

- FARSITE validation (F-score)
It's important to validate that our simulation captures the real historical data to prove the future mitigation method. We replicate the Tubbs fire using the historical fire information. Historical data is not always accurate with the fuel map due to a lack of precision in the survey. We decided to project the fuel as shown in some of the studies. And we selected the best F1 score fuel map. The study can be found in [old GitHub repo](https://github.com/fxdawnn/VeggieWildfire). The result data can be accessed through the folder F1data. The experiment was done earlier in the experiment. We analyzed the simulated fire to evaluate the overlayed (true positive) in ArcGIS Pro. The simulated data is in the Google folder upon request. The groundtruth of the historical Tubbs fire can be found in Tubbs Fire satellite data.
- WUI and protected area selection
This is necessary for buffer placement. The more selected method and data, you can refer to the paper. We place the buffer in between the protected area and fire ignition as shown in gdal_lcp. 

- Weather projection
We also show how the temperature projection can be done in a notebook environment. We maintain the weather input in the fire simulator setup. The weather data and other necessary input can be accessed through the Google folder for reproduced results.

> Fuel types are evaluated primarily using the other product and we modified them using the script here and resimulate through  **FARSITE**.

# Result and post-process
- Suitability modeling
The suitability modeling is done with **MAXENT**. We presented mainly the result in the paper after post process with ArcGIS for illustration purpose.

- Fireline intensity evaluation result
The analysis is capture in /evaluation with the collected data of the simulated result. The fire intensity is produced by FarSite and we calculate the fireline intensity in the file and evaluate it.

- Burnt area evaluation
We also evaluated the burn area using gdal in the script.





