# Data guide to the UST Global Hackathon on the 6th October 2020

## Overview
This guide provides an overview of all the data sources within the Covid-19 dataset used for the hackathon. To be used in conjuction with the associated API guides and notebooks containing examples of data innovation with the dataset.

## List of datasets within the Covid-19 dataset
All the data that collectively form our Covid-19 dataset are listed below, with sources and where and how we have enriched this data.

### 1. Covid-19 incidence related data

#### Daily incidence rates (Local Authority level)
Reporting daily on the number of [newly recorded Covid-19 cases](https://coronavirus.data.gov.uk/cases) by Local Authority. This data also reports the Local Authority population size, enabling the incidence rate (typically per 10,000 or per 100,000 people) of Covid-19 to be derived.

This data can be accessed via API number 3, located in the table at the end of the section, a notebook with example analysis can be found [here](https://www.tablesgenerator.com/markdown_tables)

#### Daily incidence rates (Middle Layer Super Output Area level)
Reporting daily on the number of [newly recorded Covid-19 cases](https://coronavirus.data.gov.uk/cases) at the 
Middle Layer Super Output Area (MSOA). This data also reports the MSOA population size, enabling the incidence rate (typically per 10,000 or per 100,000 people) of Covid-19 to be derived. The data is updated daily, with a new column added each week, the `latest_7_days` column contains the latest data most of the time, if the column is null then the latest data is contained within the latest `wk_XX` column. 

This data can be retrieved via [this API](https://c19downloads.azureedge.net/downloads/msoa_data/MSOAs_latest.csv) and can be used in conjuction with any other dataset reporting at MSOA level, including the geojson that is available in section 4 below.

#### Daily NHS 111 and 999 Covid-19 Triage rates (Local Authority level)
NHS Digital publishes the number of NHS 111 and 999 triages for Covid-19 daily. Reporting by age and gender at a Clinical Commissioning Group (CCG) level, we have attributed these figures at a Local Authority level to make them comparable with other incidence and demography data and also the business and economic metrics we outline in section 3 below.


<details open>
<summary><strong>Section 1 API details</strong></summary>
<br>
  
| API Number | Method | Endpoint | Description |
|-----------|-------------|----------|----------|
|3           |GET             |https://iqapi.azurewebsites.net/api/CoronaVirusCase          | Cumulative and daily Covid-19 incidence rates by date and upper and lower level Local Authority          |
|18           |GET             |https://iqapi.azurewebsites.net/api/UkmsoaCases          | Enriched dataset of weekly Covid-19 incidence rates at Middle Super Output Area (MSOA) level         |
|6           |GET            |https://iqapi.azurewebsites.net/api/NhsPathwaysCovid19Data          |Enriched dataset reporting on estimated daily NHS 111, 111-online and 999 triages for Covid-19 triages at a Local Authority level          |

</details>



### 2. Population demography related data

#### UK population breakdown (Local Authority level)

The Office for National Statistics publishes a [mid-yearly report](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/populationestimatesforukenglandandwalesscotlandandnorthernireland) estimating the population breakdown for every Local Authority in the UK, with several pages of supplementary information. We have collated the key attributes from this report into a table which includes an age breakdown, the median age and population density of each Local Authority.

This data can be accessed through [this API](https://iqapi.azurewebsites.net/api/UKPopulationDemographicData2018).

#### England/Wales age distribution (Local Authority/LSOA level)

The ONS also separately publishes an [age breakdown at LSOA level for England and Wales](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/lowersuperoutputareamidyearpopulationestimates) and their corresponding Local Authorities. Since most of our analysis has been conducted at LSOA level, we have created a separate table for this information. Unfortunately, neither Scotland nor Northern Ireland publish data at LSOA level.

The table contains a full breakdown of ages, with columns representing each age up to 90 years old. Residents of 90 years or older are grouped together. 

This data can be accessed via [this API](https://iqapi.azurewebsites.net/api/UkAgeBylandLsoa) and a notebook using this data can be found [here](https://coronavirus.data.gov.uk/cases).

#### England/Wales ethnicity distribution (LSOA level)

The source for this data is the most recent publicly available [UK census estimate (March 2011)](https://www.nomisweb.co.uk/census/2011/lc2101ew). The data has been directly transcribed from the public records available by selecting the type of area as super output area - lower. 

The data contains a breakdown of the total population of each LSOA by both race and ethnic group. All LSOAs in England and Wales are included. 

Data for other area types can be accessed through the nomisweb site by altering the dropdown filters.

This data can be accessed via [this API](https://iqapi.azurewebsites.net/api/UkEthnicityByLsoases) and a notebook using this data can be found [here](https://coronavirus.data.gov.uk/cases). 

#### Index of Multiple Deprivation (LSOA level)

The Index of Multiple Deprivation (IMD) is a measure of relative deprivation between different area groups. 

The IMD data for England at LSOA level is publicly made available through the [Ministry of Housing, Communities & Local Government](https://opendatacommunities.org/resource?uri=http%3A%2F%2Fopendatacommunities.org%2Fdata%2Fsocietal-wellbeing%2Fimd2019%2Findices), the most recent data having been collected in 2019.

Along with an IMD score and ranks for each LSOA in England, the data includes columns representing the variables used in calculating the IMD score. These variables include health indicators, employment percentages, crime levels and average income (amongst others). 

This data can be accessed via [this API](https://iqapi.azurewebsites.net/api/UKIMDBYLSOA ) and a notebook using this data can be found [here](https://coronavirus.data.gov.uk/cases). 

#### Area type mapping

Several different area types are present within our data and sometimes it is beneficial to be able to map between them. In order to facilitate this, here are some links to downloads from the ONS website:

[This link](https://geoportal.statistics.gov.uk/datasets/9f4c270148014f20bf24abff9a7aef62_0) is for mapping from LSOA to UTLA (Upper Tier Local Authority)

[This link](https://geoportal.statistics.gov.uk/datasets/lower-tier-local-authority-to-upper-tier-local-authority-april-2019-lookup-in-england-and-wales) is for mapping from LTLA (Lower Tier Local Authority) to UTLA

[This link](https://geoportal.statistics.gov.uk/datasets/postcode-to-output-area-to-lower-layer-super-output-area-to-middle-layer-super-output-area-to-local-authority-district-february-2018-lookup-in-the-uk) is for mapping between postcode, LSOA, MSOA (Middle layer Super Output Area) and LTLA

In order to gain a better understanding of the different area types and their corresponding coding systems, here are two supplementary links:

[This link](https://en.wikipedia.org/wiki/ONS_coding_system) explains the ONS coding system (LSOA/MSOA)

[This link](https://lgiu.org/local-government-facts-and-figures-england/#:~:text=In%20some%20areas%20of%20England,a%20single%20unitary%20authority%20instead.) explains the local government structure of the UK (LTLA/UTLA (In the data unitary councils appear as both lower and upper tier))


<details open>
<summary><strong>Section 2 API details</strong></summary>
<br>
  
| API Number | Method | Endpoint | Description |
|-----------|-------------|----------|----------|
|5    |GET      |https://iqapi.azurewebsites.net/api/UKPopulationDemographicData2018        |Linked dataset reporting on population demography and density at a lower and upper level Local Authority       |
|13      |GET             |https://iqapi.azurewebsites.net/api/UkEthnicityByLsoa          |Ethnicity groupings at LSOA level          |
|14     |GET             |https://iqapi.azurewebsites.net/api/UkAgeBylandLsoa          |Age breakdowns by LSOA          |
|15     |GET             |https://iqapi.azurewebsites.net/api/UKIMDBYLSOA          |Indices for Multiple Deprivation (IMD) at LSOA level          |

</details>

### 3. Industry and economy related data


#### Business Confidence March/April 2020

We have created two separate APIs for this data, which is concerned with survey responses from UK businesses at the onset of the pandemic. The data was initially gathered from the ONS Business Impact of Coronavirus survey and has been mapped to UK Business Counts data to generate a Business Risk metric. The first API (API Number 2), contains business counts according to survey response. The second that can be found (API Number 19) contains the Business Risk metric at a lower tier local authority level. The former API is the start point and the latter API is the end point of the following notebook which can be accessed [here] and used as a guide for working with this data.

#### Occupation, Employment & Furlough Data

In this subsection we detail the various Occupation, Employment & Furlough data that we have compiled and enriched from a variety of sources. A Jupyter Notebook that incorporates most of this data can be found [here](https://github.com/hldawe/hackathon/blob/master/Notebooks/Furlough%20Rates%20and%20Business%20Performance.ipynb). Please see this notebook for extra information and example use cases for these data sets.

**Furlough Rates**, API Number 7: This API retrieves data gathered from the ONS Business Impact of Coronavirus survey updated throughout the pandemic. The number of reporting industries has changed over time but this data set contains all reported data since the scheme started in late March of 2020.

**UK Occupations**, API Number 9: The breakdown of UK work force by Industry into the 21 Industry types, includes the number of workers per Industry at LA level.

**UK Job Type By Industry**, API Number 10: The breakdown of each above mentioned Industry into job types (number of occupations within the industry), this is the format that the following three APIs are in, therefore this dataset is used as a tool to map the following 3 API's data to LA. An example of this process can be found in the notebook linked [here](https://github.com/hldawe/hackathon/blob/master/Notebooks/Furlough%20Rates%20and%20Business%20Performance.ipynb)

**UK Occupations By Age**, API Number 8: Occupation type count at Industry level split by age brackets. The notebook linked above contains analysis using this data although the same methods can also be applied to the data from the following two APIs.

**UK Occupations By Ethnicity**, API Number 11: Occupation type count at Industry level split by ethnicity.

**UK Public/Private Occupations**, API Number 12: Occupation type count at Industry level split between public and private sector.


#### UK Companies House Data

This single API (API Number 1) contains a random sample of approximately 50,000 businesses across the UK which includes their SIC Code (sector/industry) as well as their name and address details.

 #### FTSE 100 Data

Single API which returns FTSE100 daily stock data for all 101 stocks which constitute the FTSE100 index, along with the FTSE100 index itself. The data is downloaded and updated daily from the Yahoo Finance website. Additionally, this data is augmented with Sector and Subsector information for each stock as classified by the London Stock Exchange. Date range is from January 1 2020 to the most recent date provided by the data source. A notebook explaining how the data is collated and organised can be found here.

<details open>
<summary><strong>Section 3 API details</strong></summary>
<br>
  

 
 
  
| API Number | Method | Endpoint | Description |
|-----------|-------------|----------|----------|
|      1    |      GET    |  https://iqapi.azurewebsites.net/api/CompaniesHouseData         |    Dataset reporting on all UK companies registered with Companies House      |
|      2    |      GET    |  https://iqapi.azurewebsites.net/api/BusinessConfidence         |    Enriched dataset reporting on relative business confidence across UK regions and business sectors, derived from workforce census data and ONS Covid-19 industry surveys
|      19   |      GET    |  https://iqapi.azurewebsites.net/api/UKBusinessRiskLTLA         |    Enriched dataset - estimates of business risk by industry sector and age-group at a lower level Local Authority level      |
|      7    |      GET    |  https://iqapi.azurewebsites.net/api/FurloughRate               |    Dataset reporting on furlough rates as reported periodically by the ONS throughout the pandemic
|      9    |      GET    |  https://iqapi.azurewebsites.net/api/UKOccupations              |    Occupations groupings |
|      8    |      GET    |  https://iqapi.azurewebsites.net/api/OccupationByAge            |    Occupations by age breakdown for England |
|      11   |      GET    |  https://iqapi.azurewebsites.net/api/UkOccupationByEthnicity    |    Occupations by ethnicity |
|      10   |      GET    |  https://iqapi.azurewebsites.net/api/UkJobTypeByIndustry        |    UK job types by industry group |
|      12   |      GET    |  https://iqapi.azurewebsites.net/api/UKPublicPrivateOccupations |    Occupations by public/private split |
|      ?    |      GET    | https://iqapi.azurewebsites.net/api/ftse                        |    FTSE100 Stock Index data from the beginning of 2020 to present |

</details>

### 4. GIS data

GIS (Geographical Information Systems) data contains geometric information and can be used to draw maps. There were a number of GIS data sources we used and they are listed below:

1) The geojson file found [here](https://coronavirus.data.gov.uk/cases) was used in a lot of the work we carried out including the [business risk notebook](https://coronavirus.data.gov.uk/cases) and the [furlough rates notebook](https://coronavirus.data.gov.uk/cases). It contains geometric data for the lower tier local authorities throughout the UK.

2) The data found [here](https://datashare.is.ed.ac.uk/handle/10283/2546) was used in the [vaccine distribution notebook](https://coronavirus.data.gov.uk/cases). It is a shape file with LSOA boundaries for England and Wales.

3) The [care homes notebook](https://coronavirus.data.gov.uk/cases) used a shape file found [here](https://geoportal.statistics.gov.uk/datasets/b216b4c8a4e74f6fb692a1785255d777_0?geometry=-89.275%2C33.725%2C132.736%2C69.287). This link contains shape files for different types of areas within the UK.

4) Finally, linked [here](https://geoportal.statistics.gov.uk/datasets/f341dcfd94284d58aba0a84daf2199e9_0) is the MSOA shape file which matches up with the latest MSOA incidence data.


<details open>
<summary><strong>Section 4 API details</strong></summary>
<br>
  
| API Number | Method | Endpoint | Description |
|-----------|-------------|----------|----------|
|           |             |          |          |
|           |             |          |          |
|           |             |          |          |

</details>


### 5. Other data

#### England Care Home Postcodes 2016

Single API (API no. 6) which returns names and postcodes of care homes in England as of 2016.

<details open>
<summary><strong>Section 5 API details</strong></summary>
<br>
  
| API Number | Method | Endpoint | Description |
|-----------|-------------|----------|----------|
|      6     |      GET       |    https://iqapi.azurewebsites.net/api/EnglandCareHomes      |    Postcodes of all Care Homes in England as of 2016     |
|           |             |          |          |
|           |             |          |          |

</details>



