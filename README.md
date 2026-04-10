# tick-abundance-drivers
Reproducible workflow for modeling *Ixodes scapularis* nymph density using multi-site ecological data (hosts, climate, and land cover) across eastern U.S. NEON sites.

This repository supports a multi-site analysis investigating how host populations, climate variability, and habitat structure influence the density of blacklegged tick (*Ixodes scapularis*) nymphs. The workflow integrates standardized NEON tick and small-mammal datasets with deer harvest records, temperature data, and NLCD land cover rasters to fit linear mixed-effects (LMER) and generalized additive (GAM) models.

Download the full data archive here:
* [Link to Google Drive](https://drive.google.com/drive/folders/1jJp24PxtIuCXjXVlhJW9c00l7PPKvmxz?usp=sharing)

# Reproducibility
There are two ways to reproduce this analysis. Read both options before deciding which to run.

### Option 1 — Reproduce analyses and figures from pre-processed data (recommended) 

This is the minimal path to replicate all results and figures. Pre-processed `.RData` files are provided in the Google Drive archive and are already in place if you downloaded the full repository. No NEON download or land cover processing is required.
```
setwd("path/to/Ecological Drivers of Tick Abundance")
source("R Scripts/Main.R")
```
`Main.R` will automatically run Sections 2 and 3 (model analysis and figures). Sections 0 and 1 are commented out by default.

Required packages for Option 1: 
```
install.packages(c(
  "tidyverse", "lme4", "MuMIn", "car", "mgcv", "gratia",
  "ggplot2", "patchwork", "sf", "rnaturalearth", "cowplot"
))
```
### Option 2 — Full reproduction from raw data

This option re-downloads NEON data and re-processes all raw inputs before running the analysis. It requires two manual setup steps before running `Main.R`

**Step A - NEON data** is downloaded automatically on first run by `neondatadownload.R`. An internet connection is required. The download may take up to two hours and files will be saved to `Raw Data/NEON Data Files/`. Subsequent runs skip the download if the files are already present.

**Step B - NLCD land cover raster** must be downloaded manually due to their large size (~2–4 GB each). See detailed instructions in `processedland.R` or follow these steps:

1. Go to https://www.mrlc.gov/data
2. Under **Projects** select **Annual NLCD**, under **Products** select **Land Cover**
3. Download **Land Cover (CONUS)** for each year 2013–2023
4. Unzip, rename each .tif to its year (e.g. `2013.tif`), and place in:
   `Raw Data/Landcover Data Files/`

Once both steps are complete, open `Main.R`, uncomment Sections 0 and 1, and also uncomment the Option 2 package block. Then run:
```
setwd("path/to/Ecological Drivers of Tick Abundance")
source("R Scripts/Main.R")
```
Additional packages required for Option 2 (on top of Option 1): 
```
install.packages(c(
  "neonUtilities", "neonOS", "lubridate", "raster"
))
```
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
├── RData Files/
│   ├── Processed Data Files/
│   ├── Lag Files/
│   └── modelanalysis.RData
├── csv Files/
├── Figures/
│   ├── Figures (PDF)/
│   └── Figures (PNG)/
└── Appendix Tables/
```
# Scripts Overview
Main entry point
* `Main.R` – Runs the full pipeline. Sections 0 and 1 are commented out by default (Option 1). Uncomment them for full reproduction (Option 2).

Data downloading (*Option 2 only*)
* `neondatadownload.R` – Downloads and saves NEON tick, small-mammal, and climate datasets.

Data processing (*Option 2 only*)
* `processedtick.R` – Cleans tick drag data and calculates annual site-level nymphal densities.
* `processedsmallmammal.R` – Estimates small-mammal abundance using Schnabel mark-recapture.
* `processeddeer.R` – Standardizes state deer harvest records as a proxy for deer abundance.
* `processedenv.R` – Summarizes NEON climate data (minimum temperature, diurnal range).
* `processedland.R` – Extracts percent forest cover within 5-km buffers using NLCD rasters.

Data analysis (*both options*)
* `modelanalysis.R` – Fits LMER and GAM models; exports `modelanalysis.RData`.

Figures and tables (*both options*)
* `Figures and Tables.R` - Generates all manuscript figures and appendix model-selection tables.
  
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

**Option 1 packages** (Analysis and Figures)
```
install.packages(c(
  "tidyverse", "lme4", "MuMIn", "car", "mgcv", "gratia",
  "ggplot2", "patchwork", "sf", "rnaturalearth", "cowplot"
))
```
**Option 2 additional packages** (Data Downloading and Processing)
```
install.packages(c(
  "neonUtilities", "neonOS", "lubridate", "raster"
))
```
# Acknowledgement
This project was conducted under the supervision of Professor David Allen at Middlebury College. I am grateful for his guidance, feedback, and continued support in the development of this analysis.

# Contact
**Kingsley Poon**  
Bachelor of Arts in Biology and Neuroscience  
Department of Biology & Department of Neuroscience, Middlebury College  
kpoon@middlebury.edu  

**David Allen, PhD**  
Associate Professor of Biology  
Department of Biology, Middlebury College  
dallen@middlebury.edu
