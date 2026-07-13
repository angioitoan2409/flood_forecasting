# Flood Forecasting Simulation with RIM2D

## Project Overview
This repository contains an independent research project conducted for academic and investigative purposes. It is designed to simulate urban inundation and evaluate flood risk forecasting methodologies. The project framework and implementation are heavily based on the following peer-reviewed article:

> **Apel, H., Benisch, J., Helm, B., Vorogushyn, S. and Merz, B., 2024.** *Fast urban inundation simulation with RIM2D for flood risk assessment and forecasting.* Frontiers in Water, 6, p.1310182.
> * DOI: [10.3389/frwa.2024.1310182](https://doi.org/10.3389/frwa.2024.1310182)
> * Article URL: [Frontiers in Water](https://www.frontiersin.org/journals/water/articles/10.3389/frwa.2024.1310182/full)

## Directory Structure and Source Code Description

The project is modularized into several Jupyter Notebooks, each handling specific stages of the spatial and meteorological data preprocessing pipeline required for the simulation:

* **`data_processing.ipynb`**: Spatial data processing. This module utilizes open-access Digital Elevation Model (DEM) and Surface Sealing datasets provided by the Federal State of Saxony, Germany (sources: [Geodaten Sachsen](https://www.geodaten.sachsen.de/downloadbereich-digitale-hoehenmodelle-4851.html) and [LUIS Sachsen](https://luis.sachsen.de/boden/versiegelung.html)). It is responsible for generating four of the five foundational raster matrices essential for the inundation model.
* **`getting_building.ipynb`**: Automated extraction of building footprints[cite: 4]. This notebook employs the `osmnx` and `geopandas` libraries to query and extract building polygon geometries directly from the OpenStreetMap (OSM) database, constrained by the bounding box of the study area[cite: 4]. The geometries are subsequently reprojected to the `EPSG:25833` coordinate reference system and exported as a GeoPackage, serving as the fifth foundational raster layer (the building mask)[cite: 4].
* **`radolan_events.ipynb`**: Precipitation data acquisition. Manages the downloading, extraction, and preliminary processing of raw RADOLAN (weather radar) datasets corresponding to eight historical flood events within the designated study area[cite: 1].
* **`radolan_aligned.ipynb`**: Spatial synchronization of meteorological data. This script reprojects and spatially aligns the extracted RADOLAN precipitation grids to ensure perfect conformity with the model's primary Digital Terrain Model (DTM) grid resolution and coordinate system (`EPSG:25833`)[cite: 2].
* **`ms_checking.ipynb`**: Cross-validation and sanity testing. Evaluates the spatial accuracy and volumetric consistency of the generated sewer system masks (ms5 and ms2) against the empirical results documented in the reference paper[cite: 3]. This validation is executed following the manual delineation of geographical coordinates via QGIS[cite: 3].
* **`test.ipynb`**: Sandbox environment. Contains experimental scripts and algorithms currently under active development and testing.

## Data Sources
1. **Topographical and Surface Data:** Digital Elevation Model (DEM) and Surface Sealing data from the Federal State of Saxony, Germany.
2. **Infrastructure Data:** OpenStreetMap building footprints (accessed via the OSMnx API)[cite: 4].
3. **Meteorological Data:** RADOLAN precipitation data provided by the Deutscher Wetterdienst (DWD - German Meteorological Service)[cite: 1].

## Installation and Usage

Ensure all required Python dependencies are installed prior to executing the notebooks:
```bash
pip install osmnx geopandas rasterio numpy matplotlib
