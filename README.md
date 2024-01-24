
# Socio-Demographic Features Worldwide

## Objective
The main purpose of the dashboard is to generate visuals that allow the analysis of the main social and demographic features across the world. The original dataset: Demographic and Socio-economic (full dataset) from UNESCO, lists all the countries and crucial indicators such as total population, population per age group, GDP, GNI, Fertility Rate, Infant Mortality Rate, and others. These indicators were registered over a period of 6 years, from 2018 to 2023. Most of them do not have data collected for 2023. 
The dataset contains 232 countries which made it difficult to show differences between them without using a broader classification. This is why an additional dataset is used to reference the indicators based on regions (continents) or subregions (how continents are divided).  For this, the website REST Countries and its API were used; other information such as language and capital were also included. This way the two resulting tables can be related through the country field present on both of them. 

## Steps Followed
### UNESCO Dataset
1.	Removed repeated column: Time.
2.	Removed column that contains the abbreviation for each indicator: Demo_Ind.
3.	Pivot Indicator Column: It was deemed more appropriate to analyze the data to convert the indicators into a column each. 
The resulting columns are Country, Location (abbreviation of the countries’ name), Time and 35 indicators from which 10 of them were used. 

### REST Country Dataset
1.	Removed all currency-related columns: For this dashboard, I decided to remove them because each currency has a different column in which they have only one value based on the country they were representing. The rest of the values were null. Furthermore, I wanted to express indicators such as GDP in terms of the American dollar for standardization. The columns related to the symbol of each currency were removed as well.
2.	Removed Official countries’ name and translations: The data had one column for each official name in the original country’s language and it had translations to different languages like French, English and others. It was the same scenario as the currency one: each column had values based on the country they were representing, and the rest of the values were null. Also, this data doesn’t add significant value to the study. 
3.	Removed GINI coefficient: columns related to this measure were removed because all indicators were taken from a single source (UNESCO). 
4.	Others: The dataset contained a column for the start of the week in each country and another one for the postal codes, this information was not taken into consideration and the two columns were removed. 
5.	Expand lists on Language Column: The column related to the official languages for each country had the information as lists, these were expanded, one row for each language. 
6.	New measure – Area: As the number of rows increased due to the expansion of the language lists when the field area was used, it was summing up the measure the same number of times as the number of languages the particular country had. To fix this issue, a new column named Area_New was created using the following DAX formula: 

            Area_New = SUMX(GROUPBY(More, More[Country], More[area]), [area])

### Relationship between the two tables
A relationship between the two tables was established using the Country field present in both. 

## Insights
For now, the insights will be focused on the Americas.

### Overview
The Overview shows general information about the different regions such as population, area, countries that belong to a specific region or subregion and their corresponding flag.  
America is an extensive piece of land and frequently is seen as two continents: North America and South America. A few details we can observe about them are the following:
-	North America is composed of three subregions: North America, Central America and the Caribbean. While South America is a single subregion on its own. 
-	The most populated region is North America. It encompasses the first and third most populated countries: The United States of America and Mexico. 
-	North America is also the vastest area between the two regions. 
-	South America includes the second most populated country: Brazil, and the largest one in that subregion. 
![SD_Overview](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/0a762cff-7083-4a2e-875d-b03999916885)

### GDP/GNI
UNESCO presents data up to 2022 regarding GDP per capita (US$) and GNI per capita (current US$) for the Americas.
-	For 2022, the GDP per capita was higher in North America, especially in North America (subregion) and the Caribbean. 
![GDP_North](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/87056622-7d74-4b85-8f74-891a749d8dfd)

-	South America presented a higher GDP per capita than Central America. 
![GDP_South](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/c202cc94-73fc-472e-afa4-180f204b994f)

-	The GNI is presented similarly for this same year for the two regions and subregions.
-	For North America (subregion), the GDP growth rate was larger for Canada. Second and third places were occupied by Mexico and Bermuda. 
-	The GNI per capita in US dollars for the North American subregion was $264 980 which represents 50.53% of the North American region. 
![GDP_NorthAmerica_subreg](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/e3f27339-d8a1-40f7-87dc-0312223e7bb7)

### Population
This tab focuses on showing more details about the population for 2021; the last year UNESCO has information about Infant Mortality rate and Life Expectancy at birth. 
-	As was mentioned before, North America encompasses a higher number of people in its territory. In this area, the North American subregion presents a larger population. 
-	The infant mortality rate is lower in the North American subregion with 7 infants per 1000 live births, followed by Central America with 12 infants/1000 live births and the Caribbean having the higher infant mortality rate with 16 infants/1000 live births. 
-	From the North American subregion, Canada presented the lowest rate with 4 infants per 1000 live births. 
-	From the Caribbean subregion, Haiti showed the deadliest rate with 45 infants per 1000 live births.  
-	In regard to the Life expectancy at birth, the three subregions presented similar numbers: 76 years for North America, 73 years for the Caribbean and 72 years for Central America. 
-	Canada presented the highest life expectancy with 83 years old. 

![Pop_NorthAmerica](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/2fbcd5fe-21e9-47bc-9ff7-4a9167dc6123)


![Pop_MortalityRate_TheCaribbean](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/d03efc77-ef8a-48a4-bbec-2bb325252ab2)


![Pop_LifeExpectancy](https://github.com/StellaMassaRebolledo/Dashboards/assets/72529414/c77f05fd-7440-48ec-a21d-22a74dd8c17e)


## References
-	UIS Statistics – UNESCO. UIS Database. http://data.uis.unesco.org/Index.aspx?DataSetCodeEDULIT_DS&popupcustomisetrue&langen#
-	REST Countries. https://restcountries.com/
