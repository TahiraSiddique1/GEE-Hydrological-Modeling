# GEE-Hydrological-Modeling
This script implements the **SCS Curve Number (Soil Conservation Service)** method to estimate daily surface runoff using satellite data and climate reanalysis.

## Methodology
1. **Soil Data:** Uses `OpenLandMap` soil texture to derive Hydrologic Soil Groups (HSG: A, B, C, D).
2. **LULC Data:** Uses `MODIS (MCD12Q1)` for land cover classification.
3. **Curve Number (CN):** A lookup table is applied via GEE expressions to assign CN values based on the Soil-LULC combination.
4. **Antecedent Moisture Condition (AMC):** The script adjusts the CN value based on 5-day antecedent rainfall (AMC I, II, and III).
5. **Climate Data:** Daily precipitation is sourced from `ERA5-Land` (Hourly).
6. **Output:** A time-series chart and spatial map of total runoff ($Q$) in millimeters.

## How to Run
- Define an `aoi` (Area of Interest) in the GEE Geometry tools.
- The script automatically fetches ERA5 rainfall for the year 2018.
- The chart output provides a comparison between Rainfall and Runoff over time.

## Mathematical Formula
The runoff is calculated using:
$$Q = \frac{(P - I_a)^2}{P - I_a + S}$$
*Where:*
- $Q$ = Runoff (mm)
- $P$ = Precipitation (mm)
- $S$ = Potential maximum retention
- $I_a$ = Initial abstraction (0.2S)
