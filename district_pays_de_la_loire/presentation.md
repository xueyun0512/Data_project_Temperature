# Temperature analysis 2023 - Pays de la Loire 
> [!NOTE]
> This is a self made project, NOT A scientific report

## Introduction 
This a the very first project of the repertory _Temperature analysis_. In this folder, I work with temperature datasets of 2023 in the district of Pays de la Loire. <br> The objectif of this project is to answer some questions one may ask given this dataset and offer a visualisation tool in order to see the global trend of the temperature variation. <br>
**All the SQL code is available in the file _path_.**

## Skills demonstrated
- Excel - cleaning and filtering 
- SQL analysis - _OVER(PARTITION BY   ORDER BY), ROW_NUMBER(), CASE, ALTER TABLE_
- Power BI - Visualization 

## Table of content 
1) Input data
2) Preprocessing: clean, filter, adjust the raw dataset
3) TOP 5 coldest VS TOP 5 hottest months 
4) Biggest temperature variation in a day for each month
5) The average temperature grouping by season
6) How to get the last day of each month?

## 1) Input data
The data comes from [here](https://odre.opendatasoft.com/explore/dataset/temperature-quotidienne-regionale/information/?disjunctive.region) and show the daily temperature (in °C) from 2016 to nowadays in different districts in France. There are 3 types categories of temperature: the maximum _(Tmax)_, the minimum _(Tmin)_, and the average _(Tavg)_. <br>

## 2) Preprocessing: clean, filter, adjust the raw dataset
Using Excel, I extracted the working data from the raw dataset and grap the temperature of 2023. I also added useful columns: Year, Month and Day columns. This completed, I was ready to treat my data with SQL. 
<p align="center">
  <img src="pizza_image.jpg" width="300"/>
</p>

Since I was interested by the data of the district Pays de la Loire. I created a new table **_loire_**. For the rest of the project, I will use this new table. Moreover, the temperatures are given in decimal. We convert them into integers using the function _ROUND()_ to make it easier to interpret. 

```ruby
SELECT *
INTO loire
FROM temperature
WHERE District = 'Pays de la Loire';
```
The next thing to to is analysing this data with SQL and answer interesting questions!

## 3) TOP 5 coldest VS TOP 5 hottest months
As it could be seen from the table above, the 3 coldest months are in Winter and the hottest in summer. The lowest temperature of 6.83°C is observed in January and the highest is in June with 21.67°C. To be honest, I was surprised to see June (considered as in Spring) hottest than the month of July. But with hindsight, the district Pays de la Loire is located in the west coast in France so it could explain this. 

TOP 5 Coldest Months        | TOP 5 Hottest Months  
:------------: |:-------------:
![](/district_pays_de_la_loire/tables_sql_created/top5_coldest.PNG) | ![](/district_pays_de_la_loire/tables_sql_created/top5_hottest.PNG)

## 4) Biggest temperature variation in a day for each month
As the maximum and the minimum daily temperatures are given, one may ask what is the biggest temperature with a day. The variation is know as the difference between the highest and the lowest : _δT = Tmax - Tmin_ <br>
Using the following code: 
```ruby
SELECT Month, MAX(Tmax-Tmin) AS Temperature_Variation
FROM loire 
GROUP BY Month
ORDER BY Temperature_Variation DESC;
```
The biggest temperature variation is δT = 20°C and occured in July. This resulat is not surprising as the temperature is higher in summer so the difference should also be high. 

## 5) The average temperature grouping by season

There is temperature data for all months of the year. It could be interested to group by them in season. 


 


