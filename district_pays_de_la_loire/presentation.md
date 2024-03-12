# Temperature analysis 2023 - Pays de la Loire 

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
The data comes from ![here](https://odre.opendatasoft.com/explore/dataset/temperature-quotidienne-regionale/information/?disjunctive.region) and show the daily temperature (in °C) from 2016 to nowadays in different districts in France. There are 3 types categories of temperature: the maximum _(Tmax)_, the minimum _(Tmin)_, and the average _(Tavg)_. <br>

## 2) Preprocessing: clean, filter, adjust the raw dataset
I extracted the working data from the raw dataset and grap the temeprature of 2023 in the district of Pays de la Loire. Before analysis it, I added useful columns: Year, Month and Day columns. After this step, the data looks like:
<p align="center">
  <img src="pizza_image.jpg" width="300"/>
</p>
The next thing to to is analysing this data with SQL and answer interesting questions!

## 3) TOP 5 coldest VS TOP 5 hottest months
![this screenshot](/district_pays_de_la_loire/tables_sql_created/top5_coldest.PNG)






 


