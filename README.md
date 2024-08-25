# Water indicators in Latin America & Caribbean

## Table of content
- [Project overview](#Project-overview)
- [Data sources](#Data-sources)
- [Data cleaning/preparation](#Data-cleaning/preparation)
- [Data Analysis](#Data-Analysis)
- [Results/Findings](#Results/Findings)
- [Recommendations](#Recommendations)


### Project overview
Access to safe water and sanitation is a basic human need. Nonetheless, billions of people will lack access to these basic services by 2030 unless progress quadruples, according to the United Nations. This report helps to understand the current state of these resources in Latin America and the Caribbean by analyzing the following indicators from 1998 to 2020: water stress, freshwater withdrawal by economic sectors and water productivity.

### Data sources
  1. Countries' indicators data from the World Bank's World Economic Development database, the data can be downloaded in CSV format. The file is in the assets folder.
  2. Basic information about countries, such as names and country codes based on ISO 3166-1, was obtained from the following API: https://api.worldbank.org/v2/country/all
  3. Countrie's flags were obtained from the following source: https://flagsapi.com/

### Data cleaning/preparation
All the ETL process were performed with Power Query in the Power BI Desktop software, following these steps:

  1. Data loading and inspection.

     The table had an impractical structure, with all the years in different columns. Selecting all the year columns and using the Unpivot Columns tool provides a better structure to work with.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/024f395d-954f-4381-8ec6-c8a49e381b5d)
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/4b3516c8-3aaf-4ad6-b133-5bd0047e7975)

     The countries' general information was downloaded in a JSON file and then parsed to obtained a table with needed information like ISO codes and countries' income level.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/cb5abf5d-7ff0-4a65-8e70-6b9043d8a84e)
     
     Then, this query was merged with another query that only included countries in the region being analyzed, Latin America and the Caribbean, and their populations, filtering only the needed data.
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/31aceb60-fc4b-4c31-b573-bc350a3f438a)

     To this country query, the flag API was added by creating a custom column that concatenates the predefined text of the API with the country ISO code.
     
     ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/3aafa3a5-a4f9-4982-badb-e1adbc2c582c)

2. Missing values

   The column values for each series downloaded had many missing values, denoted by double hyphens (--). Most of the missing values belonged to the years 2022 and 2023, so these years were excluded from the analysis.
   
   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/d76ef7e9-8a59-4e84-8639-bc9312fcc72a)

   Then, the missing values were replaced with blanks to ensure they do not interfere with the subsequent calculations.
   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/eaedc08f-5cc9-4d8f-b810-6a2d80de1aaf)

   A correct name and data type were assigned to each column, and then the relationships between tables were created.

   ![image](https://github.com/Luis-Baltodano/water_indicators/assets/163363364/f61e0a0f-f144-44c5-94af-63e88163d41a)

### Data Analysis

1. Water stress status

According to the Food and Agriculture Organization of the United Nations, a water withdrawal rate of 40% of available resources is considered high water stress. To understand the current state in the region, we use data from the year 2020, which had the most comprehensive information. With only three countries experiencing high water stress and three in the medium range out of a total of forty-two countries in the region, we can conclude that there was generally enough water resource to support all economic activities in the region.

![image](https://github.com/user-attachments/assets/64c061f8-a504-452c-993d-4bc7427d5998)

The countries with the highest water stress are located in the Caribbean region.

![image](https://github.com/user-attachments/assets/90d7abf5-85bc-4669-ba39-ca6b248d617e)

We can observe that geographical location has a significant impact on water stress. Islands tend to experience higher water stress due to factors such as limited resources, dependency on rainfall, and high domestic demand. With high population density, tourism, and agriculture, islands may face water demand that exceeds the available supply. The Caribbean region, in particular, experiences higher water stress, with countries in this region having lower water consumption.

![image](https://github.com/user-attachments/assets/183cd45b-1231-40b8-b35c-f400e09b5626)

To obtain the different values for each indicator, a SUM measure was created for the values. This measure was evaluated using the CALCULATE function to focus on the indicator of interest and the specific year of study, such as in the case of water stress.

![image](https://github.com/user-attachments/assets/b521a2e3-a434-4be6-9fea-173a53e8e5db)

2. Freshwater withdrawal by sector

The data provided by the World Bank categorized economic activities into three classifications: **Agriculture, Domestic and Industry**Agriculture was the sector that used the majority of the water resources in almost every country in the region. With this understanding, the next step was to analyze changes in water withdrawal over time.

First, a different measure was created to calculate the average value in percentage of water withdrawal for each sector.

![image](https://github.com/user-attachments/assets/7f9bfab1-f7d6-4689-9e78-0160be5310ed)

Water withdrawal in the agriculture sector decreased by 5.6% from 1998 to 2020, while the domestic sector showed an increase of 7.3%, and the industry sector saw an increase of 2%. 

![image](https://github.com/user-attachments/assets/9d89fc55-054b-465c-a3a3-5a493ed3a0cb)

This does not mean that the total water used in agriculture has decreased. On the contrary, the total volume of water withdrawal has increased over the years, from 133 billion to 216 billion m³. The variations in the percentage values may indicate increased access to water for the urban and rural populations in the region.

![image](https://github.com/user-attachments/assets/9f7db121-4017-4f14-9739-cc26b56742a6)

To calculate the volume in cubic meters of water withdrawal by sector, we simply multiply the total water withdrawal provided by the World Development Indicators by the average percentage for each sector, and then multiply by 1 billion to obtain complete values.

![image](https://github.com/user-attachments/assets/cf8f82a6-994e-43bb-b2b3-e52a9e31c8e4)

![image](https://github.com/user-attachments/assets/58fd5152-ed8f-4e53-9b1c-1c17a332e3f3)

We can see that the total volume of water used has increased across all three sectors. However, this has not had a significant impact on the water stress index over the period. The water stress in the region increased by only 0.9% from 1998 to 2020.

![image](https://github.com/user-attachments/assets/79d59689-058c-4349-8220-9e5b2ae5c7e2)

3. Country analysis

Drilling through each country, we can observe relevant data such as the population in the year 2020, GDP, and income level classification. The agriculture sector represents the major withdrawal of freshwater, primarily in lower and upper middle-income countries. In the country-level analysis, we can see the distribution of water usage across the three economic sectors and the water productivity factor for agriculture.

![image](https://github.com/user-attachments/assets/c542b325-6be6-4567-91e3-b05e4c91b052)

The water productivity factor helps to understand water use efficiency in monetary terms, expressed in dollars per cubic meter. This factor is important for supporting sustainable water management and maximizing the economic and environmental benefits derived from water resources.

The World Economic Development database provides a series indicator for the percentage of GDP from agriculture, forestry, and fishing. With the GDP data, we can calculate the monetary value for the sector.

![image](https://github.com/user-attachments/assets/5c720eeb-caba-40ea-aeb2-a6a5eec798dd)

Using the percentage of water withdrawal for agriculture and the total water withdrawal expressed in cubic meters, the amount of cubic meters used for agriculture was calculated.

![image](https://github.com/user-attachments/assets/a59ce156-488c-4a82-b3c8-c89fe43c260a)

Then, we just need to divide the GDP for agriculture by the water withdrawal for this sector to obtain the water productivity factor.

![image](https://github.com/user-attachments/assets/fa674b16-bf1c-4cf4-bacd-3e746d4a275f)

### Results/Findings

1. There is enough resource to supply the needs of all social and economic sectors in the region. However, factors like geographical location (islands) can lead to limited water resources, increasing water stress.

2. The agriculture and domestic sectors have increased their water withdrawal, indicating an increase in drinking water coverage. However, there must be special attention to agricultural activities to ensure efficient use of the resource. Although the industry sector has increased its water needs, its growth has been slower than that of agriculture and domestic sectors.

3. Water productivity in agriculture can be affected by various factors besides water withdrawal. Further analysis of this topic for specific years with peaks can help to understand how to improve benefits and reduce water resource waste by enhancing these other related factors.

4. Although the data does not indicate significant problems with the resource, this does not fully represent the reality of water management in the region. Other factors must be analyzed to gain a better understanding of the social and economic impact of how each country manages its available resources. Factors such as people using safely drinking water services and basic sanitation, public and private investment in water and sanitation, and renewable internal freshwater should be considered.


### Recommendations

1. For a more detailed analysis, it is recommended to seek data from internal and official sources for each country, as the data provided by the World Bank may be limited for many countries in the region.

2. Given the significant differences between Caribbean, Central American, and South American countries, it is recommended to analyze each of these regions separately for a more in-depth study.
### Limitations

There are many missing values in the World Bank database. Many relevant indicators for the study had to be excluded because of this.

   


   





    


     

     

     
     


