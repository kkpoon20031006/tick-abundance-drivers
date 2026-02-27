# tick-abundance-drivers
Reproducible workflow for modeling Ixodes scapularis nymph density using multi-site ecological data (hosts, climate, and land cover) across eastern U.S. NEON sites.

This repository supports a multi-site analysis investigating how host populations, climate variability, and habitat structure influence the density of blacklegged tick (Ixodes scapularis) nymphs. The workflow integrates standardized NEON tick and small-mammal datasets with deer harvest records, temperature data, and NLCD land cover rasters to fit linear mixed-effects (LMER) and generalized additive (GAM) models.

# Reproducibility
To reproduce the full analysis from raw data to figures:
```
setwd("path/to/Ecological Drivers of Tick Abundance")
source("R Scripts/Main.R")
```
`Main.R` executes the complete pipeline in the correct order:

1. Download NEON data (if needed)
2. Process tick, host, climate, deer, and land-cover data
3. Merge datasets
4. Fit LMER and GAM models
5. Generate all figures
6. Export appendix tables

All outputs are written automatically to their designated folders.

# Repository Structure
```
Ecological Drivers of Tick Abundance/
├── R Scripts/
│   ├── Main.R
│   ├── Data Downloading R Scripts/
│   ├── Data Processing R Scripts/
│   ├── Data Analysis R Scripts/
│   └── Data Presenting R Scripts/
├── Raw Data/
│   ├── NEON Data Files/
│   ├── Deer Data Files/
│   ├── Landcover Data Files/
│   └── Ixodes_Pathogens_County_Status_Geodata_1996_2022/
├── .RData Files/
│   ├── Processed Data Files/
│   ├── Lag Files/
│   └── modelanalysis.RData
├── .csv Files/
├── Figures/
│   ├── Figures (PDF)/
│   └── Figures (PNG)/
└── Appendix Tables/
```

# Scripts Overview
Main entry point
* `Main.R` – Runs the full analysis pipeline from start to finish.

Data downloading
* `neondatadownload.R` – Downloads and compiles NEON tick, small-mammal, vegetation, and climate datasets for all selected sites.

Data processing
* `processedtick.R` – Cleans and summarizes tick drag data, calculating annual site-level nymphal densities.
* `processedsmallmammal.R` – Processes small-mammal trapping data and estimates abundance using Schnabel estimators.
* `processeddeer.R` – Imports and standardizes state-level deer harvest records to create a proxy for deer abundance.
* `processedenv.R` – Aggregates and summarizes NEON climate data, including minimum temperature and diurnal range.
* `processedland.R` – Extracts and calculates forest cover within 5-km buffers around NEON sites using NLCD raster data.

Data analysis
* `modelanalysis.R` – Fits linear mixed-effects and generalized additive models (LMER and GAM) relating nymphal density to host, climate, and land-cover predictors.

Figures and tables
* `Figures and Tables.R` - Generates figures and appendix tables used in the manuscript.

# Data Sources
[NEON Data Portal](https://data.neonscience.org)

[National Land Cover Database](https://www.mrlc.gov/data)

**State wildlife agencies’ deer harvest reports:**  
-[Alabama](https://www.outdooralabama.com/)  
-[Florida](https://myfwc.com/)  
-[Maryland](https://dnr.maryland.gov/wildlife/Pages/default.aspx)  
-[Tennessee](https://hunterstoolbox.gooutdoorstennessee.com/)  
-[Virginia](https://dwr.virginia.gov/)  
-[Wisconsin](https://dnr.wisconsin.gov/)  
-[Massachusetts](https://www.mass.gov/orgs/division-of-fisheries-and-wildlife)  
-[Kansas](https://ksoutdoors.gov/)  
-[New Hampshire](https://www.wildlife.nh.gov/)  
-[Michigan](https://www.michigan.gov/dnr)  
-[Oklahoma](https://www.wildlifedepartment.com/)  
-[Georgia](https://gadnr.org/)  
-[Texas](https://tpwd.texas.gov/)

[U.S. Fish and Wildlife Service hunting license data](https://www.fws.gov/program/wildlife-and-sport-fish-restoration/apportionments-and-licenses-data)

# Dependencies
R version: 4.2.1

Required packages: `dplyr`, `ggplot2`, `patchwork`, `mgcv`, `gratia`, `RColorBrewer`,`sf`, `raster`, `rnaturalearth`, `rnaturalearthdata`, `lme4`, `MuMIn`, `car`, `lubridate`, `neonUtilities`, `neonOS`, `Rcapture`

Install all dependencies with: 
```
install.packages(c(
  "dplyr","ggplot2","patchwork","mgcv","gratia","sf","raster",
  "rnaturalearth","lme4","MuMIn","car","lubridate",
  "neonUtilities","neonOS","Rcapture"
))
```
# Acknowledgement
This project was conducted under the supervision of Professor David Allen at Middlebury College. I am grateful for his guidance, feedback, and continued support in the development of this analysis.

# Contact
Kingsley Poon, Bachelor of Arts in Biology and Neuroscience, Department of Biology & Department of Neuroscience, Middlebury College; kpoon@middlebury.edu

Dr. David Allen, Associate Professor of Biology, Department of Biology, Middlebury College; dallen@middlebury.edu
