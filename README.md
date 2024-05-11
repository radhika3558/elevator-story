
# Analyzing MTA elevator outage data 🚇 🛗 🚧

This repository contains code to reproduce the findings featured in our story on subway elevator outages in New York City.

Our methodology is described in at the bottom of the article. [link]

We analyzed publicly available [MTA elevator availability data](https://metrics.mta.info/?subway/elevatorescalatoravailability) and Liftnet data (received via FOIA).

Data that we collected and analyzed is in the data folders inside each of the folders for Part I and Part II.

Jupyter notebooks used for data preprocessing and analysis are available in the notebook of each folder. Descriptions for each notebook are outlined in the Notebooks section below.

## Part 1: Regression modeling for elevator outages

### Step 1: Connect to Census to add census variables

We connected Elevator availability data to the US census using a Census API key. We then fuzzy matched the station address to the latitudinal and longitudinal values. These values were then used to merge with census data on GEOIDs.

Using this merge, we were able to bring in median income data, population data, and the disabled population at the census tract of the station in question.

### Step 2: Add other requires variables: station ridership, number of routes at station level, and whether a station is a major interchange.

We also added other variables from publicly available data. For example, we added the ridership data from [MTA](https://new.mta.info/agency/new-york-city-transit/subway-bus-ridership-2022), and route data, and determined if the station was a major interchange (number of subway lines > 2).

### Step 3: Run regression models 

We used multivariable regression models to see whether the variables we added were determinant of the number of elevator outages at the station and the elevator level.

## Running the notebooks

The `elevator outage` folder contains `notebook.ipynb`, which uses data from the following path `data` > `regression` > `elevator_final.csv` (OR) `df_grouped1.csv`

## Part 2: T-test for elevator downtime

### Step 1: Cleaning, Geocoding & Merging with census data

The data we received from our FOIL request contains all maintenance activity automatically captured by LifeNet systems and manually recorded by control desk staff in E&E’s Elevator and Escalator Reporting and Maintenance System (EERMS) of the MTA. The dataset came back large and messy, so we thought it would be reasonable to explain our data cleaning process.

## Cleaning data
We first filtered the dataset down to elevator maintenance activity only, then extracted the station MRNs for later data matching. During the process of extraction, we were unable to capture 147 rows of data, which pertain to maintenance activity at either New Utrecht Av Station (MRN: 73) or Dyckman St Quarters Station (MRN: TBD). This discrepancy occurs because elevators at New Utrecht Av Station did not specify their locations within the station and Dyckman St Quarters Station did not have a Station MRN. 

Please refer to `2023_missing_station_mrn.csv` for missing values in this process.

## Geocoding 
We then filtered down our data according to this dataset of all MTA subway stations retrieved from the New York State Open Data. In this dataset, the Station ID corresponds to the Station MRN in our FOIL data, which we later used for merging to geocode our FOIL data.

Please refer to `cleaning-geocode.ipynb` for our cleaning process.

## Merging with census data
Finally, we merged the mega dataset with census data for further analysis. 

For codes and notebook of this process, please refer to `merge-with-census.ipynb`


To run `eda.iphnb` you will need to download `2023_subway_censusvar_multire.csv`, which is accessible [here](https://drive.google.com/drive/folders/1uZcIPkzq6sTAGxfVR--rEgShWm6Izdwq?usp=drive_link) in the `processed_data` folder.
