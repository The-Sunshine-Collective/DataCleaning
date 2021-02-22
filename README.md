# DataCleaning

Problem Statement: 
Solar energy is increasingly available and practical for residential and commercial use, but the complexity of data involved in decision making and high up-front cost makes choosing solar seem inacessible to many consumers. This is especially true in urban environments where roof heights are greatly varied and neighboring buildings can throw roofs into shadow for significant portions of the day. Our goal is to streamline the data inputs so users can be presented with tailored potential long-term savings figures with a minimum of complexity to make the decision to adopt solar more accessible and properly balanced against cost. 

## Guide to files:
- Solar_EDA.ipynb: This Jupyter notebook was created to gather potentially useful data, ensure it could be read in, and then select, clean, and merge into a single workable dataset which was written out to both a csv and a shapefile. Analysis was done to gather insights and some visualizations were created and saved as analyticals and visual aids. 
- Shadow_Merge.ipynb: This Jupyter notebook loads in the cleaned shapefile produced by Solar_EDA.ipynb and adds columns derived from the VIDA-NYU Shadow Accrual Maps project (https://github.com/VIDA-NYU/shadow-accrual-maps). The resulting dataframe is written to csv.
- Capacity_Calc.ipynb: This Jupyter notebook loads in the cleaned shapefile produced by Solar_EDA.ipynb and data from NYCHA's ACCESSolar programe (https://data.cityofnewyork.us/Housing-Development/NYCHA-ACCESSolar-Opportunities/gbgg-xjuf). The ACCESSolar data covers a small subset of the buildings in our cleaned dataset and includes measurements of roof areas and estimates of potential solar capacity. By merging with this data on Building Identification Number, I was able to test my estimates against theirs and examine the relationship their data establishes between roof area and estimated solar capacity.

## Methods:
The majority of the data was gathered from the NYC Open Data portal (https://opendata.cityofnewyork.us/). Data collected from this portal and considered for use included raster data of land cover and air pollution, vector data on tree canopy change, shapefiles on trees, building footprints, and address points, and csv files on the 2015 Tree Census and the ACCESSolar program. Data from other sources includes shapefiles of climate and solar data from the National Solar Radiation Database (NSRDB: https://nsrdb.nrel.gov/), binary files containing shadow accrual data from VIDA-NYU Shadow Accrual Maps project (https://github.com/VIDA-NYU/shadow-accrual-maps), and pdf files on typical utility billing from the New York Department of Public Services (https://www3.dps.ny.gov/W/PSCWeb.nsf/All/C56A606DB183531F852576A50069A75D). The geopandas module was used to read and write shape files from Jupyter Notebooks, the pandas library was used to read and write csv files, and GDAL was used to read in raster files, though ultimately the raster files were not used. Data cleaning and manipulation was done in Jupyter Notebook using pandas/geopandas, with visualizations created using matplotlib, seaborn, and the geopandas .plot method, which uses the descartes and shapely modules. 

## Conclusions:
Though using the NYC Open Data files was complicated slightly by the use of many different formats and standards, with departmental differences apparent in column choice and nomenclature, the enormous amount of data available and the existence of several standardized identifiers ultimately made it possible to bring in data from several different datasets with minimal loss. The address points dataset, building footprints dataset, and ACCESSolar dataset could all be referenced against each other using the Building Identification Number (BIN) and in cleaning and merging the address points and building footprints, only about 50 rows of data were dropped out of a total of over 300,000. The time span between the datasets was entirely limited to within a decade, making complications from time-based discrepancies minimal. The NYU shadow data, on the other hand, was extremely difficult to work with due to the format and lack of documentation and metadata. Ultimately, it was found that the distribution of heights and building footprints is extraordinarily right-skewed, with new, tall buildings with relatively small footprints being built. This gives us both an idea of our typical user and confirms that conditions exist where building shadows become an important factor. A comparison with the ACCESSolar data reinforced the assumption that building footprints are a reasonable estimate of roof space, but also suggested that capacity estimates based on solar panels currently on the market may be too high, and it was decided to defer to the ACCESSolar program's judgment and create a more conservative estimation factor derived from a linear regression of their data. 

## Requirements:
Because these Jupyter notebooks require a "data" directory to be located in the parent directory to this repo, and this directory is not included in the repo, none of the notebooks as presented here are in a functional state. However, were they to be made functional, they would require the aforementioned directory of data files as well as the following software:
- Jupyter Notebook
- numpy
- pandas
- geopandas
- matplotlib
- seaborn
- GDAL
- descartes
- struct
and the dependencies for all of the modules listed above. 
