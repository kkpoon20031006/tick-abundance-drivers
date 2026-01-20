# tick-abundance-drivers
Code and data processing workflow for modeling Ixodes scapularis nymph density using ecological data (hosts, climate, and land cover) across eastern NEON U.S. sites.

This repository supports analyses for a multi-site study looking at how host populations, climate, and habitat shape the density of blacklegged tick (Ixodes scapularis) nymphs. The workflow integrates standardized NEON tick and small-mammal data with deer harvest, temperature, and land cover data to build mixed-effects and GAM models.

# Repository Contents
* `neondatadownload.R` – Downloads and compiles NEON tick, small-mammal, vegetation, and climate datasets for all selected sites.
* `processedtick.R` – Cleans and summarizes tick drag data, calculating annual site-level nymphal densities.
* `processedsmallmammal.R` – Processes small-mammal trapping data and estimates abundance using Schnabel estimators.
* `processeddeer.R` – Imports and standardizes state-level deer harvest records to create a proxy for deer abundance.
* `processedenv.R` – Aggregates and summarizes NEON climate data, including minimum temperature and diurnal range.
* `processedland.R` – Extracts and calculates forest cover within 5-km buffers around NEON sites using NLCD raster data.
* `modelanalysis.R` – Fits linear mixed-effects and generalized additive models (LMER and GAM) relating nymphal density to host, climate, and land-cover predictors.

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

# Acknowledgement
This project was conducted under the supervision of Professor David Allen at Middlebury College. I am grateful for his guidance, feedback, and continued support in the development of this analysis.

# Contact
Kingsley Poon, Candidate for Bachelor of Arts in Biology and Neuroscience, Department of Biology & Department of Neuroscience, Middlebury College; kpoon@middlebury.edu

Dr. David Allen, Associate Professor of Biology, Department of Biology, Middlebury College; dallen@middlebury.edu
