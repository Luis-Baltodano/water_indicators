# Water indicators in Latin America & Caribbean

## Table of content
- [Project overview](#Project-overview)

### Project overview
Access to safe water and sanitation is a basic human need. Nontheless billions of people will lack access to these basic services in 2030, according to the United Nations. This report helps to understand the actual state of the resource in Latin America and Caribbean, by analyzing the following indicators, since 1998 to 2020: Water stress, Freshwater withdrawal by economic sectors, water productivity, income level.

### Data sources
  1. Countries indicators data come from the World Bank's World Economic Development database, the data can be downloaded in the CSV file.
  2. Basic information about countries like name, countrie's codes based in ISO 31666. Were obtained in the next API: https://api.worldbank.org/v2/country/all
  3. Countrie's flags were obtained in the following source: https://flagsapi.com/

### Data cleaning/preparation
All the ETL process was performed with Power Query in the Power BI Desktop software, following the next steps:

  1. Data loading and inspection.

     The table had an impractical structure, having all the years in different columns, selecting all the years columns and using the Unpivot columns tool gives a better structure to work with.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/024f395d-954f-4381-8ec6-c8a49e381b5d)
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/4b3516c8-3aaf-4ad6-b133-5bd0047e7975)

     The countries general information was downloaded in a json file and then parsed to obtained a table with needed information like ISO codes and countrie's income level.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/cb5abf5d-7ff0-4a65-8e70-6b9043d8a84e)
     
     Then this query was merged with another query that only had the countries in the region being analyzed, Latin America and Caribbean, and the population. Filtering just the needed data.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/31aceb60-fc4b-4c31-b573-bc350a3f438a)

     To this country query was added the flag API, adding a custom column that concatenate the pre-defined text of the API and the country ISO code.
     
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/3aafa3a5-a4f9-4982-badb-e1adbc2c582c)

2. Missing values

   The column value for every series downloaded had many missing values, denominated by double hyphen (--), the most missing values belonged to years 2022 and 2023, so these years were excluded from the analysis.
   
   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/d76ef7e9-8a59-4e84-8639-bc9312fcc72a)

   Then the missing values were replaced by empty values, so they don't interfer with the following calculations.
   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/eaedc08f-5cc9-4d8f-b810-6a2d80de1aaf)

   A correct name and data type was given to each column, then created the relationship between tables.

   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/f61e0a0f-f144-44c5-94af-63e88163d41a)

### Exploratory Data Analysis

1. Water stress status

According to the Food and Agriculture Organization of the United Nations, a value of 40% of water withdrawal as a proportion of available resource may considered as high water stress. So first we need to understand the actual state of the region, using values o

### Data Analysis

### Results/Findings

### Recommendations

### Limitations

   


   





    


     

     

     
     


