# Bengaluru Metro Last-Mile & Ridership Analysis

## Overview
This project analyzes ridership trends for the Namma Metro (Bengaluru Metro) system to understand the factors driving passenger traffic. The analysis integrates geospatial data, ridership statistics, and public sentiment (tweets) to model station performance and "last-mile" connectivity.

## Key Objectives
* **Walkability Analysis:** quantify the walkability of station catchments using OpenStreetMap data.
* **Ridership Forecasting:** Predict future hourly ridership using time-series forecasting.
* **Driver Analysis:** Determine the impact of location, accessibility, and public sentiment on total station entries.
* **Station Clustering:** Group stations based on ridership patterns and specific passenger complaints.

## Data Sources
The project utilizes the following datasets:
* **Metro Stations (KML):** Geospatial data for station locations (`bengaluru-metro-stations.kml`).
* **Ridership Data (CSV):** Hourly station entry data (`station-hourly.csv`).
* **Twitter Data (CSV):** Passenger tweets for sentiment analysis (`finalbangalore-1.csv`).

## Analysis Workflow
1.  **Data Preprocessing:** * Cleaning and normalizing station names across different datasets.
    * Calculating station centrality (`accessibility_score_km`) using Haversine distance from the city center.
2.  **Network Analysis (OSMnx):**
    * Generating a `walkability_score` for each station by summing the length of walkable paths within a 1km radius.
3.  **Time Series Forecasting (Prophet):**
    * Modeling hourly ridership trends with daily and weekly seasonality components to forecast traffic for the next 30 days.
4.  **Predictive Modeling (Random Forest & SHAP):**
    * Training a Random Forest Regressor to predict `Total_Entries`.
    * Using SHAP (SHapley Additive exPlanations) values to interpret feature importance.
5.  **Clustering:**
    * Grouping stations into clusters such as "Suburban Stations with Access Issues," "Busy Hubs with Ticketing Issues," and "Busiest System Hubs" based on ridership and complaint topics.

## Key Findings
* **Ridership Drivers:** The most significant predictors for ridership are **Centrality** (`accessibility_score_km`) and **Walkability** (`walkability_score`). Station location and local network density are critical factors.
* **Sentiment Impact:** While passengers frequently complain about access issues (footpaths, parking) and ticketing, these sentiment topics were found to have a **low impact** on the predictive model, suggesting they do not currently deter ridership significantly if the location is good.
* **Seasonality:** The Prophet model captures distinct daily and weekly patterns in the ridership data.

## Dependencies
The analysis requires the following Python libraries:
* `pandas`, `numpy`
* `geopandas`, `fiona` (for spatial data)
* `osmnx` (for street network analysis)
* `prophet` (for time series forecasting)
* `shap`, `sklearn` (for modeling and interpretation)
* `matplotlib`, `seaborn`, `wordcloud` (for visualization)

## Usage
To run this analysis:
1.  Ensure all dependencies are installed (see the Setup section in the notebook).
2.  Place the required datasets in the input directory (or update paths in the "Define Data Paths" section).
3.  Execute the notebook cells sequentially to generate the analysis and visualizations.
