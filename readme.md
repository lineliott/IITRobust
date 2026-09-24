# IIT Effectiveness Under Future Climate Scenarios

This is the project folder for analyzing the effectiveness of IIT under future climate scenarios.

## Data

### (1) Mosquito observations

#### Singapore

**Source:** National Environment Agency (NEA), Singapore
**Access:** Restricted

The access to mosquito abundance data from Singapore is not publicly available and requires access approval.

In Singapore, Gravitrap *Ae. aegypti* Index (GAI) data from 2019 to 2024 were obtained from the National Environment Agency of Singapore. GAI measures adult female *Ae. aegypti* abundance by calculating the weekly number of female adults captured in Gravitraps [65,66], normalized by the total number of functioning Gravitraps deployed in each spatial area.

#### Mainland China

**Source:** [China CDC](https://pmc.ncbi.nlm.nih.gov/articles/PMC8428436/)
**Folder:** `CN`

For Mainland China, bi-weekly or monthly Breteau Index (BI) and Mosq-Ovitrap Index (MOI) data from 2016 to 2019 were used as published by China CDC at the province level [9]. Where only graphical results were available, values were extracted using [WebPlotDigitizer](https://automeris.io) [67].

BI measures the number of positive containers or other water bodies per house inspected, while MOI reflects the number of positive ovitraps among all effective ovitraps.

Species information was not recorded for the China dataset, and we assumed *Ae. albopictus*, which is the dominant *Aedes* species across this region based on prior studies [68].

#### United States

**Source:** [CDC Aedes Forecast Project](https://github.com/cdcepi/Aedes-forecast-project-2019-2020)
**Folder:** `US`

In the United States, monthly county-level data of *Ae. aegypti* and *Ae. albopictus* per trap night (ATN) from 2006 to 2019 were used as summarized by the U.S. Centers for Disease Control and Prevention [70].

ATN was calculated as the number of adults identified per cumulative number of nights that traps were operational. We used CO₂-baited traps, including CDC and ABC light traps and Fay-Prince traps, for the analysis. Half the index value was taken to reflect the female population [71].

#### Europe

**Source:** [VectAbundance database](https://www.nature.com/articles/s41597-024-03482-y)
**Folder:** `EU`

In Europe, the VectAbundance database was used, which compiled weekly *Ae. albopictus* egg counts from ovitraps across Albania, France, Italy, and Switzerland between 2010 and 2022. The raw numbers of mosquitoes were collected biweekly or weekly using similar protocols and were standardized through temporal downscaling [69].

### (2) Climate

#### Global future climate projections

**CMIP6:** [Copernicus Climate Data Store — CMIP6 projections](https://cds.climate.copernicus.eu/datasets/projections-cmip6?tab=overview)

## Data processing

### (1) Climate and surveillance grid mapping

Generate longitudinal and latitudinal grid mappings for climate and surveillance data according to administrative areas.

### Singapore

#### `gravitrap_cleaning.R`

1. `gravirap_processing` — mosquito abundance time series with a cleaned time index.
2. `gravitrap_postal` — all recorded postal codes with latitude and longitude.
3. `gravitrap_cleaned.csv` — mosquito abundance by postal code, with the corresponding administrative region and cleaned time index.

#### `grid_mapping.R`

1. `SG_grid.csv` — all recorded postal codes with attached latitude and longitude, appended with the corresponding ISIMIP reference grid.

#### `ISIMIP3_processing.R`

> Run only after all `XX_grid.csv` files are ready.

1. `SG_gfdl-cm6a-lr_ssp126.csv` — precipitation and temperature by reference grid, GCM, and SSP in time series format.

#### `ISIMIP_mos_SG.R`

1. `/processed_data_20260310/` — mosquito abundance combined with precipitation and temperature by region, GCM, and SSP in time series format.

### Visualization

#### `worldmap.R`

Renders maps for historical abundance, baseline projections, and intervention projections. This script is called by `BX_final.R`, `CA_final.R`, and `HA_final.R`.
