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

### Data Analysis

1. Water stress status

According to the Food and Agriculture Organization of the United Nations, a value of 40% of water withdrawal as a proportion of available resource may considered as high water stress. So first we need to understand the actual state in the region, using values of the year 2020, because this was the year with more data. Seeing that only three countries were in high stress for that year and only three in medium range, considering that in the region are forty-two countries, we can say that there was enough water resource to supply all economic activities in the region.

![image](https://github.com/user-attachments/assets/64c061f8-a504-452c-993d-4bc7427d5998)

The countries with more water stress are located in the Caribbean region.

![image](https://github.com/user-attachments/assets/90d7abf5-85bc-4669-ba39-ca6b248d617e)

We can see that geographical location has a greater impact on water stress. Islands tend to experience higher water stress, for reasons like limited resources, dependency on rainfall and high domestic demand. with high population density, tourism, and agriculture, islands may have a water demand that exceeds the available supply. The Caribbean region experiences higher stress, with countries in this region having lower consumption.

![image](https://github.com/user-attachments/assets/183cd45b-1231-40b8-b35c-f400e09b5626)


To get the different values for each indicator was created a SUM measure of the values, which was evaluated with the calculate function for the indicator of interest and the year of study in the case of some measures like the water stress.

![image](https://github.com/user-attachments/assets/b521a2e3-a434-4be6-9fea-173a53e8e5db)

2. Freshwater withdrawal by sector

The data provided by the World Bank determined three clasifications of economic activities: **Agriculture, Domestic and Industry** being the agriculture the sector that used the most part of the resource in almost every country in the region. Understanding these the next step was to see the changes of the water withdrawal in the time and by income level.

First were created a different measure for calculate the average value in percentage of the water withdrawal for each sector.

![image](https://github.com/user-attachments/assets/7f9bfab1-f7d6-4689-9e78-0160be5310ed)

The withdrawal in the agriculture sector decrease 5.6% from 1998 to 2020, the domestic sector present an increase of 7.3% and the industry an increase of 2%. 

![image](https://github.com/user-attachments/assets/9d89fc55-054b-465c-a3a3-5a493ed3a0cb)

This does not mean that the total water used in agriculture had decreased, on the contrary, the total volume of water withdrawal has increase over the years, from 133 billions to 216 billions of m³. So the variations in the perecentage value may indicate the increased in the access to water for urban and rural population in the region. 

![image](https://github.com/user-attachments/assets/9f7db121-4017-4f14-9739-cc26b56742a6)

To calculate the volume in cubic meters of water withdrawal by sector we just multiply the total water withdrawal given by the World development indicator, by the average percentage for each sector, multipliyin by 1 billion to have complete values.

![image](https://github.com/user-attachments/assets/cf8f82a6-994e-43bb-b2b3-e52a9e31c8e4)

![image](https://github.com/user-attachments/assets/58fd5152-ed8f-4e53-9b1c-1c17a332e3f3)

We can see that the three sectors has increased the total volume of water used, but this had not a significant impact in the water stress index along the period. The water stress in the regiong augment 0.9% from 1998 to 2020.

![image](https://github.com/user-attachments/assets/79d59689-058c-4349-8220-9e5b2ae5c7e2)

3. Country analysis

Drilling through each country we can see some relevant data like population in the year 2020, the GDP and the income level clasification. The agriculture sector represents the major withdrawal of freshwater, mostly in Lower and Upper middle income countries. In the analysis by country we can see the water usage distribution along the three economic sectors and the water productivity factor for agriculture.

![image](https://github.com/user-attachments/assets/c542b325-6be6-4567-91e3-b05e4c91b052)

The water productivity factor helps to understand the water use efficiency in terms of money, it is expressed in dollar by cubic meter. This factor is important to support sustainable water management, and maximizing the economic and environmental benefits derived from water resources.

The World Economic Development database gives us the series indicator of percentage of GDP for agricultre, foresty and fishing, with the GDP we can calculate the amount of money for the sector.

![image](https://github.com/user-attachments/assets/5c720eeb-caba-40ea-aeb2-a6a5eec798dd)

With the percentage of water withdrawal for agricultre and the total water withdrawal expressed in cubic meters, was calculated the amount of cubic meters for agriculture.

![image](https://github.com/user-attachments/assets/a59ce156-488c-4a82-b3c8-c89fe43c260a)

Then just need to divide the GDP for agriculture by the water withdrawal for this sector.

![image](https://github.com/user-attachments/assets/fa674b16-bf1c-4cf4-bacd-3e746d4a275f)

### Results/Findings

1. There is enough resource to supply the needs in all social and economics sector in the region. But some factors like the geographical location (islands) can derrived in a limited water resource, increasing the water stress.

2. The agriculture and domestic sectors have increased their water withdrawal. Which means an increase in drinking water coverage, but also that there must be special attention to the agriculture activities to guarantee an efficient use of the resource. Though industry sector has increased its water needs, the growth of this sector had been slower than agriculture and domestic.

3. The water productivity in agriculture can be affected for different factors beside the water withdrawal. A further analysis in this topic for those special years with peaks can help to understand how to inprove the benefits reducing the wastes in water resource by inproving these other related factors.

4. 



### Recommendations

### Limitations

   


   





    


     

     

     
     


