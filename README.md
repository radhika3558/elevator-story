
# Analyzing MTA elevator outage data 🚇 🛗 🚧

This repository contains code to reproduce the findings featured in our story on subway elevator outages in New York City.

Our methodology is described in at the bottom of the article. [link]

We analyzed publicly available [MTA elevator availability data](https://metrics.mta.info/?subway/elevatorescalatoravailability) and Liftnet data (received via FOIA).

Data that we collected and analyzed is in the data folders inside each of the folders for Part I and Part II.

Jupyter notebooks used for data preprocessing and analysis are available in the notebook of each folder. Descriptions for each notebook are outlined in the Notebooks section below.

## Part 1: Regression modeling for elevator outages

#### Step 1: Connect to Census to add census variables

We connected Elevator availability data to the US census using a Census API key. We then fuzzy match the station address to the latitudinal and longitudinal values. These values were then used to merge with census data on GEOIDs.

Using this merge, we were able to bring in median income data, population data, and the disabled population at the census tract of the station in question.

#### Step 2: Add other requires variables: station ridership, number of routes at station level, and whether a station is a major interchange.

We also added other variables from publicly available data. For example, we added the ridership data from [MTA](https://new.mta.info/agency/new-york-city-transit/subway-bus-ridership-2022), and route data, and determined if the station was a major interchange (number of subway lines > 2).

#### Step 3: Run regression models 

We used multivariable regression models to see whether the variables we added were determinant of the number of elevator outages at the station and the elevator level.

## Running the notebooks

The `elevator outage` folder contains `notebook.ipynb`, which uses data from the following path `data` > `regression` > `elevator_final.csv` (OR) `df_grouped1.csv`

## Part 2: FOIL data

2. `foil_data` > `eda.iphnb` is Sabina's regression with foil data. 
To run `eda.iphnb` you will need to download `2023_subway_censusvar_multire.csv`, which is accessible [here](https://drive.google.com/drive/folders/1uZcIPkzq6sTAGxfVR--rEgShWm6Izdwq?usp=drive_link) in the `processed_data` folder.
