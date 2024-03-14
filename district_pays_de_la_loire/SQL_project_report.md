# Temperature analysis - Pays de la Loire - 2023
> [!NOTE]
> This is NOT a scientific report

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
7) Visualisation in Power BI

## 1) Input data
The data comes from [here](https://odre.opendatasoft.com/explore/dataset/temperature-quotidienne-regionale/information/?disjunctive.region) and show the daily temperature (in °C) from 2016 to nowadays in different districts in France. There are 3 types categories of temperature: the maximum _(Tmax)_, the minimum _(Tmin)_, and the average _(Tavg)_. <br>

## 2) Preprocessing: clean, filter, adjust the raw dataset
Using Excel, I extracted the working data from the raw dataset and grap the temperature of 2023. I also added useful columns: Year, Month and Day columns. This completed, I was ready to treat my data with SQL. 
<p align="center">
  <img src="/district_pays_de_la_loire/tables_sql_created/view_data_excel.PNG" width="800"/>
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
```ruby
SELECT TOP 5 Month, CAST(AVG(Tavg) AS DECIMAL(4,2)) AS Top5_coldest_months 
FROM loire
GROUP BY Month
ORDER BY Top5_coldest_months ;
```
The code is the same for the hottest months but we add _DESC_ at the end. This returns us the two following tables:
TOP 5 Coldest Months        | TOP 5 Hottest Months  
:------------: |:-------------:
![](/district_pays_de_la_loire/tables_sql_created/top5_coldest.PNG) | ![](/district_pays_de_la_loire/tables_sql_created/top5_hottest.PNG)

## 4) Biggest temperature variation in a day for each month
As the maximum and the minimum daily temperatures are given, one may ask what is the biggest temperature with a day. The variation is know as the difference between the highest and the lowest : _δT = Tmax - Tmin_ <br>

The biggest temperature variation is δT = 20°C and occured in July. This resulat is not surprising as the temperature is higher in summer so the difference should also be high. 

## 5) The average temperature grouping by season

There is temperature data for all months of the year. It could be interested to group by them in season. We add a column _season_ to the table _loire_ as follow:
```ruby
 ALTER TABLE loire
  ADD season AS
    CASE
      WHEN Month in ('mars','avr','mai') THEN 'Spring'
      WHEN Month in ('juin','juil','août') THEN 'Summer'
      WHEN Month in ('sept','oct','nov') THEN 'Fall'
      ELSE 'Winter'
    END
```
Now, the temperature per season can be seen:<br>

![](/district_pays_de_la_loire/tables_sql_created/temperature_season.PNG)

## 6) How to get the last day of each month?
One may also want to know which day is the last day for each month. Every month does not end with the same day_number. It could be 30, 31 or even 28 or 29 for the month of February! But no worries. We counteract this issue using the functions _ROW_NUMBER()_ and  _OVER(PARTITION BY   ORDER BY)_. Given a year and a month, the following SQL query will create a _LastDay_ column which is 1 for the last day, 2 for the penultimate last day and so on. 

```ruby
SELECT Date,Month,Day,Tavg,
ROW_NUMBER() OVER (PARTITION BY Year, Month ORDER BY Day DESC) AS Last_Day
INTO LastDay_temperature 
FROM loire;
```
For instance, the table regarding the month of March is:

 ![](/district_pays_de_la_loire/tables_sql_created/last_day.PNG)

Therefore, if one needs the last day, one may just add _WHERE LastDay =1_

## 7) Visualisation in Power BI
Visualising the data is a crucial step in the analysis task. Of course, queries are really important in order to understand deeply the dataset. But we do need a dashboard to summarize our analysis and make it straighfoward to anyone not involved in the project to have quickly an idea about the the project. <br>
Using Power BI, I was able to display the temperature trend and gather all relevant information I found through my SQL queries. 

 ![](/district_pays_de_la_loire/dashboard_powerbi.PNG)

## Conclusion
Through this project, I have learnt how to explore data with SQL queries. It was amazing to dive into the dataset and use multiple functions to extract the information I was looking for. Building a Power BI dashboard was also extremely satisfying! I do appreciate customize every single detail! <br>

I hope this little project has been enjoyable for you as it was for me! 
Thank you for reading it and have a good day ;)

Olivia 
